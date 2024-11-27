---

copyright:
  years: 2024
lastupdated: "2024-11-17"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Resiliency design
{: #resiliency-design}

**Resiliency solution components:**

Resiliency is the ability of a workload to meet a specific target Service Level Objective (SLO), Service Level Availability (SLA) or recover from a service disruption and still meet the required SLA.  Resiliency needs to be considered at both the infrastructure and application layers across the entire solution.
PVS regions

A resilient design will include Backup&Recovery and, may include Disaster Recovery (DR) and High Availability (HA) depending on Service Level Availability (SLA) requirements. 


**Backup and Recovery:**

For HANA data protection, SAP provides tools: 
- HANA Studio - An integrated development environment for managing, modeling, and monitoring SAP HANA databases.
- HANACOCKPIT - A web-based tool for administering, monitoring, and managing SAP HANA systems.
- Backint - A certified SAP interface for integrating third-party backup tools with SAP HANA for backup and restore operations.

For SAP certified HANA backup tools, please refer to SAP note 2031547.
On IBM Power System Virtual Servers, Veeam, Spectrum Protect and Cobalt Iron from Compass are recommended tools and services.

**Disaster Recovery:**

Disaster Recovery is to recover and restore system operations after a disruptive event. These events can range from natural disasters like earthquakes or floods to man-made events like cyber-attacks, power outages, or hardware failures. 

A performance-optimized disaster recovery (DR) solution is designed to not only recover from disruptions but also to do so in a manner that minimizes downtime and maintains performance levels close to or as good as the production environment. The goal is to ensure that recovery operations are efficient and that the DR site performs well during and after failover. 

- *Low Recovery Time Objective (RTO):* Aim to minimize the time it takes to restore services to their normal state. This involves using technologies and strategies that allow for quick failover, such as pre-staged and fully synchronized replicas of data and systems.
- *Low Recovery Point Objective (RPO):* Ensure that data loss is kept to a minimum by implementing frequent, near-real-time data replication and backup solutions. 
A cost-optimized disaster recovery (DR) solution aims to balance the need for effective disaster recovery with budget constraints. The focus is on achieving reliable recovery while managing and minimizing expenses.

Instead of dedicated infrastructure for DR systems, which may be idle most of the time, shared infrastructure may be configured so that DR systems share the same compute with Non-Production systems, if segmentation/compliance/licensing/Non-Production system availability and other client requirements allow.

Also, using reduced-size compute for dedicated DR systems may be an option as well. To reserve the capacity for DR systems, Shared Processor Pool can be setup with a small fee.

**High Availability :**

High Availability Purpose and Metrics- 

High Availability is to ensure systems remain operational and accessible with minimal downtime, even in the event of failures. The goal of HA is to provide continuous service by eliminating single points of failure and ensuring that critical components have redundant systems or processes in place. 

Service Level Availability (SLA) is the major metrics for high availability. When SLA requirement for the SAP application is higher than 99.5%, it is recommended to implement HA.



**Single Point Failures of SAP S/4HANA on IBM Power Systems Virtual Servers:**


| Components       | Recommendation   | 
|------------------|------------------|
| SAP Web Dispatcher                 | [SAP Web Dispatcher ](https://help.sap.com/doc/saphelp_nw73ehp1/7.31.19/en-us/48/9a9a6b48c673e8e10000000a42189b/frameset.htm){: external }    |
| SAP Central Services (ASCS for ABAP system, SCS for Java system)                 |              |
| SAP Application server                 | Multiple application servers        |
| SAP HANA                 |               |
| Shared Storage                 | [SAP Web Dispatcher ](https://cloud.ibm.com/docs/sap?topic=sap-ha-rhel-nfs)       |
| Networking                 | Highly available IBM Cloud services. For example, Direct Link, Transit Gateway, Application Load Balancer        |

{: caption="Resiliency options" caption-side="bottom"}


The SAP HANA database supports high availability in a distributed system by providing for host auto-failover. If an active host fails, for example, because of a hardware failure, standby hosts can take over and ensure the continued availability of the database. 

IBM Power Systems Virtual Servers are designed by hardened configuration within single data center to provide 99.95% SLA. For more details, please refer to [IBM Terms](https://www.ibm.com/support/customer/csol/terms/?id=i126-9268&lc=en#detail-document)

To increase availability for SAP systems on IBM Power Systems Virtual servers, High Availability instances can be deployed with “Different Server” placement group, and Disaster Recovery systems can be deployed in a different region.

To setup HA cluster for SAP applications and databases, both data replication and cluster management should be considered. Data replication can be done with database native methods, OS native tools, as well as third party continuous data protection tools. Cluster management on Linux can be done with Red Hat High Availability Add-On or SUSE High Availability Extension.

For more information on SAP HA Implementation on IBM Cloud: [SAP HA](https://cloud.ibm.com/docs/sap?topic=sap-ha-overview)

**Availability for SAP Central services :**

The following should not be different for classic/VPC/PVS, since it is more on Operating System/Application layer. 
1.	SAP documents on ASCS/ERS1: [SAP Doc](https://community.sap.com/t5/technology-blogs-by-members/sap-ascs-high-availability-using-ers-explained/ba-p/13511647){: external}
2.	SAP documents on ERS1 and ENSA2: [SAP Doc](https://community.sap.com/t5/enterprise-resource-planning-blogs-by-members/evolution-of-ensa2-and-ers2/ba-p/13481209){: external}
3.	SUSE documents on setting up HA: 
•	[ERS1](https://documentation.suse.com/sbp/sap-15/html/SAP-nw740-sle15-setupguide/index.html){: external}
•	[ENSA2](https://documentation.suse.com/sbp/sap-12/html/SAP_S4HA10_SetupGuide-SLE12/index.html){: external}
4.	RHEL documents on setting up HA: 
•	[ERS1](https://access.redhat.com/articles/3569681){: external}
•	[ENSA2](https://access.redhat.com/articles/3974941){: external}



**High Availability for SAP HANA :**

1.	SAP Documentation on SAP HANA replications, including synchronization mode and operation mode: [SAP Doc](https://help.sap.com/docs/SAP_HANA_PLATFORM/6b94445c94ae495c83a19646e7c3fd56/6d252db7cdd044d19ad85b46e6c294a4.html){: external}
2.	IBM Cloud documentation on SAP HANA high Availability: [SAP HA](https://cloud.ibm.com/docs/sap?topic=sap-ha-rhel-hana-sr)
3.	SUSE documentation on SAP HANA high availability: [SUSE DOC](https://documentation.suse.com/sles-sap/sap-ha-support/html/sap-ha-support/index.html){: external}
4.	RHEL documentation on SAP HANA high availability: [RHEL DOC](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_for_sap_solutions/8/html/red_hat_ha_solutions_for_sap_hana_s4hana_and_netweaver_based_sap_applications/asmb_sh_ha_sol_for_hana_ha-sol-hana-netweaver){: external}
