# What is Amazon CloudWatch?

It is an Amazon service that collects monitoring data, from an instance, in the form of metrics and it visualises it using automated dashboards.

![monitoring and alerts](https://user-images.githubusercontent.com/99980305/186459516-f0c0e97d-5aff-40f8-914e-fb7b7bce222b.png)

## Using AWS CloudWatch

- First, select your instance and go to the Actions dropdown menu
- Then, select Monitor and troubleshoot

![image](https://user-images.githubusercontent.com/99980305/186431266-448f0edc-20d6-42f1-8d6d-b7b29f582cf5.png)

- Select Manage CloudWatch alarms and on that page select Create an Alarm
- Select the desired thresholds and ensure that the Alarm notification toggle is on
- You can edit in the Manage CloudWatch dashboard to ensure that the topic of the alarm is your email address
- Now once the alarm is set off, you should receive an email notification

## What is Amazon SNS?

SNS stands for Simple Notification Service- a cloud service for coordinating the delivery of messages from software applications to subscribing endpoints and clients. All of the messages that are published to Amazon SNS are stored across multiple availability zones to prevent data loss.

## What is Amazon SQS?

SQS stands for Simple Queue Service is a message queue service that enables users to manage alerts from Amazon SNS.

## Monitoring and Alert Management

### What is Monitoring?

This is the process of gathering metrics about the operations of an IT environment's hardware and software to ensure everything functions as expected. 

#### What should we Monitor?

Golden Signals:

- Latency- the delay between a client's request and the response of the cloud service provider
- Traffic- the amount of demand (the type of demand depends on the system) that is being placed on a system 
- Errors- the rate of requests that fail
- Saturation- the measure of the utlilisation of the resources within a system

#### Benefits of Monitoring

- Improve the security of an application/network
- Achieving and maintaining ideal application performance
- Optimising service availability
- Simple scaling in the event of cloud activity increases or decreases

### What is Alert Management?

Alerts are informational records used to monitor systems to assess current or upcoming problems. Alert management is the management of these alerts. 

#### What Actions should be taken in case of an Alert?

- Preparing for alerts
- Processing alerts once they occur
- Responding to alerts after they occur
