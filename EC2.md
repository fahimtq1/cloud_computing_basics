# What is EC2?

EC2 is a AWS service which provides the user an instance of a Virtual Machine on a pay-as-you-go basis. 

## Deploying the app on an EC2 instance

![AWS](https://user-images.githubusercontent.com/99980305/185410653-905abb9c-7d31-4bad-99d5-8d9e256bbcee.png)

### Deploying the Sparta App

- Navigate to EC2 page on AWS account (after logging in and selecting the correct region)
- Launch a new instance
- Select the desired OS
- Choose the instance type
- Configure the instance Public IP to be enabled and the other desired settings
- Add the default storage
- Add a tag: Key=Name and Value=eng122_fahim_app
- Configure the firewall to allow the desired internet ports: 22, 80, 3000 
- You can then set the SSH key with the correct permissions with `chmod 400 "ssh key"`
- Connect to the EC2 instance on your localhost by using the SSH client command in the location of where the .pem ssh key is
- Use the following command to install the monolothic application onto your EC2 instance: `scp  -i ~/.ssh/eng122.pem -r /c/Users/Fahim/AWS_practice/sparta_app  ubuntu@ec2-52-211-140-38.eu-west-1.compute.amazonaws.com:`
- Now install the dependencies for the app: Nginx, Nodejs and pm2
- Configure the reverse proxy
- The app should work!

## Deploying the app using two-tier architecture

### What is two-tier architecture?

It is a type of software architecture in which an application is split into two layers: the presentation layer and a data layer. The presentation layer contains the software content of the application and the data layer contains the database for the application. These two components are stored in different locations, hence the term two-tier. 

In this project, the tiers are contained in each EC2 instance: app and db.

![AWS](https://user-images.githubusercontent.com/99980305/185652521-8c4f0188-0ea1-4090-b503-951f51283c9c.png)

### How to successfully deploy a two-tier application on AWS

- Create the app instance 
- Open port 22, 80 and 3000
- Install the app dependencies: Nginx, Nodejs and pm2
- Configure Nginx as the reverse proxy
- Set the DB_HOST environment variable with the db instance's private IP
- Create the db instance
- Open port 22 and 27017 (with app private IP address)
- Install mongoDB
- Configure the mongod.conf file to allow all IP's
- The app should work!

## Provisioning an EC2 Instance

At the bottom of the configure instance details section, under user details, you can add a provisioning script. Start the script with `#!/bin/bash`. You can then add a provisioning script to automate the configuration of your instance.
