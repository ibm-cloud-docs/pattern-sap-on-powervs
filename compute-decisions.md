---

copyright:
  years: 2024
lastupdated: "2024-11-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for compute
{: #compute-decisions}

| Architecture decision              | Requirement                             | Decision                | Rationale                                     |
|----|----|----|----|
| Compute (NetWeaver)                      | SAP certified \n  SAPS requirements |SAP certified on S922, E980, S1022 and E1080  \n Shared cores  |Each core provides 5570 – 7600 SAPS depending on the machine type. \n As granular as 0.25 cores can be provisioned for each VM. \n Resize could be done without restarting VM within a limit. |
| Compute (HANA)                                  | SAP certified  \n  RAM/SAPS requirements          | SAP certified Scale-Up and Scale-Out HANA profiles on E980, S1022 and E1080 \n Dedicated cores |SAP certified HANA profiles, with RAM range from 256GB to 32TB RAM  \n  Select profiles for OLAP or OLTP  \n  Both scale-up and scale-out are supported.  \n  Each machine type has a max limit on number of cores and RAM. Make sure each HANA resource requirement is within the limit. |
| Compute (AnyDB) | SAP certified    | SAP certified on S922, E980, S1022 and E1080        |Oracle should use dedicated cores. \n If no specific licensing requirement, shared cores may be use for other databases. |
| SAP BOBI                | Supportability  \n  SAP Certified                                   | SAP certified Gen2 VSI in Workload VPC          |   SAP BOBI is supported on x86 only           |
| Jump Box               | Segregate from Workloads \n Easy access from VPN \n  Can access Internet \n  Can connect to workload VMs                         | SAP certified Gen2 VSI in VPC Landing Zone          |                                                                                   |
| Management Systems               | Segregate from Workloads  \n  Easy access from VPN  \n Can connect to workload VMs                         | Gen2 VSI in VPC Landing Zone (Edge VPC or Management VPC)          |                                                                                   |
{: caption="Architecture decisions for compute" caption-side="bottom"}
