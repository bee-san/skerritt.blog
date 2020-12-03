---
template: post
title: Disaster Recovery with AWS
slug: Aws-disaster-recovery
socialImage: /media/p2p.jpg
draft: false
date: 2020-12-02T23:42:12.596Z
description: A quick introduction to disaster & recovery in AWS
category: AWS
---

We'll need to invoke our disaster recovery plans to restore our datta if our storage or server fails.

With traditional backup methods, the data we need might not be available because:
* Backup data is stored in the same location as the production data, and the disaster impacted the backups.
* If using a tape backup method, the tapes could fail making the data unreadable.
* The tapes could get lost when in transit.
* Manual involvement could lead to errors, such as incorrect tape rotation and labelling.

Not to mention how ineffective traditional backups might be:
* Scalability: As our infrastructure expands, so will our backup systems. This can be very costly.
* Costs: Implementing an effective backup solution can be a huge upfront cost.
* Data Availability: If our data is stored off site, it may take longer to get our data.

The speed at which we can launch our environment in AWS to replicate our production system is of significant value.

Benefits of using Cloud Storage for our DR include:
* Offsite backup.
* No scalability constraints.
* No huge upfront costs.
* High Durability and availability. 

Now lets imagine our production environment in our local data centre experiences an outage.

We can launch a new VPC with new AMIs with custom applications. We can create EBS storage volumes based on the backed up data within AWS s3 and attach those volumes to our instances.

We now have our production back up and running.

The main benefits are:
* Cost Efficient.
* Scalable.
* Available and Durable.
* Secure.
* Reliable.
* Zero maintenance of hardware.
* Offsite storage.
* Replication & automation easily configured.
* Readily Available.
* Easy to test DR plans using AWS infrastructure.

# Considerations when using AWS as a DR solution
We have to balance storage solution fit for our purposes with conforming to specific DR compliance set by government regulations.

Let's discuss 2 terms.

* Recovery Time Objective (RTO)
Maximum amount of time in which a service can remain unavailable before it's classed as damaging to the business.
* Recovery Point Objective (RPO)
Maximum amount of time for which data could be lost for a service.

## How to get data in and out of AWS?
The method in which we choose to move our data from on-premise to the cloud varies  on our own infrastructure. If we have a direct connection to AWS, we can use that with connectivity of 10 gbp/s.

We may need a hardware/software VPN that can be use. 

Or we can use our own internet connection to AWS.

Depending on how much data we need to use, we may need to use something else as the lines won't have enough bandwidth.

We can use AWS snowball.

<figure>
	<img src="/media/awsdr/snowball.jpg" alt="">
	<figcaption></figcaption>
</figure>

They come in 50TB or 80TB in size to our datacentre, where we can copy our data to it before it is shipped back to AWS for uploading to S3. 

We can use multiple snowballs to transfer petabyte of data.

In extreme circumstances, we can use Snowmobile.
<figure>
	<img src="/media/awsdr/snowmobile.jpg" alt="">
	<figcaption></figcaption>
</figure

This can transfer up to 100PB per snowmobile (45-foot shipping container) pulled by a semi-trailer truck. **It is for exabyte-scale transfer service**.

### Storage Gateway
A software appliance is configured on site in our data centre and offers a range of moving our data into AWS.

## How quickly do we need our data back?
This closely relates to our RTO requirements and how critical the data is to our business.

Our connectivity to AWS also plays an important part in this timeframe.

## How much data to import / export?

We should also calculate our target transfer rate. TO help us calculate this, we can use a calculator.

Our data backup solution needs to offer the capacity and we have the means to transfer the data there.

## Security
Ensuring our data has the right level of security and safeguarding it from unauthorised access is essential.

When working with sensitive information, we must encrypt the data in-transit and at rest.

## Compliance

Compliant with laws.

AWS has AWS artifact which allows us to review and access AWS compliance reports.

We can issue to auditors.

Accessed via the AWS management console and issued by external auditors to AWS themselves.

# Using Amazon S3 as a backup solution
S3 has:
* Huge capacity to scale
* Store data from 1 byte to 5TB
* Multiple security features
* 3 storage classes offering different benefits
* Highly durable
* Highly available

| Class             | Durability | Availability | Price |
|-------------------|------------|--------------|-------|
| Standard          | 11 9s      | 4 9s         | £££   |
| Infrequent Access | 11 9s      | 3 9s         | ££    |
| Glacier           | 11 9s      | N/A          | £     |

## Standard
The reliability has an SLA of the service. This level of durability is achieved by automatic-replication to multiple devices and multiple accessibility zones.

Also supports in-rest and in-transit encryption.

Data management capabilities through life cycle policies to automatically move data to another storage class for cost optimisation or it can delete the data all together.

