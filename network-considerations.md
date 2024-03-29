---

copyright:
  years: 2024
lastupdated: "2024-01-12"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

Networking is a key aspect of any cloud deployment that should not be
overlooked. The network design should consider enterprise connectivity,
latency, throughput, resiliency, and security requirements.

For security purposes, it is recommended to isolate production from
nonproduction workloads as a best practice. In addition, it's also a
best practice to isolate by application tiers (for example application versus
database). PowerVS enables the creation of logical isolation across
separate LPARs.

To provide isolation and centralized advanced security functions, the
network design follows the "Hub and spoke" VPC model. The Edge VPC serves as
the hub for which all ingress and egress traffic flows. The Edge is a
virtual network (VPC) that acts as a central point of connectivity to
on-premises network and all other VPC and PowerVS environments. PowerVS
is connected to the Edge ("Hub") through a Transit Gateway that allows
traffic routing between each of the PowerVS, VPC, and classic
environments in the IBM Cloud account.

Enterprise connectivity is needed to connect the SAP environment to one or more client data centers. IBM Cloud Direct Link is typically used for this
connectivity and if redundancy is needed, two direct links can be used
in a resilient design.

A separate Management VPC (not illustrated) can be deployed into
multiple regions if needed, to host management infrastructure and
services that are also connected to the Edge and PowerVS through Transit Gateway.

For a list of all Networking Considerations, see [networking design considerations](/docs/sap?topic=sap-networking-design-considerations).
