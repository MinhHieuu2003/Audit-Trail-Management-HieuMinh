---
title : "Preparation Steps"
date :  2025-07-30
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---


{{% notice info %}}
You need to create one Linux instance in the public subnet and one Windows instance in the private subnet in advance to perform this lab.
{{% /notice %}}

To learn how to create EC2 instances and VPCs with public/private subnets, you can refer to the following labs:
  - [Introduction to Amazon EC2](https://000004.awsstudygroup.com/vi/)
  - [Working with Amazon VPC](https://000003.awsstudygroup.com/vi/)

To use System Manager to manage Windows instances in particular and all your instances on AWS in general, you need to grant permissions for your instances to work with System Manager. In this preparation section, we will also create an IAM Role to allow the instances to work with System Manager.