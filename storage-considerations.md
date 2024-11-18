---

copyright:
  years: 2024
lastupdated: "2024-11-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Storage design
{: #storage-design}

SAP solutions want to ensure that there is enough available storage to accommodate the existing environment and allow for additional data growth for primary, backup, and archive storage. You need to choose the appropriate SAP Certified profile to meet primary storage and growth requirements for workloads.

The storage tiers in Power Systems Virtual Server are based on I/O operations per second (IOPS). It means that the performance of your
storage volumes is limited to the maximum number of IOPS based on storage tier.

IBM Power Virtual Server offers you the option to select an I/O operation per second (IOPS) based storage as per your requirements. Flexible IOPS is a tier-less storage offering that removes the notion of disk type and replace it with a storage pool. Each of the storage pools supports multiple storage tiers. The storage tiers are based on different IOPS levels.


The following tiers of FlashSystem storage is available for IBM Power System Virtual servers:

- Fixed IOPs (5000 IOPs) - Provides a fixed performance level of 5000 IOPs, ideal for predictable workloads.
- Tier 0 - High-performance storage for latency-sensitive, mission-critical applications.
- Tier 1 - Balanced storage option offering a mix of performance and capacity for high performance like HANA.
- Tier 3 - Cost-effective, general-purpose storage designed for less demanding, archival, or backup workloads

For each Power Systems Virtual Server instance, select storage from a variety of storage tiers.  For the most up to date documentation see the [storage tiers topic](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).

Specific SAP storage guidelines can be found at [Storage Guidelines for SAP HANA based on Flexible IOPS](/docs/sap?topic=sap-storage-design-considerations#sap-fiops-config)

When you plan an SAP deployment, IOPS and its effect on latency needs to also be considered. When choosing a storage tier, make sure that you consider not just the average I/O load, but more importantly the peak IOPS of your storage workload.

For SAP NetWeaver and SAP AnyDB databases (such as IBM Db2 or Oracle DB), Tier 1 (NVMe) is recommended but Tier 3 (SSD) can be used.
Typically, Tier 3 storage tier is not suitable for production workloads.

The client is responsible for backing up data on PowerVS storage. Custom backup solutions can use Veeam or Spectrum Protect on Bare metal with local disk for operational and Cloud Object Storage for 2nd copy and long-term archiving. Backups over the network need to be considered for backup windows and restores.

[Other Storage Considerations](https://cloud.ibm.com/docs/sap?topic=sap-storage-design-considerations)
