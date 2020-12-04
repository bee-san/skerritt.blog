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

# AWS Trusted Advisor
Recommend improves across AWS account based on AWS best practices.
* Cost Optimisation (save money)
* Performance (finds performance issues)
* Security (finds security weaknesses)
* Fault tolerance (best practices to maintain server operations)

Free 6 core checks.
* Service limits
* Security groups, EBS snapshots, RDS snapshots, IAM use, MFA on root account.

Business and above has AWS Support API and can track them using the AWS trusted advisor dashboard.

Trusted advisor notifications (completely free). Tracks cost savings and emails up to 3 recipients over a week.

Exclude items allows us to exclude specific resources.

Action Links, many checks have hyperlinks which lets us quickly reach the issue to resolve it ASAP.

Access management, tightly integrated with IAM.

data is automatically refreshed every 24 hours, but manual every 5 minutes if we want.

# CloudWatch
Monitor resources via a series of metrics and allow us to quickly react to events and dynamically adjust any availability or scalability issues. The metrics dependant on each service as each service is used different.

Can also create custom metrics if we need to measure specific things.

Basic monitor records metrics every 5 minutes. Detailed monitoring records at 1 minute intervals. Comes at an additional cost though.

All cloudwatch detail is recorded for 2 weeks.

Alarms are pre-defined thresholds. Let's say our server reaches 90% CPU utilisation. Cloudwatch will notify us of the impending disaster. The response would be to launch another server to even the load (auto-scaling). Or send us a message via SNS.

Alarms have 3 states:
* Ok (its not bad, its okay)
* Alarm (metric is outside of threshold and alarm is activated)
* Insufficient data (not enough data to determine alarm state)

Has a logging repository. We can go to a single place to see all logs, such as multiple web servers from a single place. We can also export the logs and use a third party tool to analyse the data.

# AWS Health Dashboard
Offers service & personal health dashboards.

Service provides a complete health check of all services in all regions at that time (or past 7 days).

Personal health dashboard will notify you of any service disruptions that you are using in your account. It is for disruptions that personally affect you.

We can also view planned maintenance and scheduled changes in our health dashboards.