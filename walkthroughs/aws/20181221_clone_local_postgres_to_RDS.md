*Journal*  
Rasmus Groth  
*20181221, Utterslev, Copenhagen, Denmark*

# How to clone a local Postgres database to a remote AWS RDS via an EC2 instance

Today we are going to dump the local database to a file and transfer it to an AWS EC2 instance and then restore it into the RDS instance. This might sound cumbersome, but using the ability to connect within the AWS security groups makes it at least half managable. restoring the dump remotely.

### Create EC2 instance
First we need an EC2 instance. Go to the [aws dashboard](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#LaunchInstanceWizard:) and launch an RDS instance with Postgres installed.

### Create an RDS instance
Got to the [RDS dashboard](https://us-west-2.console.aws.amazon.com/rds/home?region=us-west-2) and create a new instance. Make sure Public accessibility to [yes].

### Configure your VPC
Amazon assigns all services to their [Virtual Private Clouds](https://us-west-2.console.aws.amazon.com/vpc/home?region=us-west-2). The VPC you are using for the RDS has to have DNS resolution and hostnames enabled and have **two** subnets each in separate availability zones for this to work. I struggled **a.lot** with this.

### Setup DNS for the VPC
When you try to connect to the RDS database, you will fail unless your VPC and security groups are properly configured

### Get keys
If you haven't already, create a ```.pem``` file with [keys](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#KeyPairs:sort=keyName) and store it in your ```~/.ssh/``` folder.

### Log in to your EC2 instance
Get the default username for your AMI instance from [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) or [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html) and the ip from the EC2 dashboard
```
ssh -i ~/.ssh/ccat.pem my_AMI_username@xx.xxx.xxx.xxx
```

### Install Postgres
Then we need to [install pgsl](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-14-04) on the EC2 instance to allow communication with the RDS remote
```
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
```

### Local dump
Ok, back to your local computer - we need to make a local dump of the database we want to run on the RDS instance before we move forward.
```
pg_dump dbname=my_pg_db -f my_db_dump.sql -U postgres
```
Or as a compressed ```.dump``` file
```
pg_dump -Fc -o dbname=my_pg_db > my_db_dump.dump -U postgres
```
(The -Fc means custom dump format)

### Copy dump to EC2
Secure copy database dump file to remote EC2 server
```
scp -i ~/.ssh/mykeys.pem /?/my_db_dump.sql my_AMI_username@xx.xxx.xxx.xxx:~/my_db_dump.sql
```

## Restore to Amazon RDS
```
psql \
   -f my_db_dump.sql \
   --host=not_the_real_host.cdvhxtrsfceo.us-west-2.rds.amazonaws.com \
   --port=5432 \
   --username=not_my_real_un \
   --password \
   --dbname=my_pg_db
```

### Check that it worked
Connect to the RDS instance:
```
psql \
    --host=not_the_real_host.cdvhxtrsfceo.us-west-2.rds.amazonaws.co \
    --port=5432 \
    --username=not_my_real_un \
    --password \
    --dbname=my_pg_db \
```
And use the command ```\d``` to check that the tables are there and try a select * from one of them to ensure they have the content
