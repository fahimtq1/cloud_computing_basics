# Auto-Scaling and Load Balancing

![auto-scaling (3)](https://user-images.githubusercontent.com/99980305/186672945-8ac8e518-016e-4594-8833-da0bbb05e1b0.png)

## What is Auto-Scaling?

Auto-scaling is a method of automatically scaling, up or down, the number of computational resources, that are being allocated to your application, based on its needs at any given time. In order to perform auto-scaling in AWS, there are a few pre-requisites:

- AMI
- Load balancer
- Target group
- Launch configuration
- Auto-scaling group

### What is an AMI?

AMI stands for Amazon Machine Image. It is an image, provided by AWS, that provides the information required to launch an instance with a specific configuration. Multiple instances can be launched from a single AMI, if each instance is required to have the same configuration.

### What is a Load Balancer?



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
