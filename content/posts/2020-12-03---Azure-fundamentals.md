---
template: post
title: Overview of Azure Services
slug: azure-overview-services
socialImage: /media/p2p.jpg
draft: false
date: 2020-12-02T23:42:12.596Z
description: "What are the different Azure services?"
tags:
    - "azure"
    - "cloud"
    - "AZ-900"
category: "cloud"
---

- [Compute](#compute)
  - [Azure Virtual Machines](#azure-virtual-machines)
  - [Azure App Service](#azure-app-service)
  - [Azure Container Instance](#azure-container-instance)
  - [Azure Functions](#azure-functions)
- [Storage](#storage)
  - [Blob Storage](#blob-storage)
  - [Azure File Storage](#azure-file-storage)
  - [Azure Data Lake Storage Gen2](#azure-data-lake-storage-gen2)
  - [Relational Databases](#relational-databases)
  - [Azure Synapse Analytics](#azure-synapse-analytics)
  - [NoSQL](#nosql)
- [Netowkring](#netowkring)
  - [Virtual Network (VNet)](#virtual-network-vnet)
  - [Subnets](#subnets)
  - [VVNet peering](#vvnet-peering)
  - [Azure VPN](#azure-vpn)
  - [ExpressRoute](#expressroute)
- [Miigration](#miigration)
  - [Azure Migrates](#azure-migrates)
  - [Azure Active Directory](#azure-active-directory)
- [DevOps](#devops)
  - [Azure DevOps](#azure-devops)
  - [Azure Pipelines](#azure-pipelines)
  - [Azure DevTest Labs](#azure-devtest-labs)
  - [Azure CDN](#azure-cdn)
- [IoT](#iot)
  - [Azure IoT Central](#azure-iot-central)
  - [Azure IoT Hub](#azure-iot-hub)
  - [Azure Sphere](#azure-sphere)
- [Analytics](#analytics)
  - [Azure HDInsight](#azure-hdinsight)
  - [Azure Databricks](#azure-databricks)
  - [Azure Synapse Analytics](#azure-synapse-analytics-1)
- [AI](#ai)
  - [Cognitive Services](#cognitive-services)
  - [Azure Bot Service](#azure-bot-service)
  - [Azure Machine Learning Studio](#azure-machine-learning-studio)
  - [Machine Learning Services](#machine-learning-services)
- [Integration](#integration)
  - [Logic Apps](#logic-apps)
  - [Event Grid](#event-grid)

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

# Miigration
## Azure Migrates
Help migrates on-premise to the cloud.
## Azure Active Directory
Syncs on-premise with Azure directory through Windows Active Directory.

# DevOps
## Azure DevOps
Family of other things in this category.
## Azure Pipelines
Creates automated workflows (CI).
## Azure DevTest Labs
Spin up non-production environments easily.
## Azure CDN
Is a CDN, uses edge server and caching to serve content faster.
# IoT
## Azure IoT Central
Fully managed SAAS that lets us create IoT applications.
## Azure IoT Hub
More customised, handles communications with millions of IoT devices. It's what IoT central uses behind the scenes.
## Azure Sphere
Make IoT devices more secure.
# Analytics
## Azure HDInsight
Big data frameworks such as Hadoop.
## Azure Databricks
More user friendly than Spark
## Azure Synapse Analytics
Combines data warehouse functionality with support for Spark.
# AI
## Cognitive Services
Used for prebuilt AI tools. Don't need to know machine learning to use.
Grouped into 5 categories.
1. Decision
2. Language
3. Speech
4. Vision (classify images)
5. Web search
## Azure Bot Service
Create chatbots.
## Azure Machine Learning Studio
Lets us train and deploy machine learning models with a drag & drop interface.
## Machine Learning Services
Full control overy stage of the ML process.

# Integration
## Logic Apps
Detect events that happen and notifies us or something else. 
## Event Grid
We'd normally need to use Event Grid to notify our logic app of particular events.