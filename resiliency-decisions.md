---

copyright:
  years: 2024
lastupdated: "2024-11-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for resiliency
{: #resiliency-decisions}

| Architecture decision | Requirement | Decision | Rationale |
|----|----|----|----|
|High Availability SAP                  | 99.5% SLA for SAP applications is required Or 99.95% infrastructure SLA is required |DB native replication: \n * HANA System Replication (HSR) \n * Oracle DataGuard \n * Db2 HADR \n * Sybase Replication Server \n * MSSQL Always-On \n * Cluster: \n * Pacemaker-based cluster with Red Hat Enterprise Linux HA Add-On, or with SUSE Linux High Availability Extension|Single zone high availability deployment of SAP application and database is supported.  [Multi-zone is possible](https://cloud.ibm.com/docs/sap?topic=sap-ha-rhel-mz){: external}|
|HANA Replication      | System Replication or Storage based replication         |HANA System Replication (HSR) | Asynchronized HANA System replication to the secondary region. \n To implement Storage based replication, please check with IBM Power System Virtual Server team first. |
|Disaster Recovery for SAP on Linux/AIX | Disaster recovery capability in secondary region      | IBM Storage Protect                                                                                                                                                                                                                                | * IBM Storage Protect Plus provides near instant recovery and replication in hybrid multi-cloud environments. \n [IBM Storage Protect Plus](https://www.ibm.com/products/ibm-storage-protect-plus/resources){: external} \n * Support for databases Standard lead with offering (MSSQL, Oracle, HANA) \n * Standard DR capability for RPO < 15 min, RTO < 4 hours is achievable \n * [Veeam is an alternative for AIX as the operating system](https://helpcenter.veeam.com/docs/backup/plugins/sap_hana_plugin.html?ver=120){: external}  |
| Disaster Recovery for SAP on AIX/IBM i | Disaster recovery capability in secondary region      | Global Replication Service (GRS)                                                                     | Global Replication Service-GRS is based on Global Mirror Replication as a configurable option. Global replication service is available only in WDC and DAL as of now. It will be available in all PowerVS regions soon. \n  [Global Replication Service-GRS](https://www.ibm.com/blog/announcement/introducing-global-replication-service-on-ibm-power-systems-virtual-server){: external}        |
| Disaster Recovery - Cost Optimized    | Low HANA disaster recovery capability in secondary regionCost as a priority instead of low RTO/RPO | Implement shared processor Pool                          | Set up shared processor pool to reserve capacity in the secondary region. Set up DR systems on minimum sized VMs to save operating cost. This is a Power Systems virtual server special feature.  \n Alternative: DR and Non-Production systems to share the same compute infrastructure       |
| Backup & Recovery on Power Systems Virtual Servers                         | Backup as a service                                                | Automated Secure Backup by Compass         | Backup as a service for IBM Power System Virtual Server workloads, including SAP HANA. \n  Backup for x86 workloads is coming soon.          |
| Backup – Linux/AIX/x86                         | Back up of NetWeaver and DB data                                                | IBM Storage Protect         | IBM Storage Protect is an SAP certified backup tool for SAP HANA and works with Backint.  \n    It is supported on both Power and x86, for SAP and NonSAP.  \n      Another option is Veeam.           |
| Backup – IBM i                          |                                                        | FalconStor VTLIBM Storage Protect         | Although SAP on IBM i/Power Systems Virtual Servers is not SAP certified, client may choose it if service provider supports. \n Alternative: Veeam is supported on AIX. \n  However, if there is HANA/Linux in client’s landscape, only one SAP certified backup tool should be used. Then IBM Storage Protect is recommended.   |
| Backup – Snapshot                         | Point in time copy of data volume                                                 | FlashCopy         | IBM Power Systems Virtual Servers offering : \n  SAP note 2039883 - FAQ: SAP HANA database and data snapshots (storage snapshots)Although SAP on IBM i/Power Systems Virtual Servers is not SAP certified, client may choose it if service provider supports. 
          |
{: caption="Architecture decsions for resiliency" caption-side="bottom"}
