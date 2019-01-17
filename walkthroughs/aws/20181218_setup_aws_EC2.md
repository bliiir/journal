*Journal*
Rasmus Groth
*20181207, Utterslev, Copenhagen, Denmark*

# Setup AWS EC2

Follow [this](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html) tutorial:

### Create key file
Create the .pem file [here](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#KeyPairs:)

### Download key file
Download the .pem file and put it in the ```/Users/username/.ssh``` folder.

### Set permissions
Change the file permissions so only you can read it: ```chmod 400 filename.pem```


### Create an EC2 Instance


## Connect to the server
Connect to the server from the terminal: ```ssh -i ~/.ssh/filename.pem username@ip-number```


## Install

Update the installed applications
```
sudo apt-get update
sudo apt-get dist-upgrade #
```
Or
```
sudo apt full-upgrade
```

Install pip
```
sudo apt-get install python3-pip
```
Initialize git
```
git init
git remote add origin https://github.com/bliiir/ccat.git
git pull origin master
```

Install requirements
```
pip install -r requirements.txt
```

See other notes for how to set up EC2 and RDS
