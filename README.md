# AWS Cost Optimization Resources for Startups
Welcome. This reference has been prepared by Solutions Architects at AWS to help Startups easily find additional resources that provide specific guidance on various techniques for effective cost optimization.  

We hope this proves useful as you navigate the various options available to you for maximizing the value you can get out of running on AWS. As always, should you have questions on anything, please don't hesitate to contact your local startup team. you can also email <sup-apj@amazon.com>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Contents

- [No Effort Options](#no-effort-options)
  - [Savings Plans](#savings-plans)
  - [Spot](#spot)
- [Services](#services)
  - [EC2](#ec2)
  - [EBS](#ebs)
  - [RDS](#rds)
  - [DynamoDB](#dynamodb)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
  
    
<br>
<br>
<br>

# No Effort Options


## Savings Plans

## Spot
AWS Spot Instances are an amazing option allowing you to take advantage of spare capacity in AWS datacenters to receive up to 90% discounts on your instances. You can learn more here 
[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)

The catch is if AWS needs that spare capacity, you will receive a 2 min warning before your instance is reclaimed. 

To learn how you might take advantage of this, you can try yourself in this workshop:
https://ec2spotworkshops.com/


# Services
## EC2


## EBS
In general, for almost all workloads, if you are on GP2 you will benefit from moving to GP3.
https://aws.amazon.com/about-aws/whats-new/2020/12/introducing-new-amazon-ebs-general-purpose-volumes-gp3/

Find out how much you stand to save with this EBS GP2 to GP3 Cost savings calculator: https://d1.awsstatic.com/product-marketing/Storage/EBS/gp2_gp3_CostOptimizer.dd5eac2187ef7678f4922fcc3d96982992964ba5.xlsx
  
Here's a blog post describing how you can migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs: https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/



## RDS
## DynamoDB