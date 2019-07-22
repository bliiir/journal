### Journal
*Rasmus Groth, Betahaus, Barcelona, 20181009*

# Deploy a project to AWS

## Local

### Install database

#### MySQL
...

#### PostgreSQL
Download [PostgreSQL](https://www.postgresql.org/download/macosx/) and go through the installation process.
If you pick the EDB enterprise option, you will get pgAdmin bundled with it. If not, you can download it [here](https://www.pgadmin.org/download/pgadmin-4-macos/)

Install database connector. Make sure you are in your venv.
```
pip install psycopg2-binary
```

### Dump the sql data
This takes the schemas and the content of you database and dumps it into a json file.
[Full Walkthrough](https://gist.github.com/sirodoht/f598d14e9644e2d3909629a41e3522ad)

```
python3 manage.py dumpdata > datadump.json
```
### Switch database in Django
This swithches the database in Django but retains the models so you still have the actual models in code in Django in models.py.

From
```py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```
To
```py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'books',
            'USER': 'postgres',
            'PASSWORD': os.environ['POSTGRESS_SECRET_KEY'],
            'HOST': 'localhost',
            'PORT': '',
    }
}
```
But there is no content in the database yet - let's sort that out.
```
python3 manage.py migrate --run-syncdb
```
This creates the tables in the new database
```
python3 manage.py shell
```
Clear the database to ready it for the content
```
>>> from django.contrib.contenttypes.models import ContentType
>>> ContentType.objects.all().delete()
>>> quit()
```

### Load the data
```
python3 manage.py loaddata datadump.json
```
You now have tables and content in the Django ORM, but they aren't in the actual datbase yet. We need to make migrations for that to happen.

### Make Migrations

```py
python manage.py makemigrations
python manage.py migrate
```
You should now have all the tables and data in your new database.

### Git
Create a repo for the project on github and push the local to the remote. We are going to clone this repo onto the aws server when we are done with the setup.

---

## Remote

### Initialize AWS server
[Launch EC2 instance with Ubuntu Server](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#LaunchInstanceWizard:)

#### Set Security groups
| Type | Protocol | Port range | Source | Description |
| :-- | :--| :-- | :-- | :-- | :--|
| SSH |  TCP | 22 | My IP x.x.x.x/x | SSH for admin |
| HTTP |  TCP | 80 | Anywhere x.x.x.x/x | Public access |
| Custom TCP |  TCP | 8000 | Anywhere x.x.x.x/x | Testing |

 Create key pair and download as .pem file

### Connect to the AWS server
* Download .pem file
* Move .pem file to `~/.ssh` folder
* Change .pem file rights: `chmod 400 keyfilename.pem`
* Find the ip number for the server on [aws dashboard](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#Instances:sort=instanceId)
* SSH onto server: `ssh -i "~/.ssh/filename.pem" ubuntu@xx.xx.xx.xx`

You should see something like this:

```py
...
Warning: Permanently added '54.187.55.203' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-1021-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri Oct 12 12:56:13 UTC 2018

  System load:  0.0               Processes:           84
  Usage of /:   13.3% of 7.69GB   Users logged in:     0
  Memory usage: 13%               IP address for eth0: 172.30.2.72
  Swap usage:   0%

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```
Nicely done! You have installed an operating system on a remote server and you are now working on the server through the terminal. Take a minute to appreciate the fact that you are manipulating hardware that is probably thousands of miles away through your console - rock'n'roll!! 🤟

### Set up AWS web server
In the terminal you just opened, type in the commands below. Note that each one will trigger a cascade of messages and a few interactions in the terminal:

```
sudo apt-get update
sudo apt-get install python3-pip
sudo apt-get install python3-dev
sudo apt-get install nginx
sudo apt-get install curl
sudo apt-get install python3-venv
```

Great - you have now installed the webserver on top of the Ubuntu OS you had already installed. Time to get back to your Django project.

### Set up project
#### Git
* `git init`
* `git clone https://github.com/userName/repoName.git`

#### Virtual Environment
* `python3 -m venv env`
* `source env/bin/activate`
* `pip install -r requirements.txt`

#### Python Database connections
| Database | Command |
| :-- | :-- |
| MySql | `pip install mysqlclient` |
| PostgreSQL | `pip install psycopg2` |

#### Gunicorn
* pip install gunicorn


### Database install / Amazon RDS
Before we move on to Django, we have to set up a database on AWS. For this we will use their RDS service. RDS means *Relational Database Service*. It is simply a server dedicated to running your database. In this example I will be using a PostgreSQL installation, but the steps are similar if you use MySQL or other relational databases. If you are using Sqllite, you can skip this step as your database is running on the same EC2 instance we just set up.

Go to the [AWS RDS dashboard](https://us-west-2.console.aws.amazon.com/rds/home?region=us-west-2#) and click Launch Instance. On the following screen click PostgreSQL and next:

![](https://www.dropbox.com/s/hunqbp5itb2fvr3/Screenshot%202018-10-14%2017.17.39.png?raw=1).

On the next screen you set your instance name, master username and passwords. If you are having trouble with this, check out the aws guide [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateDBInstance.html).

Remember to set the public accessibility to **yes** open the RDS to the EC2 IP number we are running the webserver on. I had to fiddle a bit with the security groups to make it work. My conclusions are - do not use the same security group you are using for the EC2 as that will mean that port 80 etc is open. Create a new one dedicated to the RDS server.

When you are done, go to the [RDS instances page](https://us-west-2.console.aws.amazon.com/rds/home?region=us-west-2#dbinstances:) and click on the instance you just made and find the **endpoint** under the 'Connect' section. We are going to need the in the following section.


### Django
Open `project/settings.py` and make the following changes:

* Change `DEBUG` to `FALSE` and set `ALLOWED_HOSTS` to the EC2 public IP and `localhost`.

```py
# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = False

ALLOWED_HOSTS = ['{your ip number}','localhost']
```
In the same file change DATABASES as follows:

```py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': '{name_of_database}',
            'USER': '{master_username}',
            'PASSWORD': '{postgresqlPassword}',
            'HOST': '{RDS_endpoint}',
            'PORT': '{db_port}',
    }
}
```
Everything in `{}` is replaced by your actual info including the brackets themselves.

| Placeholder | Explanation |
| :-- | :-- |
| `{name_of_database}` | The name of the rds instance you made earlier |
| `{master_username}` | The master username you chose when setting up the RDS instance. Usually *root* |
| `{RDS endpoint}` | The endpoint you copied in the previous section |
| {db_port} | The database port - usually 5432 for PostgreSQL |


### Configuring Gunicorn
I am following [this tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-18-04#creating-systemd-socket-and-service-files-for-gunicorn) from Digital Ocean for this part

Log on to the EC2 server

```py
ssh -i "filename.pem" ubuntu@x.x.x.x
```
Create a `gunicorn.socket' file in the following folder:
```
sudo vim /etc/systemd/system/gunicorn.socket
```
In this file, paste the followin, save and exit:
```
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
```
Next, create, edit, save and close the following file as follows:
```
sudo vim /etc/systemd/system/gunicorn.service
```
```
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User={user}
Group=www-data
WorkingDirectory=/home/{user}/{projectdir}
ExecStart=/home/{user}/{project}/{env}/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          {myproject}.wsgi:application

[Install]
WantedBy=multi-user.target
```
* `{user}` is the name of the folder you have your project in - in my case it was 'ubuntu'
* `{projectdir}` is where you have your virtual environment folder `env/`
* `{myproject}` is the name of your Django app




...
