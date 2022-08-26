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

A load balancer is a tool used in auto-scaling to distribute incoming application traffic to registered targets (e.g. EC2 instances). AWS has different [types of load balancers](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/load-balancer-types.html):

- Application Load Balancer
- Network Load Balancer
- Classic Load Balancer
- Gateway Load Balancer

### What is a Target Group?

A target group specifies, to a load balancer, the directions for incoming traffic. The target group has target types, which determines the type of target that can be specified when registering targets with this group.

### What is Launch Configuration?

It is a template that an EC2 auto-scaling group uses to launch EC2 instances. The creation of a launch configuration includes the ID of the AMI. 

### What is an Auto-Scaling Group?

This contains a set of EC2 instances that are present for the purpose of automatic scaling and management. 

## How to Perform Auto-Scaling?

To create each of the following, their respective pages can be found on the left hand menu of the EC2 console page:

- Create AMI of selected instance- Actions -> Image and templates -> Create image
- Create Load Balancer- select the necessary load balancer type, other settings and desired EC2 instance
- Create Target Group- select the necessary target type, protocol, default VPC, default advanced health check settings and select the relevant instance
- Create Launch Configuration- select the AMI and configure the EC2 template for the auto-scaling group, choose the relevant key pair that is the same key as for the instance
- Create Auto-Scaling Group- create a new launch template with the AMI and relevant settings, attach to created load balancer, configure the group size and select a [scaling policy](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-simple-step.html)
- Attach the Load balancer, Target group and Launch configuration to the auto-scaling group in the auto-scaling group settings
