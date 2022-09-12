# AWS Cost Optimization Resources for Startups
Welcome. This reference has been prepared by Startup Solution Architects at AWS to help Startups easily find additional resources that provide specific guidance on various techniques for effective cost optimization.  

We hope this proves useful as you navigate the various options available to you for maximizing the value you can get out of running on AWS. As always, should you have questions on anything, please don't hesitate to contact your local startup team. you can also email ~~<sup-apj@amazon.com>~~

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Contents

- [Useful Tools](#useful-tools)
  - [AWS Budgets](#aws-budgets)
  - [Cost Explorer](#cost-explorer)
  - [Trusted Advisor](#trusted-advisor)
  - [Anomaly detection](#anomaly-detection)
  - [AWS Organizations](#aws-organizations)
  - [Tagging](#tagging)
  - [Pricing Calculator](#pricing-calculator)
  - [Cost & Usage Report](#cost--usage-report)
  - [Well-Architected Framework](#well-architected-framework)
  - [Cost Optimization Workshop](#cost-optimization-workshop)
- [No Effort Options](#no-effort-options)
  - [Reserved Instances](#reserved-instances)
  - [Savings Plans](#savings-plans)
- [AWS Product and Services](#aws-product-and-services)
  - [Data Transfer Out](#data-transfer-out)
    - [Analyze  Data Transfer Costs using Cost Explorer](#analyze--data-transfer-costs-using-cost-explorer)
    - [Use Private IP for Internal Services Communication](#use-private-ip-for-internal-services-communication)
    - [Consider using CloudFront to reduce Data Transfer Out Costs](#consider-using-cloudfront-to-reduce-data-transfer-out-costs)
    - [Use VPC End-Points for S3 and DynamoDB](#use-vpc-end-points-for-s3-and-dynamodb)
      - [Use interface endpoints for other services](#use-interface-endpoints-for-other-services)
    - [Managed services often exempt you from data transfer charges.](#managed-services-often-exempt-you-from-data-transfer-charges)
  - [DynamoDB](#dynamodb)
  - [EBS](#ebs)
  - [EC2](#ec2)
  - [ECS](#ecs)
  - [EKS](#eks)
  - [Graviton](#graviton)
  - [RDS](#rds)
  - [S3](#s3)
  - [Spot](#spot)
  - [CloudWatch](#cloudwatch)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
  
    
<br>
<br>
<br>

# Useful Tools

## AWS Budgets
Get alerted and take action when AWS spend reaches a threshold:

https://aws.amazon.com/aws-cost-management/aws-budgets/

## Cost Explorer
Analyze your costs by region, service, tag, and more:

https://aws.amazon.com/aws-cost-management/aws-cost-explorer/

## Trusted Advisor
Trusted Advisor gives you automated guidance for cost optimization, detecting under-utilized instances and other areas of improvement:

https://aws.amazon.com/premiumsupport/technology/trusted-advisor/


## Anomaly detection

AWS Cost Anomaly Detection is an AWS Cost Management feature that uses machine learning to continuously monitor your cost and usage to detect unusual spends. 

https://docs.aws.amazon.com/cost-management/latest/userguide/manage-ad.html



## AWS Organizations

(More info coming soon)

Use AWS Accounts as an accounting and security boundary, while keeping centralized billing and security controls using AWS Organizations:
https://aws.amazon.com/organizations/

This japanese blog post describes how you can use Control Tower to ease multi account setups
https://aws.amazon.com/jp/blogs/startup/multi-accounts-and-control-tower/



## Tagging
Tagging is a powerful way to organize and allocate costs:

https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html


## Pricing Calculator
Estimate your workload costs ahead of time:

https://calculator.aws/


## Cost & Usage Report
Detailed reports can be scheduled for export as CSV for analysis:

https://aws.amazon.com/aws-cost-management/aws-cost-and-usage-reporting/
## Well-Architected Framework
The Well-Architected Framework gives best practice guidance on Cost Optimization and other topics:

https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html

Inside your AWS Console, you can use the Well-Architected Tool to interactively go through the framework's guidance:
https://aws.amazon.com/well-architected-tool/

Learn more about the Cost Optimization pillar:
https://aws.amazon.com/products/management-tools/partner-solutions/#Resource_and_Cost_Optimization
## Cost Optimization Workshop
To get hands-on with these recommendations, the Activate Next Workshop shows you how to design cost-effective workloads:

https://activate-next.workshop.aws/
# No Effort Options


## Reserved Instances
In return for a commitment of 1 or 3 years, AWS offers discounts on EC2 instance usage of up to 75%:

https://aws.amazon.com/aws-cost-management/aws-cost-optimization/reserved-instances/


## Savings Plans
Benefit from discounts on compute usage, across EC2, Fargate, and Lambda, with Compute Savings Plans:

https://aws.amazon.com/savingsplans


# AWS Product and Services

## Data Transfer Out


### Analyze  Data Transfer Costs using Cost Explorer
This blog post goes into more detail.  
https://aws.amazon.com/blogs/mt/using-aws-cost-explorer-to-analyze-data-transfer-costs/


### Use Private IP for Internal Services Communication
if you deploy ec2 instances in a public subnet, you can choose to have a public IP. If you are communicating between two ec2 instances in the same VPC, make sure to use the private IP so your traffic doesn't leave the AWS network.  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html


### Consider using CloudFront to reduce Data Transfer Out Costs 
Cloudfront is a bit cheaper and has a free tier. As a side bonus you also get performance benefit. https://aws.amazon.com/about-aws/whats-new/2021/11/aws-price-reduction-data-transfers-internet/


### Use VPC End-Points for S3 and DynamoDB
Avoid the anti pattern of inter service communication going out to the internet and coming back in. Use Gateway endpoints! They are free. 
https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html


#### Use interface endpoints for other services
For services other than S3 and DynamoDB you need an interface endpoint.
https://docs.aws.amazon.com/vpc/latest/privatelink/aws-services-privatelink-support.html

https://aws.amazon.com/privatelink/pricing/
Min charge is 0.013 * 730 = $9.49
And then $0.01 / PB

Look at this if your DTO for interservice communication is higher than this.


### Managed services often exempt you from data transfer charges.
It's important to understand what charges you incur for data transfer. It's worth noting that aside from removing undifferentiated heavy lifting, using managed services also exempts you from certain data transfer charges within a region.  

To illustrate this, this blog explores data transfer costs in relation to RDS. 
https://aws.amazon.com/blogs/architecture/exploring-data-transfer-costs-for-aws-managed-databases/



## DynamoDB

## EBS
In general, for almost all workloads, if you are on GP2 you will benefit from moving to GP3.
https://aws.amazon.com/about-aws/whats-new/2020/12/introducing-new-amazon-ebs-general-purpose-volumes-gp3/

Find out how much you stand to save with this EBS GP2 to GP3 Cost savings calculator: https://d1.awsstatic.com/product-marketing/Storage/EBS/gp2_gp3_CostOptimizer.dd5eac2187ef7678f4922fcc3d96982992964ba5.xlsx
  
Here's a blog post describing how you can migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs: https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/

## EC2

Deploy the ready-to-use Instance Scheduler, allowing you to start and stop instances on a schedule to help save costs.
https://aws.amazon.com/solutions/implementations/instance-scheduler/

Consider alternate processors  (often 10% cheaper)
https://aws.amazon.com/ec2/amd/

ARM based (up to 40% better price over performance.)  
https://aws.amazon.com/ec2/graviton/

Use Auto Scaling to use just the compute you need. No need to over-provision for peak load.
https://aws.amazon.com/autoscaling/

With over 400 instance types available, the Instance Explorer can help you find the right one for your needs:
https://aws.amazon.com/ec2/instance-explorer/

## ECS
ECS Fargate is a highly recommended way for startups to deploy their applications as it  removes undifferentiated heavy lifting of managing instances. This blog post is a cost optimization checklist to help you optimize on cost.
https://aws.amazon.com/blogs/containers/cost-optimization-checklist-for-ecs-fargate/


To further optimize you can use Fargate spot, but you need to architect for handling the interruptions if the computer resources get reclaimed.  
This japanese blog post describes how to do that.
https://aws.amazon.com/blogs/containers/graceful-shutdowns-with-ecs/  
[JP version]
https://aws.amazon.com/jp/blogs/news/graceful-shutdowns-with-ecs/


Container insights is super helpful for gaining visibility into what your containers are doing. This blog introduces the product and what you can do with it
https://aws.amazon.com/blogs/mt/introducing-container-insights-for-amazon-ecs/


For a full list of Amazon ECS Container Insights metrics, see Amazon ECS Container Insights Metrics https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-ECS.html



## EKS

There are various tools and plugins you should know about to help you optimize your EKS usage.

AWS Node Terimination handler helps you gracefully handle EC2 instance shutdown within Kubernetes. https://github.com/aws/aws-node-termination-handler
This is important for auto scaling and leveraging spot.

[Karpenter](https://karpenter.sh/) is a high performance auto scaling solution. Use it with Spot to reap savings. https://aws.amazon.com/blogs/containers/using-amazon-ec2-spot-instances-with-karpenter/

This blog post describes recommended tips for cost optimization in AWS.
https://aws.amazon.com/blogs/containers/cost-optimization-for-kubernetes-on-aws/

These plugins will help give visibility into your costs
https://github.com/hjacobs/kube-resource-report  



another helpful tool for cost visibility is [Kubecost](https://github.com/kubecost/kubectl-cost). Kubecost enables users to view costs broken down by Kubernetes resources including pods, nodes, namespaces, labels, and more. 
https://aws.amazon.com/blogs/containers/aws-and-kubecost-collaborate-to-deliver-cost-monitoring-for-eks-customers/

use it in conjunction with 
https://github.com/kubecost/cost-model  


AWS also has cluster level cost allocation tagging.
https://aws.amazon.com/about-aws/whats-new/2022/08/amazon-eks-cluster-level-cost-allocation-tagging/  

[JP version]
https://aws.amazon.com/jp/about-aws/whats-new/2022/08/amazon-eks-cluster-level-cost-allocation-tagging/


This plugin is used to scale in and out the deployments based on time of day. This can result in significant cost-savings when there are many deployments that only need to be available during business hours.
https://github.com/hjacobs/kube-downscaler




## Graviton

github graviton link


## RDS

Understanding how you are using your RDS instances is key to RDS optimization. A highly effective tool to aid you in this is `Performance Insights`  
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PerfInsights.html


These links provide practical hands on workshops to show you how to leverage Performance Insights to get the most out of your RDS instances

Performance Monitoring Workshop for RDS PostgreSQL and Aurora PostgreSQL - https://catalog.us-east-1.prod.workshops.aws/workshops/31babd91-aa9a-4415-8ebf-ce0a6556a216/en-US


RDS MySQL Performance Insights Lab - https://catalog.us-east-1.prod.workshops.aws/workshops/0135d1da-9f07-470c-9845-44ead3c78212/en-US/lab8

This workshop is part of a new program we run with startups to help developers be better practioners of relational databases. If you are interested in running this for your startup, please get in touch with us.  
DB4Dev workshop - https://catalog.workshops.aws/db4devs/en-US



## S3

This workshop walks you through S3 Cost optimization tips: https://catalog.us-east-1.prod.workshops.aws/workshops/f238037c-8f0b-446e-9c15-ebcc4908901a/en-US/002-services/002-storage/003-s3


This blog post will outline how you can optimize for both predictable and dynamic access patterns - https://aws.amazon.com/blogs/storage/amazon-s3-cost-optimization-for-predictable-and-dynamic-access-patterns/

Use the S3 Storage Classes to optimize your storage costs:
https://aws.amazon.com/s3/storage-classes

## Spot
AWS Spot Instances are an amazing option allowing you to take advantage of spare capacity in AWS datacenters to receive up to 90% discounts on your instances. Spot is available to use with EC2 instances directly and also with ECS and EKS. You can learn more here 
[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)

The catch is if AWS needs that spare capacity, you will receive a 2 min warning before your instance is reclaimed. 

To learn how you might take advantage of this, you can try yourself in this workshop:
https://ec2spotworkshops.com/

Learn more about Spot: https://aws.amazon.com/ec2/spot


## CloudWatch
Custom Metrics can be pushed to CloudWatch from your application:
https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html

Viewing standard and custom metrics in a CloudWatch dashboard:
https://catalog.workshops.aws/observability/en-US/metrics/viewmetrics
