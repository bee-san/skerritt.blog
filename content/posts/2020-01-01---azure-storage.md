---
template: post
title: Overview of Azure Storage
slug: azure-overview-storage
socialImage: /media/p2p.jpg
draft: false
date: 2020-12-02T23:42:12.596Z
description: "Overview of Azure storage?"
tags:
    - "Azure"
    - "Cloud"
    - "AZ-900"
category: "Cloud"
---

# Blob storage
Binary Large Object (Blob) storage is a way of storing large files.

There are 3 types of Blobs in Azure:
## Blob Blocks
Divided into blocks of up to 100MB in size. Blobs of up to 4.75TB can be stored as blob blocks in Azure.

Using multiple blocks to represent the blob allows for more efficient handling of large blobs. Usually, the complexity of managing individual blocks is handled for you so you can simply deal with the entire blob rather than individual blocks.

## Append Blobs
Append blobs are optimized for appending new data at the end of the blob. This is particularly useful for storing log data where new lines are added at the end and the data never needs to be modified after it is written.

## Page Blobs
Page blobs are optimized for random read/write operations. The name comes from the practice of operating systems organizing memory into pages of relatively small sizes that can be easily managed. In Azure, page blobs are collections of individual pages of up to 4MB each. They are used for storing virtual machine disks in Azure.

# Creating Storage
<figure>
	<img src="/media/azurestorage/1.png" alt="">
	<figcaption></figcaption>
</figure>

The Status Indicates that the Primary storage location is Available. In the event of an outage in Azure, you may see a different value here. This storage account has no secondary storage location, but you can create storage accounts with primary and secondary storage locations. 
The Replication property of a storage account determines this.

The Performance can be standard or premium. When you need guaranteed latency you should use premium storage. Premium storage has much higher storage costs because they use solid-state drives (SSDs) whereas standard storage uses magnetic spinning hard disk drives (HDDs).

Access tier optimizes the storage and cost based on how frequently data is accessed. The Hot tier is for frequently accessed data and carries the highest cost for storage but the lowest cost for accessing the data. The cool and archive tiers reduce are suited for less frequently accessed data with archive offering the lowest cost for storage but the highest cost for accessing data. The archive tier actually stores the data offline and the data needs to be "rehydrated" to the hot or cool storage before it can be read. Cool and archive tiers also include a penalty if you delete the blob within 30 days and 180 days, respectively, of when they are first moved into these tiers.
The Replication sets the durability and availability of the storage. The following options are available:
* Locally-redundant storage (LRS) is the cheapest option and stores the data in a single data center. If that data center goes offline you will not be able to access the data.
* Zone-redundant storage (ZRS) stores data across three data centers in a region. It can tolerate individual data center outages but not regional outages.
* Geo-redundant storage (GRS) stores data across multiple data centers in two regions, a primary region and a secondary region. This option is more expensive but can tolerate entire regional outages. There is also read-access geo-redundant storage (RA-GRS) which allows you to read from the secondary region compared to GRS which only allows you to access the secondary in the case of a Microsoft-initiated region failover to the secondary.
* 
Finally, the Account kind describes if the storage account is general-purpose or specialized. General-purpose accounts allow storage of blobs, tables, files, and queues whereas specialized kinds only allow one type such as only blob storage. There are different pricing models for each account kind so a specialized kind may reduce your costs. StorageV2 is the recommended default.

Blobs are stored inside of containers.

General-purpose azure storage accounts can store files on network accessible file shares. Blob storage can store any type of file as well but file shares are best suited for use cases where you want to share files using computers' file systems to make accessing and sharing files easy. Azure file shares support the industry-standard Server Message Block (SMB) protocol and can be used to share files across Windows, macOS, and Linux machines. 

Azure virtual machines (VMs) use Azure disks as their attached disk storage. Azure disks are built-on top of page blobs which are the type of blobs optimized for random access. When you create Azure disks you can choose to manage the storage account yourself or to use managed disks where Azure manages the storage account for you. Managed disks are the preferred option. Within managed disks you can choose between:

* Ultra SSDs which provide the best throughput and I/O operations per second (IOPS) performance characteristics but at the highest prices. Consider Ultra SSDs for mission-critical I/O intense applications such as running databases.
* Premium SSDs are the next best performing and are well-suited to production workloads with all but the highest performance I/O requirements that may benefit from using Ultra SSDs.
* Standard SSDs are the least expensive SSD option and are suitable for production workloads with low I/O performance requirements such as web servers and lightly used applications.
* Standard HDDs use spinning disk technology and are therefore the least expensive option but also provide the lowest performance. Use them for backups and infrequently accessed applications.
* 
Azure disks give you the freedom to attach and detach from different VMs. They will maintain their data but the data is only usable when a disk is attached to a VM. You will inspect a VM with two disks attached to it in this Lab Step.

# Virtual Machines

Each VM has one OS disk which contains the operating system and is used to boot the VM. 

All disks are encrypted at rest automatically and transparently to any users. This means if someone were to steal a physical disk from an Azure data center the physical disk would be encrypted and unusable. 

This is true for all data in Azure storage accounts. However, for Azure disks, you can also encrypt the virtual disk at the operating system level. This is referred to as Azure Disk Encryption (ADE). 

This protects against someone attempting to copy your Azure disk and attach it to an Azure VM because they would not be able to decrypt the data without the encryption key. Azure recommends enabling ADE for production workloads.

Azure automatically provides a Temporary Storage disk that will be lost forever once the VM is deleted, while Azure disks can be attached and detached from VMs and persist their data. The data disk the VM has attached to it is not automatically formatted and does not appear in the list. Each operating system provides tools to format the data disks, but that is outside of the scope of this Lab.

