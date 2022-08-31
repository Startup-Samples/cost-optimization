# AWS Cost Optimization Resources for Startups
Welcome. This reference has been prepared by Solutions Architects at AWS to help Startups easily find additional resources that provide specific guidance on various techniques for effective cost optimization.  

We hope this proves useful as you navigate the various options available to you for maximizing the value you can get out of running on AWS. As always, should you have questions on anything, please don't hesitate to contact your local startup team. you can also email <sup-apj@amazon.com>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Contents

- [Useful Tools](#useful-tools)
  - [AWS Budgets](#aws-budgets)
  - [Cost Explorer](#cost-explorer)
  - [Trusted Advisor](#trusted-advisor)
  - [Anomaly detection?](#anomaly-detection)
  - [AWS Organizations](#aws-organizations)
  - [Tagging](#tagging)
- [No Effort Options](#no-effort-options)
  - [Reserved Instances](#reserved-instances)
  - [Savings Plans](#savings-plans)
- [Services](#services)
  - [DynamoDB](#dynamodb)
  - [EBS](#ebs)
  - [EC2](#ec2)
  - [ECS](#ecs)
  - [EKS](#eks)
  - [RDS](#rds)
  - [S3](#s3)
  - [Spot](#spot)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
  
    
<br>
<br>
<br>

# Useful Tools

## AWS Budgets

## Cost Explorer

## Trusted Advisor

## Anomaly detection?

## AWS Organizations

Account setup.  
Control tower?



## Tagging







# No Effort Options


## Reserved Instances

## Savings Plans




# Services

## DynamoDB

## EBS
In general, for almost all workloads, if you are on GP2 you will benefit from moving to GP3.
https://aws.amazon.com/about-aws/whats-new/2020/12/introducing-new-amazon-ebs-general-purpose-volumes-gp3/

Find out how much you stand to save with this EBS GP2 to GP3 Cost savings calculator: https://d1.awsstatic.com/product-marketing/Storage/EBS/gp2_gp3_CostOptimizer.dd5eac2187ef7678f4922fcc3d96982992964ba5.xlsx
  
Here's a blog post describing how you can migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs: https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/

## EC2


## ECS
ECS Fargate is a highly recommended way for startups to deploy their applications as it  removes undifferentiated heavy lifting of managing instances. This blog post is a cost optimization checklist to help you optimize on cost.
https://aws.amazon.com/blogs/containers/cost-optimization-checklist-for-ecs-fargate/


## EKS

There are various tools and plugins you should know about to help you optimize your EKS usage.

AWS Node Terimination handler helps you gracefully handle EC2 instance shutdown within Kubernetes. https://github.com/aws/aws-node-termination-handler
This is important for auto scaling and leveraging spot.

[Karpenter](https://karpenter.sh/) is a high performance auto scaling solution. Use it with Spot to reap savings. https://aws.amazon.com/blogs/containers/using-amazon-ec2-spot-instances-with-karpenter/

This blog post describes recommended tips for cost optimization in AWS.
https://aws.amazon.com/blogs/containers/cost-optimization-for-kubernetes-on-aws/

These plugins will help give visibility into your costs
https://github.com/hjacobs/kube-resource-report  
https://github.com/kubecost/cost-model  

This plugin is used to scale in and out the deployments based on time of day. This can result in significant cost-savings when there are many deployments that only need to be available during business hours.
https://github.com/hjacobs/kube-downscaler



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


## Spot
AWS Spot Instances are an amazing option allowing you to take advantage of spare capacity in AWS datacenters to receive up to 90% discounts on your instances. Spot is available to use with EC2 instances directly and also with ECS and EKS. You can learn more here 
[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)

The catch is if AWS needs that spare capacity, you will receive a 2 min warning before your instance is reclaimed. 

To learn how you might take advantage of this, you can try yourself in this workshop:
https://ec2spotworkshops.com/