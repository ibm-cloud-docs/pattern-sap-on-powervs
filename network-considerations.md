---

copyright:
  years: 2024
lastupdated: "2024-11-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

Networking is a key aspect of any cloud deployment that should not be overlooked.  The network design should consider enterprise connectivity, latency, throughput, resiliency, and security requirements.  

For security purposes, it is recommended to segregate production from non-production workloads as a best practice.  In addition, it’s also a best practice to segregate by application tiers (e.g., application vs. database).  PowerVS enables the creation of logical isolation between separate LPARs.

To provide isolation and centralize advanced security functions, the network design follows “Hub and spoke” VPC model.  The VPC Landing Zone (Edge VPC) serves as the hub for which all ingress and egress traffic flows.  The Edge is a virtual network (VPC) that acts as a central point of connectivity to on-premises network and all other VPC and PowerVS environments.  PowerVS is connected to the VPC Landing Zone via a Transit Gateway which allows traffic routing between each of the PowerVS, VPC and classic environments in the IBM Cloud account.

Enterprise connectivity is needed to connect the SAP environment to the client data center(s).  IBM Cloud Direct Link is typically used for this connectivity. Direct Link is a cloud native offering with built in high availability. Deploying multiple Direct Links can further increase high availability. 

A Workload VPC can be deployed into multiple regions if needed, to host x86 workloads, in any.  

A separate Management VPC (not illustrated) can be deployed into multiple regions if needed, to host management infrastructure and services.

All VPCs and Power Workspaces are connected through Transit Gateway.

Cloud Internet Services (CIS) is an FS Validated service [IBM Terms](https://www.ibm.com/support/customer/csol/terms/?id=i126-8065){: external}. It provides reliability, performance, and security for Internet facing applications, websites, and services using Cloudflare's 300+ Global Points of Presence (PoPs). It includes Domain Name Service (DNS), Global Load Balancer (GLB), Distributed Denial of Service (DDoS) protection, Web Application Firewall (WAF), Transport Layer Security (TLS), and Caching.

For a list of all Networking Considerations, see [networking design considerations](/docs/sap?topic=sap-networking-design-considerations).

Quick summary on connections: \n  -  Enterprise on-prem to IBM Cloud connection: Direct Link is a cloud native offering with built in high availability. Deploying multiple Direct Links can further increase availability. \n  - Internet traffic to IBM Cloud: CIS. \n  - Connection between VPCs and Power System Virtual Server workspaces: Transit Gateway and Power Edge Routers. \n  - Inter region connections: Global Transit Gateway. \n  -  Workloads segregation: Security Groups and ACLs can be configured with Edge VPC, Management VPC, SAP workloads in Power workspaces and Workload VPCs. \n  - Latency and network bandwidth considerations: 10 Gbps network bandwidth is usually required between SAP application and HANA. SAP Application and database layers should be closed to avoid unnecessary latency, hence it is not recommended to be separated on different platforms or availability zones.
