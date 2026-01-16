---

copyright:
  years: 2026
lastupdated: "2026-01-16"

subcollection: pattern-sap-on-powervs

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Compute design
{: #compute-design}

IBM® Power® Virtual Server is an IBM Power server offering. You can use the [Power Virtual Server](/docs/power-iaas?topic=power-iaas-getting-started) to deploy a virtual server, also known as a logical partition (LPAR), in a matter of minutes. You can provision flexible, secure, and scalable compute capacity for Power enterprise workloads both on IBM Power Virtual Server (Off-premises and On-premises) in your data center.

IBM Power System Virtual Servers are currently available with flexible hardware configurations on Power S922, S1022, E980, E1050, E1080 and S1122.

The Flexibility of IBM Power Systems Virtual Servers hardware capability
includes:

-   Cores (CPU)

-   Memory (RAM)

-   Data volume size

-   Data volume type / performance tier

-   Network interfaces

-   PowerVM Host Pinning Policy (soft or hard)

-   PowerVM Host CPU Binding (dedicated or shared)

-   Shared Processor Pool for capacity reservation

SAP has certified Power Systems Virtual Server profiles to meet client requirements. Please refer to SAP notes 2947579 and 2855850 for the most up to date information. All SAP HANA profiles require dedicated cores. SAP HANA scale-up and scale-out configurations are both supported on IBM Power Systems Virtual servers.

For information on SAP HANA Scale Out configuration on IBM Power Systems Virtual servers:
[IBM Power Virtual Server certified profiles for SAP NetWeaver](https://cloud.ibm.com/docs/sap?topic=sap-refarch-hana-scaleout){: external}

IBM Power Virtual Servers are available with fully adjustable CPU Cores and Memory (RAM GB). It is permitted to define a custom size of the IBM Power Virtual Server to use for SAP NetWeaver, in accordance with existing SAP NetWeaver or AnyDB for IBM Power Systems best practices and guidance from SAP.

Compute and OS considerations:
[OS considerations](https://cloud.ibm.com/docs/sap?topic=sap-compute-os-design-considerations){: external}

For sizing information see:  Sizing process for SAP Systems
[sizing information](https://cloud.ibm.com/docs/sap?topic=sap-sizing&interface=ui){: external}

For a distributed SAP installation, to avoid latency caused issues, SAP does not support the application and database layers to be deployed across different platforms.

Shared processor Pool offers an option for clients to reserve capacity with minimum compute for Disaster Recovery systems.
