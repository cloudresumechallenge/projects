---
title: "Traditional Web Hosting on AWS"
---

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| Traditional Web Hosting on AWS | AWS | Understand how to run your application in a traditional web architecture | [@tonytalkstech](https://twitter.com/tonytalkstech) and [@loujaybee](https://twitter.com/loujaybee) |

### Intro

The Cloud Resume Challenge uses many serverless technologies, such as Lambda and S3. This focus on serverless allows the challenger to focus on the application and delivery details without having to be bogged down with operational concerns, which is great! Delivering an application to the cloud is one of the most important skills to learn.

Many companies utilize a number of traditional technologies within AWS to deliver applications, most of which are less managed than the serverless technologies. These include [Elastic Cloud Compute (EC2)](https://docs.aws.amazon.com/ec2/index.html), which provides virtual machines in AWS, and [Virtual Private Cloud (VPC)](https://docs.aws.amazon.com/vpc/index.html), which provides virtual networking constructs in AWS.

This challenge is focused on adapting the Cloud Resume Challenge to provide a deeper dive into the traditional technologies, especially focused on the networking stacks within AWS.

### Helpful reading

* AWS has a wonderful [whitepaper](https://docs.aws.amazon.com/whitepapers/latest/web-application-hosting-best-practices/welcome.html) that has a full implementation of this architecture.
* AWS VPCs are notoriously difficult to understand, so it's helpful to read as much as possible. [AWS's VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) goes over as much detail as you could ever want. I would recommend focusing on [Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-subnets.html), [Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html), [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html), and [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html).

### Challenge steps

1. **Create an EC2 instance** based on an [Amazon Linux 2](https://aws.amazon.com/amazon-linux-2/) AMI from AWS. Use the default networking components that are given in your AWS account. Make the instance publicly accessible to the internet. Be aware that a _running_ EC2 instance costs money. If you aren't actively working on this challenge, remember to **stop** the instance. The lowest-cost EC2 instance is currently the `t4g.nano`, which costs ~$3/month. EC2 instances use [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) as host-based firewalls. Make sure your EC2 instance only allows HTTP (and, optionally, HTTPS) traffic from the public internet.
1. **Install a web server** [using the `user_data` property](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html) on your EC2 instance, invoke `yum` to download `httpd` (Apache). Make your EC2 instance return a simple HTML file when you access it from the public internet over HTTP (and, optionally, HTTPS).
1. **Configure high availability** by using duplicate EC2 instances in multiple Availability Zones in the same Region. Route traffic from the internet across each of the EC2 instances by using an [Application Load Balancer](https://aws.amazon.com/elasticloadbalancing/application-load-balancer/). **Application Load Balancers aren't cheap.** They currently are ~$28/month in the major US Regions.
1. **Setup Auto Scaling** instead of manually creating new EC2 instances and adding each to the load balancer. Use [EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html). You will always want at least two instances. For now, use CPU Utilization as the scaling metric until a more appropriate metric is available. Be sure to [attach your Application Load Balancer to the Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/attach-load-balancer-asg.html).
1. **Deploy your own AWS networking components**. You will be creating a [VPC](https://aws.amazon.com/vpc/) to logically separate all deployed AWS resources. Within the VPC, you'll create multiple [Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html). Create one for each Availability Zone in the Region. With a new VPC, you must re-create any Security Groups you previously created. Now that you have your own network, re-create your EC2 instances within the new Subnets. Once the old default network components are no longer in use, delete them.
1. **Secure your networking** by moving your EC2 instances to a private subnet in your VPC. A private subnet is defined as one that does not have a NAT Gateway in it, so it cannot reach the public internet. Lock down your EC2 instance's Security Groups to only allow traffic from the Application Load Balancer.
1. **Allow your web server to communicate with the internet**. This will require you to update your network stack to create public subnets with NAT Gateways and route table rules to allow traffic from your private subnets to the public subnets.
1. **Migrate your resume** to your EC2 web server instances. Remember to secure the traffic from the EC2 instances to the API Gateway by utilizing Security Group rules.
1. **Update DNS** to point to your Application Load Balancer instead of your CloudFront distribution.
1. **Write up a blog post** about what you learned! Include a diagram, specifically focusing on the networking details and security. Be sure to reflect on the particular challenges, especially with adapting the Cloud Resume Challenge to this traditional challenge.

### Extra credit

1. **Setup infrastructure-as-code (IaC)** instead of pointing and clicking within the AWS Console to create your AWS resources. Define your resources within a Terraform file. Get familiar with `terraform plan` and `terraform apply`. Why Terraform? To learn an IaC tool that can be used across multiple cloud providers.
1. **Create a deployment pipeline for multiple environments**, such as a development environment and production environment. Deploy your Terraform resources using the same code (with different names and variables). Separate these environments by using two separate VPCs. Separate the pipelines by deploying to the production environment from the default branch (typically `main`), while every other branch deploys to the development environment.
1. **Replace your Lambda function** with an EC2 instances hosting the API. This should involve installing Apache (`httpd`) and Python on the new EC2 instances. Place these EC2 instances in a separate subnet than the web server instances and secure the traffic using Security Groups. This should allow you to remove the public subnets, as well.
