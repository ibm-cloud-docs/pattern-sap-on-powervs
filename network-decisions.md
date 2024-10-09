---

copyright:
  years: 2024
lastupdated: "2024-01-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for network
{: #network-decisions}

| Architecture decision                    | Requirement                                                                                                            | Decision                                                                     | Rationale                                                                                                                                                                          |
|----|----|----|----|
| Connectivity from Cloud to enterprise         | Connectivity that is needed between client and IBM Cloud                                                                           | Redundant Direct Link Connect Connections                                        | Preferred depending on security requirements. Lower cost than DL Dedicated                                                                                                             |
| Connectivity from Managed Service Providers   | Secure, encrypted connectivity between MSPs and IBM Cloud                                                                  | P2P VPN through VPC VPN Gateway                                                  | [VPN Gateway](/docs/vpc?topic=vpc-using-vpn) - securely connect Virtual Private Cloud (VPC) to another private network (site-2-site) for management purposes     |
|                                               |                                                                                                                            |                                                                                  | A VPN gateway consists of two back-end instances for high availability in the same zone                                                                                                |
| BYOIP/Edge Gateway                            | Capability that is needed for customers to provide isolation, security, and edge routing services                                    |IBM Cloud VPC facilitates BYOIP                                              | Client can [bring their own subnet](https://cloud.ibm.com/docs/vpc?topic=vpc-configuring-address-prefixes) IP address range to a IBM Cloud VPC                                         |
|                                               |                                                                                                                            |Edge Gateways: Palo Alto, Fortinet, F5 - client choice based on requirements | Edge Gateway is client choice based on requirements                                                                                                                                    |
| Network Segmentation/Isolation                | Ability to provide network isolation across workloads                                                                      | VPCs and subnets                                                                 | Native VPC isolation by using separate VPCs and subnets for prod and nonprod environments, and separation of workload                                                           |
|                                               |                                                                                                                            | Separate PowerVS LPARs                                                           | PowerVS isolation                                                                                                                                                                 |
| Cloud Native Connectivity (to cloud services) | Ability to connect to cloud services over the private network                                                              | Virtual Private Endpoints                                                        | Communicate with IBM Cloud services over the private network by using a virtual private endpoint (VPE)                                                                                    |
| Cloud Landing-zone Connectivity               | Connect across multiple VPCs and to IBM Cloud Classic environments                                                         | Transit Gateway \n Global Transit Gateway                                                                  | Use TGW to connect separate VPCs (Edge), Classic (if needed), and PowerVS. Global transit gateway to connect to environments in other regions for resiliency and data replication purposes |
| Load Balancing (Public)                       | Load balancing over the public network across two regions if an outage occurs (DR) for failover to the other region. | Cloud Internet Services (CIS)                                                    | Public load balancing for resiliency needs per SAP best practices. CIS also provides DDoS services. |
| Load Balancing (Private)                      | Load balancing workloads across multiple workload instances over the private network                                       | SAP Web Dispatcher \n IBM Cloud Application Load Balancer (ALB)                                                               | The ALB load balances inter-application server requests across Web Dispatcher hosts. The ALB is a floating IP with multiple subnets or servers that are attached to the backend pool. |
| Domain Name System (DNS)                      | Ability to resolve DNS names on site                                                                                       | IBM continues to forward or relay the DNS to client DNS Servers onsite          | This is the default option in the absence of a specific customer requirement to manage DNS                                                                                             |
{: caption="Architecture decisions for network" caption-side="bottom"}
