---
title: Management Fundamentals for AWS
date: "2020-12-03T23:46:37.121Z"
template: "post"
draft: false
slug: "AWS-management"
category: "Cloud"
tags:
  - "VPN"
  - "Privacy"
  - "AWS"
description: "Management Fundamentals for AWS."
socialImage: "/media/p2p.jpg"
---

# AWS Config
One of the largest headaches we have is understanding:
* What resources do we have? Do we have resources that are no longer needed?
* Their status, security vulns.
* How are they linked?
* What changes have occurred on a resource?
* Is the infrastructure compliant with governance controls?
* Accurate auditing information?

AWS Config records and captures source changes allowing us to perform actions against the data. It can:
* Capture resource changes
* Act as a resource inventory.
* Store configuration history for individual resources
* Provide a snapshot of configurations
* Notifications about changes (using SNS)
* Provide AWS CloudTrail integration (who made the change and when)
* Use rules to check compliance
* Security Analysis
* Identify relationships between resources

AWS Config does not capture this for all services, but iit does for the most common services such as EC2, VPC, RDS, S3, IAMA.

AWS Config is region specific. We have to configure AWS Config for each region we want to have AWS config for.

# CloudTrail
Record and track all AWS API requests. Can be from a user using an SDK, AWS CLI or more.

When autoscaling launches an instance, this is recorded by cloudtrail.

Every API request is recorded as an event that's stored in a log file on S3.

New log files are typically created every 5 minutes and then stored in an S3 bucket. Also can deliver to a CloudWatch logs log file (for custom metrics).

Supports all regions and over 60 AWS services & features.

## Use cases for captured data
Effective for security analysis. Answers "What is the API call and who made it and when?"

Can resolve and manage day-to-day operational issues such as who, what, and when an API was used which could have cause an outage.

