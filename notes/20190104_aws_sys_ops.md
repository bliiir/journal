*Journal*
Rasmus Groth
*20190104, Utterslev, Copenhagen, Denmark*

# System operations

## Setting up server recovery

### EC2

I used [AWS cloudwatch recovery alarms](https://aws.amazon.com/premiumsupport/knowledge-center/automatic-recovery-ec2-cloudwatch/) to set up automatic reboot if a system check fails two checks two minutes in a row.

Wether this is the best setup remains to be seen, but I will consider it resolved for now.

### RDS
From [this](https://serverfault.com/questions/435323/amazon-aws-rds#435509) Stack Overflow answer:

> The RDS service automatically manages failing machines and moves your data to a new machine with the same name so it looks like nothing happened. This is part of the service you're paying for when you use AWS RDS instead of just installing your database of choice inside a regular EC2 instance.

That means that I have both the database and the system server covered for crashes. I use Git version control on the main server and automatic 10 day backups on the RDS instance.

I will consider the matter resolved.
