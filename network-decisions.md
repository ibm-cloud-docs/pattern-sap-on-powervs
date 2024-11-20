---

copyright:
  years: 2024
lastupdated: "2024-11-17"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for network
{: #network-decisions}

| Architecture decision                    | Requirement                                                                                                            | Decision                                                                     | Rationale                                                                                                                                                                          |
|----|----|----|----|
| On-premise to IBM Cloud Enterprise connectivity        | Connectivity needed between client and IBM Cloud                                                                           | Direct Link Service                                        | Enterprise connection with built-in high availability. \n  High availability can be achieved with multiple instances. \n  Different bandwidths and metered/unmetered options to choose from.                                                     | 
| BYOIP/Edge Gateway        | Capability needed for customer to provide isolation, security and edge routing services	                                               | IBM Cloud VPC facilitates BYOIP  \n  Edge Gateways: Palo Alto, Fortinet, F5 - client choice based on requirements                         | Client can bring their own subnet IP address range to an IBM Cloud VPC \n  Edge Gateway is client choice based on requirements                                                     | 
| Network Segmentation/Isolation        | Ability to provide network isolation across workloads	                                               | VLAN, Subnet, LPAR                         |                                                    | 
| Cloud Native Connectivity (to cloud services)        | Ability to connect to cloud services over the private network	                                               | Virtual Private Endpoints in VPC through Transit Gateway                         | Communicate with IBM Cloud services over the private network using a virtual private endpoint (VPE)                                                   | 
| Cloud Landing-zone Connectivity between  VPC/PVS/Classic        | Connect across multiple VPCs and to IBM Cloud Classic environments	                                               | Transit Gateway                         | Use TGW to connect separate VPCs (Edge), Classic (if needed) and PowerVS.                                                   | 
| Between regions        | Connect multiple regions	                                               | Global Transit Gateway                         |                                                    | 
| Internet facing        | Global Routing option    DDoS protection	                                               | Cloud Internet Services (CIS)                        |   IBM CIS is based on CloudFlare, providing many routing and firewall features against internet traffic                                                 | 
| Load Balancing         | Load balancing HTTP, HTTPS, WebSocket workloads across multiple instances	                                               | IBM Cloud Application Load Balancer (ALB)                        |   ALB is a virtual load balancing service on layer 7, which may work with SAP web Dispatcher, may handle HTTP, HTTPS, WebSocket traffic.  \n   ALB may provide floating IP required by high availability clusters \n  NLB as another option provides layer 4 load balancing with higher cost                                                 | 
| Domain Name System (DNS)         | Ability for client to resolve DNS entries in IBM Cloud	                                               | IBM will continue to forward/relay the DNS to client DNS Servers onsite                        |   This is the default option in the absence of a specific customer requirement to manage DNS                                                 | 
{: caption="Architecture decisions for network" caption-side="bottom"}