## Infrequent Access
Used for data that is accessed less frequently than standard. The availability takes a hit, but the cost is far less than standard class. 

Commonly used for backups as we have same durability and immeditade retrieval when needed.

Uses the same SLA as S3 standard class.

Same security & device management as standard class. 

The main different is the cost!

## Glacier

This is classed as a different service, but it operates in conjunction with S3.

Stores data in archives, as opposed to S3 buckets.

Can be up to 40TB in size.

Stored in vaults, with different security measures to that of S3.

Used for data archiving and is commonly referred tto as the cold storage service.

We can move data into glacier using:
* Lifecycle rules from S3
* AWS SDKs
* Amazon Glacier API

Also retains the same level as durability, and encryption in-transit and in-rest.

Also has its own security measures that differ from S3. Such as write-once-read-many (WORM) and vault access policies.

Can help comply to HIPAA and PCI in an overall solution.

The most significant difference is that we do not have immediate access.

Depending on what we use, data retrieval can take from minutes to hours. This can be a problem if we are in a DR situation whereby we need immediate access.

There are a number of retrieval methods.

### Expedited
* Used for urgent access to a subset of an archive.
* Less than 250mb.
* Data in 1 - 5 minutes.
* 3 cents per GB, 1 cent per request.

### Standard
* Retrieve any of our archives, regardless of size.
* Takes 3 - 5 hours
* 1 cent per GB, 5 cents per 1000 requests (cheaper).

### Bulk
* Cheapest option
* Petabytes of data
* 5 - 12 hours
* 0.0025 per GB, 0.025 per 1,000 requests.

## S3 Cross Region Replication
By default, S3 will not replicate across regions, we have to specifically request that.

From a DR point of view, we want to configure this to help with:
* Reduced latency of data retrieval (if one datacentre is having a bad time, we can use another in a different region).
* Governance & Compliance (We may need to store backup data at a minimum distance from the source)

## Multipart uploads
* **Multiple concurrent reads & writes (performance). If a folder is larger than 100MB, we should use multi-part upload.**
This allows us to break an object down into separate parts and upload it (like Bittorrnt).

## S3 Security
* IAM policies - allow and restrict access to S3 buckets.
* Bucket Policies - JSON policies assigned to individual S3 buckets
* Access control lists - which user or AWS account can access an object?
* Lifecycle policies - automatically manage and move data between classes based on compliance and governance controls.
* MFA delete - User has to enter MFA code to delete object which prevents accidental deletion
* Versioning - Ensures we can recover from misuse of object or accidental deletion. But requires additional space as a separate object is made for each version.

We should use as many of these as possible based on the risk factor of the data being stored.

# AWS Snowball
* Petabyte of scale
* 50TB or 80TB device
* Dust, water and tamper resistant.
* All data is automatically encrypted with keys generated by AWS Key Management Service.
* End to end tracking with E ink shipping label.
* Can be tracked with AWS SNS or via management console.
* AWS Snowball is HIPAA compliant.

We need ot create an export job in AWS. We then receive delivery of Snowball. We connect it to our local network. We then transfer the data.

# AWS Storage Gateway
Downloaded as a VM, and allows us to use file, volume, and tape gateway configurations.

## File Gateways
Mount or map drives to an S3 bucket as it it were a share held locally.

Encrypted with SSE-S3.

As well as this, also has a local cache on premise which reduces egress traffic loss.

We must associate with S3 bucket which it then presents as an NFS gateway.

Like Dropbox, but for S3.

## Stored Volume Gateways
Backup local storage volumes to S3 while entire data library is on premise for low latency access. iSCSI devices mapped to on-premise storage. 

Data written to NAs/SAN/DAS then asynchronously sync with S3. Also provides a buffer, and has a maximum storage of 512TiB.

Data is sent over an encrypted SSL channel, and storage gateway makes it easy to take snapshots which are stored as EBS snapshots on S3. These snapshots are incremental so only the changes are stored.

Makes recovering from a disaster very simple.

## Cached Volume Gateways
* Primary data storage is S3
* Local data storage is used for buffering and a local cache for recently accessed data.
* Each volume can be up to 32TiB with 32 gateways so up to 1024TiB total.
* Possible to take EBS snapshots.

## Virtual Tape Library
* Use Glacier for data archiving
* Replacing physical components with virtual
* Tape backup infrastructure with AWS
* Storage gateway has a capacity to hold 1500 tapes.
* Virtual tapes with 100GiB to 2.5TiB in size. Backed by S3 and appear in virtual table library.
* Every VTL has 10 Tape Drives.
* Media changer - manages tapes to and from tape drive to VTL and is presented as an iSCSI.
* Archive - archive tapes from our VTL to glacier (VTL = virtual tape library). Storage gateway uses standard retrieval which takes 3 - 5 hours.