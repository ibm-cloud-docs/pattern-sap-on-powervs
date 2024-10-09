---

copyright:
  years: 2024
lastupdated: "2024-01-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for storage
{: #storage-decisions}

| Architecture decision       | Requirement                                       | Decision                                                                                                                                           | Rationale      |
|----|----|----|----|
| Primary Storage - Production      | SAP HANA DB size 128 GB - 768 GB                                       | Flash Storage from IBM FS9000 series devices     | * Fixed 5,000 IOPS storage for storing log files. Log files are usually up to 512 GB and need the high performance \n * Tier 0 storage for data file system \n * Tier 3 storage for shared file system \n * Maximize performance and optimize costs for peak IOPS workload|
|       | SAP HANA DB size 960 GB - 22.5 TB                 | Flash Storage from IBM FS9000 series devices                                                                                                             | * Tier 0 storage for storing log files. Log files are usually up to 512 GB and need the high performance \n * Tier 3 storage for data file system \n * Tier 3 storage for shared file system  \n * Maximize performance and optimize costs for peak IOPS workload|
| Primary Storage - nonproduction | Tier 3 - 3 IOPS                                        | Flash Storage from IBM FS9000 series devices                                                                                                             | Recommended for all non-DB tiers (App. Servers) including noncritical DB LPARs |                    |
| Backup Storage                    | Backup storage for servers                             | Bare Metal with local disk                                                                                                                               | Bare Metal on classic offers profiles to accommodate larger storage sizes.
|                                   |                                                        | Block storage                                                                                                                                            |Cloud Object Storage for offsite 2^nd^ copy for lower costs                 |
|                                   |                                                        | Cloud Object Storage                                                                                                                                     | Combine Block and Cloud Object Storage for long-term needs                                   |                    |
| Data or Storage Migration \n For more migration information, see [Moving SAP Workloads](/docs/sap?topic=sap-faq-moving-sap-workloads#faq-moving-sap-workloads-overview)| Migration tools from existing environment to PowerVS | Migration tools from existing environment to PowerVS                                                                                               |Image import obviates the need for testing and is useful for nonproduction or POC systems
|                                   |                                                        |DB DR Replication                                                                                                                                    |Using Native DB Replication minimizes the need for testing efforts
|                                   |                                                        |SAP Standard Migrations Tools                                                                                                                        |SAP Standard Migration options like SWPM, DMO
|                                   |                                                        |Backup and Restore tools                                                                                                                                |Aspera for high-speed data transfer ideal for Migrations
|                                   |                                                        |Aspera data transfer                                                                                                                                 | Minimize
|                                   |                                                        | GLVM                                                                                                                                                 | Business disruption due to migration
|                                   |                                                        |     | Cost and efforts that are incurred in testing migrated databases                     |                    |
{: caption="Architecture decisions for storage" caption-side="bottom"}
