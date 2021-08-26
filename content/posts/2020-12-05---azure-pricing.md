---
template: post
title: "Azure Pricing & Support"
slug: azure-pricing-support
socialImage: /media/image-3.jpg
draft: true
date: 2020-12-02T01:37:42.899Z
description: "Intro to pricing with Azure"
category: "Azure"
-tags:
    - "AZ-900"
---

In order to use Azure, we need an Azure subscription.

Azure Subscriptions are linked to accounts that created the subscription.

There are 3 main types of subscriptions:
* Free
Unlimited access with £200 credit as as trial.
* Pay as you go
Pay for the services and resources that we use on a monthly basis.
* Member Benefits
Like MDN subscribers. Substantial discounts over pay as you go subscription.

The person who creates the Azure subscription becomes the global administrator for that subscription.

Separate subscriptions can be a way to create a division of responsibility for Azure services.

There are 3 purchasing options.
* Enterprise

Customer enters into an enterprise agreement.

To qualify a private business must have 500 users and devices, public needs 250 users and devices.

Enterprise enjoy savings of 15 - 40%.

* Web Direct

Normal pay as you go plan billed monthly. Pay public prices. We should review the additional options for savings.

* Cloud Service Providers (CSP)
Microsoft partnered companies. Billing and payments are billed directly to the CSP.

Virtual networks are free. But many do on a usage called metering. These are considered metered resources.

The few factors are:
* Type of resource
* Size of resource (CPUs, Memory, Network)
* Time Based (deallocated machines do not incur charges)

Bandwidth charges exist. But mostly for egress traffic (outbound). Outbound data incurs charges after the first 5GB per month. 

The price calculating tool is an excellent online tool to assist in estimating the costs of deploying to azure.

# Minimising Azure Costs

Spending Limits and Quotas. The azure subscription is suspended when the limit is met. 

We can:
* Remove spending limit indefinitely
* Remove spending period for current billing period
* Keep the current spending period

We can tag to azure resources for cost tracking. Tags can be applied on project, department, environment or any other purposes.

With Azure Reservations we can pay in advanced for specific products. 1 year or 3 year periods with up to 72% cost savings over pay as you go.

Azure advisor is a tool that can be used to assist in managing Azure costs. The Advisor has 4 blades. We can use this to identify under-utilised resources.

# Support Plans
* Basics
No technical support
* Developer
Trial and non production environments

Response time is 8 hours.
* Standard

24/7 access. response time is 1 hour.

* Professional Direct
24/7 and response within 1 hour. Opertional support, training and proactive guidance.
* Premier

24/7 with 15 minute. All features of direct but guidance by a technical account manager,