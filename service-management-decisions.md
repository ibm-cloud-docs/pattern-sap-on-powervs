---

copyright:
  years: 2024
lastupdated: "2024-11-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for service management
{: #service management}

| Architecture decision    | Requirement | Decision | Rationale |
|----|----|----|----|
| SAP Monitoring    |Provide Integration, Exception, Health, and System Monitoring                        |SAP Solution Manager   \n  SAP FocusRun|SAP Native tools             |
| Non-SAP application monitoring   |                                                                                 |Instana (BYO Monitoring)                        |Instana provides additional application performance metrics and automate application performance management for the Web, App, and Database tiers. Instana provides data and actionable insights to monitor the applications and automate root-cause analysis.              |  
| Cloud Platform Monitoring   |  Monitor and correlate performance metrics and events                                                                               | IBM Cloud Infrastructure Monitoring (SysDig)                        |Instana provides additional application performance metrics and automate application performance management for the Web, App, and Database tiers. Instana provides data and actionable insights to monitor the applications and automate root-cause analysis.              |  
| Logging    |  Diagnose issues, analyze stack traces and exceptions, identify the source of errors, and monitor different log sources through a single view      | IBM Cloud Logs                        |  IBM Cloud Logs is a scalable logging service that persists logs and provides users with capabilities for querying, tailing, and visualizing logs. [IBM Cloud Logs ](https://cloud.ibm.com/docs/cloud-logs){: external}             |  
| Management/Orchestration          |  Automate management processes to keep applications and infrastructure secure, up to date, and available                                                                               |Watson AIOPs, Ansible  + Terraform                         |                            |  
| Security monitoring   |  Security Information and Event Management (SIEM) tool that can be used to monitor security events within your SAP environment.                                                                               | IBM QRadar                     |Collects and analyzes security data from SAP systems and IBM Cloud. \n  Detects and alerts on potential security threats. \n   Integration with SAP security logs and IBM Cloud security services.                      |  
{: caption="Architecture decisions for service management" caption-side="bottom"}
