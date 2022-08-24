# Cloud Computing

Please see this [link](https://github.com/fahimtq1/virtualisation_basics/blob/main/PROJECT.md) for a description on the application that will be deployed in this project.

## Definition 

Cloud computing is the delivery of on-demand computing services over the internet. There are two cloud computing models: the deployment model and the services model. There are three main cloud computing service providers: Amazon Web Services (AWS), Microsoft Azure and Google Cloud Platform (GCP). 

## Benefits

- Scalability- easier, faster and cheaper provisions for scaling up and down 
- Server storage- service providers manage and maintain servers
- Data security- better security in the cloud and user can avoid monitoring security protocols
- Maintenance- computing systems are maintained by the service provider, therefore reducing the costs of the user

## Deployment Model 

- Public Cloud

The cloud infrastructure is available to the public over the internet and is owned by a service provider.

- Private Cloud

The cloud infrastructure is operated and owned by a single organisation.

- Hybrid Cloud

The cloud infrastructure is a mixture of both the public cloud and the private cloud. 

## Service Model 

- Infrastructe as a Service (IaaS)

This service provides users access to basic computing infrastructure (servers and storage), so virtualisation can occur. The rest of the components are managed by the user.

- Platform as a Service (PaaS)

The service provider provides the necessary components for a cloud-based development environment, so that developers can conduct the developing, testing and managing of an application. 

- Software as a Service (SaaS)

In this case, the service provider handles all the components of a complete cloud computing environment, including the hosting and managing of a software application.

## Deploying the app on an EC2 instance

![AWS](https://user-images.githubusercontent.com/99980305/185410653-905abb9c-7d31-4bad-99d5-8d9e256bbcee.png)

### What is AWS?

AWS is a cloud computing platform. It provides: Infrastructure as a Service (IaaS), Platform as a Service (PaaS) and Software as a Service (SaaS). AWS is mainly used in DevOps practices as IaaS. 

### What is EC2?

EC2 is the AWS version of a Virtual Machine. 

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

## Disaster Recovery Plan (DR)

These plans are made in case of any unexpected disaster, so that there is a backup available for a web application. There are multiple ways of doing this:

- Multiple Availability Zones

On AWS, within a region, there are multiple zones (data centres) that an application can be deployed.

- Multiple Regions

There are multiple regions in which an application can be deployed. This DR is more expensive than the multiple availability zones method. 

- Multiple Cloud Deployment

This is the most expensive method, as it has different cloud computing service providers as backups.

- Hybrid Cloud

This is a mixture between a public cloud and private cloud model. 
