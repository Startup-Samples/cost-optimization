# AWS Cost Optimization Resources for Startups
Welcome. This reference has been prepared by Startup Solution Architects at AWS to help Startups easily find additional resources that provide specific guidance on various techniques for effective cost optimization.  

We hope this proves useful as you navigate the various options available to you for maximizing the value you can get out of running on AWS. As always, should you have questions on anything, please don't hesitate to contact your local startup team. If you aren't already in contact with them, simply visit https://aws.amazon.com/startups/ and click on the `Get In Touch` button.

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
  - [Cloudwatch](#cloudwatch)
  - [Data Transfer Out](#data-transfer-out)
  - [DynamoDB](#dynamodb)
    - [Application auto scaling](#application-auto-scaling)
    - [Storage-IA table class](#storage-ia-table-class)
    - [general guidance](#general-guidance)
  - [EBS](#ebs)
  - [EC2](#ec2)
  - [ECS](#ecs)
  - [EKS](#eks)
  - [Graviton](#graviton)
  - [Lambda](#lambda)
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

make sure to checkout the optimization recommendations  
https://aws.amazon.com/blogs/aws-cloud-financial-management/launch-resource-optimization-recommendations/


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


<br>
<br>

# No Effort Options


## Reserved Instances
In return for a commitment of 1 or 3 years, AWS offers discounts on EC2 instance usage of up to 75%:

https://aws.amazon.com/aws-cost-management/aws-cost-optimization/reserved-instances/


## Savings Plans
Benefit from discounts on compute usage, across EC2, Fargate, and Lambda, with Compute Savings Plans:

https://aws.amazon.com/savingsplans


<br>
<br>


# AWS Product and Services

## Cloudwatch
Make sure you have set retention policies on logs  
https://aws.amazon.com/blogs/infrastructure-and-automation/reduce-log-storage-costs-by-automating-retention-settings-in-amazon-cloudwatch/

if you are using [Custom Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html) consider switching to Embedded Metric Format (EMF).  
https://aws.amazon.com/about-aws/whats-new/2019/11/amazon-cloudwatch-launches-embedded-metric-format/
The main difference is that EMF doesn't incur a charge when submitting a custom metric.

<br>
<br>

## Data Transfer Out

- Analyze Data Transfer Costs using Cost Explorer
This blog post goes into more detail.  
https://aws.amazon.com/blogs/mt/using-aws-cost-explorer-to-analyze-data-transfer-costs/


- Use Private IP for Internal Services Communication  
if you deploy ec2 instances in a public subnet, you can choose to have a public IP. If you are communicating between two ec2 instances in the same VPC, make sure to use the private IP so your traffic doesn't leave the AWS network.  
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html


- Use VPC End-Points for S3 and DynamoDB  
Avoid the anti pattern of inter service communication going out to the internet and coming back in. Use Gateway endpoints! They are free. 
https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html


  - Use interface endpoints for other services.  
    For services other than S3 and DynamoDB you need an interface endpoint.
    https://docs.aws.amazon.com/vpc/latest/privatelink/aws-services-privatelink-support.html  
    https://aws.amazon.com/privatelink/pricing/  
    Min charge is 0.013 * 730 = $9.49
    And then $0.01 / PB
      
    Look at this if your DTO for interservice communication is higher than this.

- Consider using CloudFront to reduce Data Transfer Out Costs  
Cloudfront is a bit cheaper and has a free tier. As a side bonus you also get performance benefit. https://aws.amazon.com/about-aws/whats-new/2021/11/aws-price-reduction-data-transfers-internet/



- Managed services often exempt you from data transfer charges.  
It's important to understand what charges you incur for data transfer. It's worth noting that aside from removing undifferentiated heavy lifting, using managed services also exempts you from certain data transfer charges within a region.  
To illustrate this, this blog explores data transfer costs in relation to RDS. 
https://aws.amazon.com/blogs/architecture/exploring-data-transfer-costs-for-aws-managed-databases/

<br>
<br>

## DynamoDB


- writes are 5x more expensive than reads. e.g on-demand: https://aws.amazon.com/dynamodb/pricing/on-demand/
- attribute names contribute to storage. Use shorter names if storage costs are an issue
- rethink if attribute values need to be in dynamo. a good example is storing image data. rather than storing in Dynamodb, does it make more sense to store it in S3 and store just the key in Dynamo
- breaking up an item into multiple items may make sense depending on the access pattern.
- Use TTL for data that loses significance after a period of time:  https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html


### Application auto scaling
Use Application auto scaling to adjust capacity dynamically to traffic.  
Keep in mind, DynamoDB read/write capacity is automatically adjusted according to an application traffic.  
There is, however, a limit on the number of times you can adjust the Read/Write capacity / day. This means you can't reduce write capacity if the read capacity is reduced by more than the allowed number of times.  
Therefore in this case, you might pay more because of the unnecessary high write capacity.

A strategy here is to adjust only the write capacity on the schedule while fixing the read capacity.  
In this way you can reduce DynamoDB costs incurred by the write capacity, which we already know is 5x more expensive than read capacity.

https://aws.amazon.com/blogs/database/amazon-dynamodb-auto-scaling-performance-and-cost-optimization-at-any-scale/

documentation: https://docs.aws.amazon.com/autoscaling/application/userguide/services-that-can-integrate-dynamodb.html

If DynamoDB storage cost exceeds 50 percent of the cost of throughput (reads and writes) consistently, then the DynamoDB Standard-IA table class is the most economical choice for you.

### Storage-IA table class

If DynamoDB storage cost exceeds 50 percent of the cost of throughput (reads and writes) consistently, then the DynamoDB Standard-IA table class is the most economical choice for you.
Good examples of potential candidates are tables that store infrequently accessed data, such as application logs, old social media posts, e-commerce order history, and past gaming achievements.    
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithTables.tableclasses.html  
https://aws.amazon.com/dynamodb/pricing/on-demand/


### general guidance
How do I optimize costs with Amazon DynamoDB?
https://aws.amazon.com/premiumsupport/knowledge-center/dynamodb-optimize-costs/

Safely reduce the cost of your unused Amazon DynamoDB tables using on-demand mode
https://aws.amazon.com/ko/blogs/database/safely-reduce-the-cost-of-your-unused-amazon-dynamodb-tables-using-on-demand-mode/  


<br>
<br>


## EBS
In general, for almost all workloads, if you are on GP2 you will benefit from moving to GP3.
https://aws.amazon.com/about-aws/whats-new/2020/12/introducing-new-amazon-ebs-general-purpose-volumes-gp3/

Find out how much you stand to save with this EBS GP2 to GP3 Cost savings calculator: https://d1.awsstatic.com/product-marketing/Storage/EBS/gp2_gp3_CostOptimizer.dd5eac2187ef7678f4922fcc3d96982992964ba5.xlsx
  
Here's a blog post describing how you can migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs: https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/

<br>
<br>


## EC2

Turn off instances you are not using.

Deploy the ready-to-use Instance Scheduler, allowing you to start and stop instances on a schedule to help save costs.
https://aws.amazon.com/solutions/implementations/instance-scheduler/

Make sure to rightsize your instances. You can manually eyeball from cloudwatch or use helpful tools like Compute Optimizer.  
https://aws.amazon.com/blogs/aws/aws-compute-optimizer-your-customized-resource-optimization-service/  
https://aws.amazon.com/blogs/compute/optimizing-ec2-workloads-with-amazon-cloudwatch/  
https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-right-sizing/identifying-opportunities-to-right-size.html  
https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-right-sizing/tips-for-right-sizing-your-workloads.html



Consider alternate processors  (often 10% cheaper)
https://aws.amazon.com/ec2/amd/

ARM based (up to 40% better price over performance.)  
https://aws.amazon.com/ec2/graviton/

(more on [graviton below](#graviton))

Learn how to leverage [Spot in the section below](#spot)

Use Auto Scaling to use just the compute you need. No need to over-provision for peak load.
https://aws.amazon.com/autoscaling/

With over 400 instance types available, the Instance Explorer can help you find the right one for your needs:
https://aws.amazon.com/ec2/instance-explorer/


Learn how AWS Cost Explorer Rightsizing Recommendations Integrates with AWS Compute Optimizer  
https://aws.amazon.com/ko/blogs/aws-cloud-financial-management/launch-aws-cost-explorer-rightsizing-recommendations-integrates-with-aws-compute-optimizer/


<br>
<br>


## ECS

Make use of automated tagging via the `propogate tags` option. This will help increase visibility into costs
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-using-tags.html


Container insights is super helpful for gaining visibility into what your containers are doing. This blog introduces the product and what you can do with it
https://aws.amazon.com/blogs/mt/introducing-container-insights-for-amazon-ecs/

For a full list of Amazon ECS Container Insights metrics, see Amazon ECS Container Insights Metrics https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-ECS.html

ECS Fargate is a highly recommended way for startups to deploy their applications as it  removes undifferentiated heavy lifting of managing instances. This blog post is a cost optimization checklist to help you optimize on cost.
https://aws.amazon.com/blogs/containers/cost-optimization-checklist-for-ecs-fargate/

To further optimize you can use Fargate spot for significant cost savings  
https://aws.amazon.com/blogs/compute/deep-dive-into-fargate-spot-to-run-your-ecs-tasks-for-up-to-70-less/  

But you need to architect for handling the interruptions if the computer resources get reclaimed.  
This japanese blog post describes how to do that.
https://aws.amazon.com/blogs/containers/graceful-shutdowns-with-ecs/  
[JP version]
https://aws.amazon.com/jp/blogs/news/graceful-shutdowns-with-ecs/

this workshop guides you through how to deploy using fargate spot  
https://ec2spotworkshops.com/ecs-spot-capacity-providers/module-2.html


<br>
<br>


## EKS

Make use of automated tagging.  
https://aws.amazon.com/about-aws/whats-new/2022/08/amazon-eks-cluster-level-cost-allocation-tagging/


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

<br>
<br>


## Graviton

This github repo is maintained by the AWS Graviton team. It is meant to help new users start using the Arm-based AWS Graviton and Graviton2 processors which power the latest generation of Amazon EC2 instances. While it calls out specific features of the Graviton processors themselves, this repository is also generically useful for anyone running code on Arm.  
https://github.com/aws/aws-graviton-getting-started

If you want to get hands on there is a workshop you can follow:  
https://graviton2-workshop.workshop.aws/en/gettingstarted.html

In general moving to a managed service is an easy way to reap immediate savings. this blog post outlines some of the considerations for RDS and Graviton:  
https://aws.amazon.com/blogs/database/key-considerations-in-moving-to-graviton2-for-amazon-rds-and-amazon-aurora-databases/

<br>
<br>


## Lambda

Understand how Lambda billing works.  
https://aws.amazon.com/blogs/aws/new-for-aws-lambda-1ms-billing-granularity-adds-cost-savings/ 

In general the formula is 
> Duration = Execution time (sec) * Function Size (allocated memory GB)  
> Cost = Number of Invocations * Duration 

This blog post series provides good guidance on how to optimize your lambda. Focus on Rightsizing using [AWS Lambda Powertuning Tool](https://github.com/alexcasalboni/aws-lambda-power-tuning) as the lowest hanging fruit  
Part 1: https://aws.amazon.com/ko/blogs/compute/optimizing-your-aws-lambda-costs-part-1/  
Part 2: https://aws.amazon.com/ko/blogs/compute/optimizing-your-aws-lambda-costs-part-2/  


[Provisioned concurrency](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html) is primarily intended to reduce cold start times. It can, however, help reduce cost when you have a constant steady state amount of invocations. This is because the duration cost of lambda in provisioned concurrency is ~70% less than on-demand. **Only attempt this if you are very sure about your utilization**
https://aws.amazon.com/lambda/pricing/


Review if graviton is a practical option:  
https://github.com/aws/aws-graviton-getting-started#lambda-on-graviton


Explore if commercial options like [Savings Plans](https://aws.amazon.com/about-aws/whats-new/2020/02/aws-lambda-participates-in-compute-savings-plans/) are a good fit. See if you can bundle this with other compute that you use.



This workshop will give you hands on guidance on different serverless optimization scenarios  
Serverless Optimization Workshop: https://catalog.us-east-1.prod.workshops.aws/workshops/2d960419-7d15-44e7-b540-fd3ebeb7ce2e/

To increase visibility, this blog walks you through logging and introduces [Embedded Metric Format](https://aws.amazon.com/about-aws/whats-new/2019/11/amazon-cloudwatch-launches-embedded-metric-format/) for custom metrics  
https://aws.amazon.com/ko/blogs/compute/operating-lambda-logging-and-custom-metrics/


<br>
<br>

## RDS

The lowest hanging Fruit is to migrate to Graviton based instances. More info on considerations in the [graviton section](#graviton)

Understanding how you are using your RDS instances is key to RDS optimization. A highly effective tool to aid you in this is `Performance Insights`  
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PerfInsights.html


These links provide practical hands on workshops to show you how to leverage Performance Insights to get the most out of your RDS instances

Performance Monitoring Workshop for RDS PostgreSQL and Aurora PostgreSQL - https://catalog.us-east-1.prod.workshops.aws/workshops/31babd91-aa9a-4415-8ebf-ce0a6556a216/en-US


RDS MySQL Performance Insights Lab - https://catalog.us-east-1.prod.workshops.aws/workshops/0135d1da-9f07-470c-9845-44ead3c78212/en-US/lab8

This workshop is part of a new program we run with startups to help developers be better practioners of relational databases. If you are interested in running this for your startup, please get in touch with us.  
DB4Dev workshop - https://catalog.workshops.aws/db4devs/en-US

<br>
<br>

## S3

key tip: "_If you don't need it, delete it_"



This workshop walks you through S3 Cost optimization tips: https://catalog.us-east-1.prod.workshops.aws/workshops/f238037c-8f0b-446e-9c15-ebcc4908901a/en-US/002-services/002-storage/003-s3


This blog post will outline how you can optimize for both predictable and dynamic access patterns - https://aws.amazon.com/blogs/storage/amazon-s3-cost-optimization-for-predictable-and-dynamic-access-patterns/

Use the S3 Storage Classes to optimize your storage costs:
https://aws.amazon.com/s3/storage-classes

<br>
<br>

## Spot
AWS Spot Instances are an amazing option allowing you to take advantage of spare capacity in AWS datacenters to receive up to 90% discounts on your instances. Spot is available to use with EC2 instances directly and also with ECS and EKS. You can learn more here 
[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)

The catch is if AWS needs that spare capacity, you will receive a 2 min warning before your instance is reclaimed. 

To learn how you might take advantage of this, you can try yourself in this workshop:
https://ec2spotworkshops.com/

Learn more about Spot: https://aws.amazon.com/ec2/spot

<br/>
<br/>  

## CloudWatch
Custom Metrics can be pushed to CloudWatch from your application:
https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html

Viewing standard and custom metrics in a CloudWatch dashboard:
https://catalog.workshops.aws/observability/en-US/metrics/viewmetrics

Reduce log-storage costs by automating retention settings in Amazon CloudWatch  
https://aws.amazon.com/ko/blogs/infrastructure-and-automation/reduce-log-storage-costs-by-automating-retention-settings-in-amazon-cloudwatch/
