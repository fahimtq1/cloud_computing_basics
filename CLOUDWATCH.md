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

## Auto-Scaling and Load Balancing

![auto-scaling (3)](https://user-images.githubusercontent.com/99980305/186672945-8ac8e518-016e-4594-8833-da0bbb05e1b0.png)

### What is Auto-Scaling?



## Logs

See [this documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/QuickStartEC2Instance.html)

CloudWatch Logs agent provide an automated method of sending log data to CloudWatch Logs from Amazon EC2 instances.

These steps will demonstrate how to configure the CloudWatch Logs agent on an EC2 instance that runs Linux:

- `curl https://s3.amazonaws.com//aws-cloudwatch/downloads/latest/awslogs-agent-setup.py -O`- installs log agent
- `sudo python ./awslogs-agent-setup.py --region eu-west-1`- configures the log agent with a log group and log stream
- Event are then logged within the configured log stream dashboard on AWS

### Exporting logs to S3 bucket

See [this documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/S3ExportTasksConsole.html) to change the permissions of an S3 bucket. 

It is sufficient to follow these steps as found in the documentation:

- Choose your bucket in the S3 console
- Navigate to Permissions -> Bucket policy
- In the Bucket Policy Editor, add:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "logs.eu-west-1.amazonaws.com"   # specify correct region
            },
            "Action": "s3:GetBucketAcl",
            "Resource": "arn:aws:s3:::name-of-bucket"
        },
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "logs.eu-west-1.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::name-of-string/random-string/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        }
    ]
}
'''

With the correct permissions applied, the log events can now be exported to the S3 bucket:

- Navigate to the CloudWatch console
- Select Log groups
- Navigate to Actions -> Export data to Amazon S3
- On this page, select the relevant settings (from and to times and the name of the bucket)
- Select Export
