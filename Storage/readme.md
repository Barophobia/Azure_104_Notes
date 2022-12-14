# Storage

## Table of Contents

- [Storage](#storage)
  - [Table of Contents](#table-of-contents)
  - [Storage Accounts](#storage-accounts)
  - [Interaction tools](#interaction-tools)
    - [Storage explorer](#storage-explorer)
    - [AzCopy](#azcopy)
    - [Databox](#databox)
      - [Benefits](#benefits)
      - [Specifications](#specifications)
      - [Databox Components](#databox-components)
  - [Access tiers](#access-tiers)
  - [Storage account resiliency](#storage-account-resiliency)
    - [Types of redundancy](#types-of-redundancy)
      - [Locally Redundant Storage (LRS)](#locally-redundant-storage-lrs)
      - [Zone Redundant Storage (ZRS)](#zone-redundant-storage-zrs)
      - [GRS](#grs)
      - [GZRS](#gzrs)
  - [Storage Access Control](#storage-access-control)
    - [Shared Account Keys](#shared-account-keys)
      - [Protect your access keys](#protect-your-access-keys)
      - [Viewing Access Keys](#viewing-access-keys)
    - [Shared Access Signatures (SAS)](#shared-access-signatures-sas)
      - [Types of shared access signatures](#types-of-shared-access-signatures)
        - [User delegation SAS](#user-delegation-sas)
        - [Service SAS](#service-sas)
        - [Account SAS](#account-sas)
      - [Forms of SAS](#forms-of-sas)
      - [How SAS works](#how-sas-works)
      - [When to use SAS](#when-to-use-sas)
      - [Best practices with SAS](#best-practices-with-sas)
    - [Azure Active Directory Integration](#azure-active-directory-integration)

## Storage Accounts

Storage accounts contain all of your azure storage data objects, including blobs, file shares, queues, tables and disks, on creation they must have a unique name (This is unique to the whole of azure not just your subscription) and allows access from anywhere in the world over HTTP or HTTPS.

## Interaction tools

There are many ways to interact with data that is stored on azure, the easiest being through the azure portal.

### Storage explorer

The storage explorer application is provided by microsoft, using this you can connect to different storage accounts and resource allocated to the account you have signed in to.

You can also use this tool to upload data to a storage resource. 

![storage explorer](images/storage_explorer.png)

### AzCopy

AZCopy is a command-line utility that you can use to copy blobs or files to and from a storage account.  To use AZCopy you must authorise using either Azure Active Directory or a SAS Token. AZCopy can be used to create containers, upload and download data. 

![azcopy Example](images/azcopy.png)

### Databox

Databox is the azure solution that lets you send terabytes of data into and out of azure in a quick, inexpensive and reliable way. The secure data transfer is accelerated by shipping a proprietary storage device to the user to put their data on and send back, currently the maximum usable storage capacity is 80TB. The device has rugged casing to protect and secure data during the transit.

You can order the data box via the azure portal. Once the device is received, you can quickly set it up using the local web UI.

![Databox webUI](images/databox_webui.png)

Import use cases:
  
- Onetime Migration:
    When a large amount of on-prem data needs to be moved to azure.

- Initial bulk transfer (Seedbox):
    An initial bulk transfer is done using Data box (seed) follow by incremental transfers over the network.

Export use cases:

- Disaster recovery of a large amount of data:
    When a copy of the data from azure is needed to be restored to an on-prem environment.

- Migration back to on prem:
    When you want to move all the data back to on-prem or another cloud service provider.

#### Benefits

**Speed** - Databox uses 1-Gbps or 10Gbps network interfaces to move data in and out of azure

**Secure** - Databox has built in security protects:
    - The device has a rugged casing secured by tamper resistant screws and tamper evident stickers.
    - The data on the device is encrpyted with AES-256 encryption at all times.
    - The device can only be unlocked with a password provided in the Azure portal
    - Once the data from an import order is uploaded to azure,, the disks on the device are wiped clean in accordance with NIST 800-88r1 standards.

#### Specifications

![Databox Specs](images/databox_specs.png)

#### Databox Components

![Databox_view](images/data-box-combined.png)

## Access tiers

**Hot** - A tier optimised for storing data that is accessed or modified frequently. The hot tier has the highest storage costs, but lowest access costs.

**Cool** - A tier optimised for storing data that is infrequently accessed or modified. Data in the cool tier should be stored for a minimum of 30 days. The cool tier has lower storage costs and higher access costs compared to the hot tier.

**Archive** - An offline tier omptimised for storing data that is rarely accessed with flexible latency requirements, on the order of hours. Data in the archive tier should be stored for a minimum of 180 days.

## Storage account resiliency

Azure storage always stores multiple copies of your data so that it's protected from planned and unplanned events. Redundancy ensures that a storage account always meets its availability and durability targets even when failures occur.

When deciciding which resiliency option to choose there are tradeoffs that will need to be considered for example lower costs and higher availability.

### Types of redundancy

#### Locally Redundant Storage (LRS)

Locally redundant storage replicates your storage account three times within a single data center in the primary region. LRS provides atleast 11 nines uptime over a given year.

LRS is the lowest cost redundancy option and offers the least durability compared to other options. LRS protects your data against server rack and drive failures. However, if a disaster such as a fire or flood occurs within the data center, all replicas of a storage account using LRS may be lost or unrecoverable.

![LRS](images/locally-redundant-storage.png)

#### Zone Redundant Storage (ZRS)

Zone redundant storage replicates your storage account synchronously across three azure availability zones in the primary region. Each availability zone is a seperate physical location with independent power, cooling and networking. ZRS provides availability of at least 12 nines over a given year.

With ZRS,your data is  still accessible for both read and write operations even if a zone is down. If a zone becomes unavailable azure will deal with the networking updates such as DNS repointing, this may take some time to complete so an application may have temporary issues before the networking has been updated.

![ZRS](images/zone-redundant-storage.png)

ZRS provides excellent performance, low latency and resiliency for your data if it becomes temporarily unavailable. However, ZRS by itself may not protect your data against a regional disaster where multiple zones are permanently affected.

#### GRS

Geo-Redundant Storage copies your data synchronously three times within a single physical location in the primary region using LRS, then it copies the data asynchronously to a single physical location in a secondary region, when the data is written to the second region it is then replication within that location using LRS. GRS provides availability of at least 16 nines ove ra given year.

![GRS](images/geo-redundant-storage.png)

#### GZRS

Geo-Zone-Redundant-Storage combines the high availability provided by redundancy across availability zones with protection from regional outages provided by geo-replication. Data in a GZRS Storage account is copied across three azure availability zones in the primary region and is also replicated to a secondary geographic region for protection from regional disasters.

With a GZRS storage account you are able to continue to read and write data if an availability zone becomes unavailable or is unrecoverable. Additionally, your data is ptoected in the case of a complete regional outage or a disaster in which the primary region isn't recoverable. GZRS is designed to provide at least 16 nines of availability over a given year.

![GZRS](images/geo-zone-redundant-storage.png)

## Storage Access Control

Each time you access data in a storage account, your client application makes a request over HTTPS/HTTP. By default, every resource in Azure Storage is secured and every request to a secure resource must be authorised.

The following table shows the options that azure storage offers for authorising access to data.

![Auth Chart](/Storage/images/auth_chart.png)

### Shared Account Keys

When you create a storage account, Azure generates two 512-bit storage account access keys for the account. These keys can be used to authorise access to data in your storage account via shared key authorisation.

Microsoft recommends that you use Azure key vault to manage access keys and that you regularly rotate and regenerate keys. Using azure key vault makes it easy to rotate keys without interruption to applications.

#### Protect your access keys

Storage account access keys are similar to a root password for your storage account.

#### Viewing Access Keys

Access keys can be found under the 'Security + Networking' Section of the storage account. 

Inside of the 'Access Keys' option you can also set a reminder so that you never forget to rotate or regenerate keys. If you wanted to manually rotate or regenerate keys this is also where you could do it.

### Shared Access Signatures (SAS)

A shared access signature provides secure delegated access to resources in a storage account. With a SAS, you have control over how a client can access your data.
For example:
    - What resources the client may access
    - What permissions they have with those resources.
    - How long the SAS is valid

#### Types of shared access signatures

This is used to allow control over what can be done by the client.

When generating the SAS a URI will be generated that can be used with Azure storage explorer.

Azure storage supports three types of shared access signatures:
    - User delegation SAS
    - Service SAS
    - Account SAS

##### User delegation SAS

A user delegation SAS is secured with Azure active directory credentials and also by the permissions specified for the SAS. User delegation SAS applies to Blob Storage only.

##### Service SAS

A service SAS is secured with the Storage account key. A service SAS delegates access to a resource in only one of the Azure storage Services: Blob, Queue, Table or Azure Files.

##### Account SAS

An account SAS is secured with the storage account key. An account SAS delegates access to resources in one or more of the storage services. All operations available via a service or user delegation SAS are also available via an account SAS.

#### Forms of SAS

- Ad hoc SAS:
  - When you create an ad hoc SAS, the start time, expiry time and permissions are specified in the SAS URI. Any type of SAS can be an ad hoc SAS.

- Service SAS with storage access policy:
  - A stored access policy is defined on a resource container, which can be a blob container, tbale queue or file share. The stored access policy can be used to manage constraints for one or more service shared access signatures. When you associate a service SAS with a stored access policy, the SAS inherits the constraints i.e the start time, expiry time and permissions that were defined in the stored access policy.

#### How SAS works

A shared access signature is a signed URI that points to one or more storage resources. The URI includes a token that contains a special set of query parameters. The token indicates how the resources may be accessed by the client. The signature is constructed from the SAS parameters and signed with the key that was used to create the SAS. This signature is used by Azure storage to authorise access to the storage resource.

![SAS URI Example](images/sas-storage-uri.png)

#### When to use SAS

A SAS should be used to give secure access to resources in a storage account to any client who does not otherwise have permissions to that resource.

#### Best practices with SAS

When you use SAS in your applications, you need to be aware of these two potential risks:
    - If a SAS is leaked, it cna be used by anyone who obtains it.
    - If a SAS provided to a client application expires and the application is unable to retrieve a new SAS from the service, the applications functionality may be hindered.

Recommendations:
    - Always use HTTPS to create and/or distribute a SAS
    - Use a user delegation SAS when possible (AD Auth SAS)
    - Have a revocation plan in place
    - Configure a SAS Expiration policy
    - Create a stored access policy for a service SAS

### Azure Active Directory Integration

You can use AAD for authorising requests to blob, queue and table resources. Microsoft recommends using Azure AD credentials to authorize requests to data when possible for optimal security and ease of use.