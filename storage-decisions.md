---

copyright:
  years: 2024
lastupdated: "2024-11-17"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for storage
{: #storage-decisions}

| Architecture decision       | Requirement                                       | Decision                                                                                                                                           | Rationale      |
|----|----|----|----|
| SAP HANA data and log      | High I/O required by SAP to meet performance requirements                                       | At least Tier 1 FlashStorage is required for Production HANA    | For Non-Production HANA, lower tier storage may be used but performance will be negatively impacted |                                                                                  |
| AnyDB Data and log      | Tier 1 FlashStorage for big production database that performance may be a concern            |                                             | Tier 3 storage can be used for smaller databases, or non-production databases       |      
| SAP Netweaver installation and application logs      | General purpose            |   Tier 3 FlashStorage                                          | General purpose storage         |      
| Shared storage      | SAP mounts for /usr/sap/trans, /sapmnt, and so on  \n Shared storage for High Availability Cluster            |   A cluster of Power System virtual servers with highly available storage as NFS server to provide the shared storage                                          | Third party service CTERA can be an option too         |   
{: caption="Architecture decisions for storage" caption-side="bottom"}
