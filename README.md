# AWS-AUTOSCALING - Security Group 
This lab experience involves Amazon Web Services (AWS). I will use the AWS Management Console


Groups

Your EC2 instances are organized into groups so that they can be treated as a logical unit for the purposes of scaling and management. When you create a group, you can specify its minimum, maximum, and desired number of EC2 instances. 

### Launch configurations

Your group uses a launch configuration as a template for its EC2 instances. When you create a launch configuration, you can specify information such as the AMI ID, instance type, key pair, security groups, and block device mapping for your instances. 

### Launch template

A launch template is similar to a launch configuration, in that it specifies instance configuration information. ... However, defining a launch template instead of a launch configuration allows you to have multiple versions of a template. With versioning, you can create a subset of the full set of parameters and then reuse it to create other templates or template versions.

Auto Scaling groups are commonly paired with load balancers that evenly distribute requests across all the instances in the group. In this Lab, you will create a load balancer before creating an Auto Scaling group so that the Auto Scaling group can be configured to work with the load balancer at creation time.

A Launch Template is a template that an Auto Scaling group uses to launch Amazon EC2 instances.  The Launch Template essentially contains the blueprint or DNA for the exact type of instance that should be launched. Hence, when auto-scaling, each instance is guaranteed to be just like the last one. It's repeatable, scalable, and reliable.

I created a Security Group to configure a rule allowing SSH traffic, enter the following values:

Type:  SSH  
Source:   Anywhere-IPv4
Description: SSH

And to configure a rule allowing HTTP traffic, enter the following values:

Type: Enter HTTP and select HTTP
Source: Select Anywhere-IPv4
Description: Enter HTTP
In a non-lab environment, you are likely to be required to have a much more restrictive Source. For example, you may be required to specify a corporate IP range to reduce the likelihood of unauthorized access.


![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/2c895500-c150-4d81-8fed-6f875d29db16)


![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/d904b6d6-218e-49ef-9d0d-3f10e027995c)



I have created a security group that I can specify in the launch template you are about to create.
![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/49719a60-778c-4f4c-bf74-8bb382cdabf8)



In the left-hand menu, under Instances, I click Launch Templates:


![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/f43a74dc-7ca5-45e8-88d6-208f23679c9b)

You will use the key pair to access EC2 instances launched with this configuration later in the lab.

![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/2515125b-70ae-41d7-9597-373e7f165bcb)
In situations where you don't need SSH, you don't have to configure a key pair, this is often preferred in terms of security.

Under the Network Settings section, click the Security groups drop-down and select webserver-cluster:

This is the security group I created earlier.
![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/837b010b-ab1f-4d89-9efe-6355ea731a53)

 Take a look at the Storage (volumes) section.

This part of the form allows you to add or increment the size of any EBS volume attached to each EC2 instance started by the Auto Scaling group. Leave the defaults and do not add any EBS volumes.

Typically large EBS volumes are only needed if your software requires storage space to process the application data. Many applications store raw or processed data with Amazon S3, Redshift, DynamoDB, or another storage/database service provided by Amazon. When that is the use case, large EBS volumes are usually not required. This lab environment does not need extra disk space.


Scroll down to the bottom and click Advanced details:

More configuration options will appear.

I scrolled down to the Detailed CloudWatch monitoring option, and select Enable:

![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/f9ce3a0a-ed5f-475e-88a1-5858d091dbab)

By default, CloudWatch monitors EC2 instances approximately every 5 minutes. Detailed monitoring enables monitoring more often (each minute). 

Note: Enabling detailed monitoring incurs an extra cost.

User data text-box at the bottom of the page, enter the following script:


![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/2fcd5ac8-537c-4acd-bb2d-33280e512da7)


This bash script installs PHP, an Apache webserver (httpd), and a tool for stress testing called Stress.

Warning: The EC2 instances will never reach 100% CPU Utilization due to the limitations of the burstable credit. They should reach an usage of about 80%.

![image](https://github.com/kalejcamto/AWS-AUTOSCALING/assets/101201140/29dda73d-9d70-4641-9b03-72bddbd09074)


































