---
template: post
title: Overview of Azure Services 
slug: azure-overview-services
socialImage: /media/p2p.jpg
draft: false
date: 2020-12-02T23:42:12.596Z
description: What are the different Azure services?
category: cloud
tags:
    - "azure"
    - "cloud"
    - "AZ-900"
---

# Compute

## Azure Virtual Machines

Runs VMs for Windows & Linux. If we currently have VMs, the easiest way to migrate is to "lift and shift". Take our VMs on premise and migrate to the cloud.

Azure VMs are known as Infrastructure as a service.

## Azure App Service
Platform as a service. We can host applications here like Heroku without worrying about the underlying infrastructure.

If we have an application that is not a web or mobile app we have to use VMs.

## Azure Container Instance
Let's us host containers. Microsoft provides a variety of ways to run containers. THe simplest way is Azure container services.

If we have a more complex setup we might want to use Azure Kubernetes service.

## Azure Functions
Microsoft's main serverless functionality. The consumption plan is better as we only pay for when a function is running.

# Storage
## Blob Storage
Object storage, collection of files. Flat structure, used for unstructured data. 

One of the great things is that it has multiple access tiers.
* Hot: frequently accessed
* Cool: infrequently accessed
* Archive: rarely accessed. Also takes several hours to get files out.

## Azure File Storage
Typical SMB storage. Can mount in Windows. Is hierarchical.

## Azure Data Lake Storage Gen2
Hadoop compatible storage for use with data analytics software.

## Relational Databases
* Azure SQL Database
* MySql, MariaDB and PostgreSQL for open source DBs.

## Azure Synapse Analytics
For data warehouses.

## NoSQL
* Azure Cosmos DB
* Azure Cache for Redis


# Netowkring
## Virtual Network (VNet)
* Virtual Network
## Subnets
* Routes that define how traffic shifts between thing
By default all outbound traffic is allowed, for income we need an IP address assigned.
## VVNet peering
Can get VNets to talk to eachother.
## Azure VPN
Sends encrypted traffic over the internet.
## ExpressRoute
Private dedicated connection between us and Azure. Provides higher speed & reliability.

