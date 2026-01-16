---

copyright:
  years: 2026
lastupdated: "2026-01-16"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Migration design
{: #migration-design}

There are several migration scenarios, but the most straight-forward is a
direct "lift-and-shift" (homogeneous) where the Infrastructure and SAP
versions remain the same. For example, on-premises SAP NetWeaver ABAP 7.0
running on VMWare to the same environment on cloud. Migration from
on-premises to another infrastructure platform or SAP version
(heterogeneous) can become more complex, especially when combined with a
DB conversion or application server upgrade.

For a list of migration options and tools, see [Moving SAP Workloads](/docs/sap?topic=sap-faq-moving-sap-workloads#faq-moving-sap-workloads-overview).

Types for SAP Migration :

There are two types of SAP migration categories:

•	Homogeneous - Target has the same OS/DB/SAP versions as the source.

•	Heterogeneous - Target has a different OS, SAP or database type or version than the source


The following tables summarize various approaches for a homogeneous and
heterogeneous migration; all dependent on client environments and
preferences.

## Homogeneous Migration :
{: #homogeneous-migration}

| Migration method                                       | Technique summary                                                  | Advantages and concerns                                                 | Associated tools**                                                  |
| - | - | - | - |
| Virtual Machine (VM) Backup and Restore                     | Create lpar image while application is offline. Use the image to create a VM on IBM Power System Virtual Server                                                                                  | -	Lift and shift operation. \n  -	Potentially big downtime window so it is best for smaller images \n  -	Configurations may need to be updated post migration. | Aspera for data transfer  \n  IBM Expert Labs for optional professional migration service  |
| Database Backup and Restore                     | Backup the source database using native DBMS tools. \n   Restore backup copy to a "shell" copy of source system prebuilt on PowerVS, using identical versions of software.    |-   Time to transfer large database backups may require big downtime window. \n  -	•	Target needs same/compatible vendor software to restore from backups file(s) received. | Aspera for initial data transfer \n  Backup/Restore tools for backup and recovery, as well as delta sync: Veeam, Spectrum Protect and Cobalt Iron by Compass    |
| Fresh Build and Copy the Config                     | Build a fresh copy of the SAP system on PowerVS and copy/reenter configuration parameters as required.    |Good for applications and middleware servers not requiring data transfer.                                                                                                 Risk of error introduction if post installation manual procedures are applied to reproduce exact configuration. |     |
| Create a Disaster Recovery System                     | Create a DR system on IBM Power System Virtual Servers and establish continuous data replication until Failover during GoLive    |Minimum downtime.  | Database native such as  HANA System Replication  \n  Continuous Data Protection: Veeam, Spectrum Protect \n  Third Party tools for replication, such as LinBit DR     |
{: caption="Homogeneous migration" caption-side="bottom"}

## Heterogeneous migration :
{: #heterogeneous-migration}

| Migration method                                                                    | Technique summary                                                                                                                                   | Advantages and concerns                                                                                           | Associated tools                |
|----|----|----|----|
| SAP Export/Import                       | Move or Re-Platform to different CPU Architecture, OS, or database. Uses System        |-   Extended downtime window.  \n  -  Network bandwidth may impact the performance of migration negatively   | SAP tool SWPM, DMO is an option allowing DB conversion at the same time of migration  |
| Two Step Migration: Lift and Shift, followed by transformation                     | Create a staging environment in IBM Cloud as a target to Lift&Shift  the on-premise system. \n  Migrate the staging system to IBM Power System Virtual Server with desired OS/DB/SAP version  |Multiple Extended downtime windows.  \n   Complex execution requires expert level technical knowledge and planning skills | SAP software to build "shell" system;  \n Aspera (optional) to expedite lift and shift transfer; \n  SAP SUM for Netweaver upgrade;\n SAP SWPM with DMO for migration with database conversion  |
| IBM Services and Partner Tools (e.g. SNP) [SNP](https://www.snpgroup.com){: external}                     | IBM Consulting provides enterprise system migration services from planning to execution.     | Expertise of IBM Consulting  \n  Minimal downtime. | SAP installation software;  \n SNP CrystalBridge (via IBM Consulting); \n SNP Cockpit (via IBM Consulting).  |
{: caption="Heterogeneous migration" caption-side="bottom"}

IBM Migration services:

*	Expert Labs
* IBM Services for Cloud Migration
* IBM Cloud Partners


More Information on SAP Migration to IBM Power Systems Virtual Servers :

- For more information on migrating SAP to IBM Power System Virtual servers: [Doc](/docs/sap?topic=sap-sapmig-overview)

- For more information on migration to IBM Power System Virtual server, especially if you have workloads on AIX or IBM i, please refer to: [Doc](/docs/power-iaas?topic=power-iaas-system-migration)
