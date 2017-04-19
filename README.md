# Udacity LinuxServer
The project is deployed on AWS EC2 Intance.

[Project example](http://52.207.154.219/restaurant/)

## Login to EC2 Instance
1. Download instance private key.
2. Locate private key `cd /user/downloads/key`
3. `chown 400 yourKeyPair.pem`
4. `ssh -i .ssh/yourkeyPair.pem ubuntu@Ip-address`

## Create a new User 
Create a new user named grader and give sudo permission  
`sudo adduser grader`  
Password:`grader`  
verify:`grader`  
`sudo visudo`  

We add the following line after the comment line, “User privilege specification”:  
`grader ALL=(ALL:ALL) ALL`

## Update packages
`sudo apt-get update`  
`sudo apt-get upgrate`

#### install python environment
`sudo apt-get install python-psycopg2`  
`sudo apt-get install python-flask python-sqlalchemy`  
`sudo apt-get install python-pip`

### Configure timezone
update EC2 instance timezone to UTC:  
`sudo dpkg-reconfigure tzdata`  
and change it to   
`sudo apt-get install ntp`

### Install Apache and mod_wsgi
`sudo apt-get install apache2`  
`sudo apt-get install libapache2-mod-wsgi`

## Generate KeyPairs
While you still on login as unbutu generate the key and save the key  
`ssh-keygen`  
Enter file in which to save the key (/home/grader/.ssh/id_rsa): /home/grader/.ssh/grader  
/home/grader/.ssh/grader


## Add grader user to sudo group
`sudo adduser grader sudo`   
`Switch to grader user`  
`sudo su grader`  

## Create the SSH directory
`mkdir .ssh`   
`chmod 700 .ssh`  
`touch .ssh/authorized_keys`  
`chmod 600 .ssh/authorized_keys`  
## edit the authorized_keys 
while login as grader copy the genereated key that you created on previews steps.  
` nano .ssh/authorized_keys`  
Paste the key you created and save it.

## Clone Item Catalog
`cd /var/www/`  
`sudo git clone https://github.com/leo831/Restaurant.git`  


## Create WSGI Application
`sudo touch application.wsgi` 

`#!/usr/bin/python`  
`import sys`  
`import logging`  
`logging.basicConfig(stream=sys.stderr)`  
`sys.path.insert(0, "/var/www/Restaurant/")`  
`from project  import app  as application`  
`application.secret_key = 'super_secret_key'`  

#### Restart apache
`sudo service apache restart ` 

## PostgreSQL
`sudo apt-get install postgresql postgresql-contrib`  
`sudo -i -u postgres`  
`createuser --interactive`  
`createdb catalog`  
`psql`  
`\password catalog`

## Git
`sudo apt-get install git-all`  
