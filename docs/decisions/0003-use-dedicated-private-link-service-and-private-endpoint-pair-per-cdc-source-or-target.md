---
status: "proposed"
date: 2025-03-28
decision-makers: 
consulted: 
informed: 
---

# Use a dedicated Private Link Service and Private Endpoint pair per CDC source or target, with IP address mapping

## Context and Problem Statement

We aim to provide secure access between our 3rd-party managed Estuary Flow Private Deployment data plane in Azure Australia East and our various change data capture (CDC) targets and sources, both within the same Azure region and on-premises. To achieve this, we need to determine the most suitable private connectivity option. While considering [ADR-0002](0002-use-private-link-services-in-hub-vnet.md), it was recognised that a design pattern for the number of Azure Private Links and associated components was also needed, which is covered by this decision record.

## Decision Drivers

Align with the [Estuary Flow Private Deployment option](https://docs.estuary.dev/getting-started/deployment-options/#private-deployment) using Azure Private Link, and the design principles of the [Azure Well-Architected Framework (WAF)](https://learn.microsoft.com/en-us/azure/well-architected/pillars) pillars at the workload level:

* Operational Excellence
* Cost Optimisation
* Security
* Reliability
* Performance Efficiency

## Considered Options

* Dedicated Azure private link service and private endpoint pair per CDC source or target, with IP address mapping
* Single Azure private link for all CDC sources and targets, with TCP/UDP port to IP mapping
* Single Azure private link service and dedicated private endpoint per CDC source or target, with TCP Proxy v2

## Decision Outcome

Chosen option: "Dedicated private link service and private endpoint pair per CDC source or target, with IP address mapping", because it is operationally simpler than the alternatives.

## Pros and Cons of the Options

### Dedicated Azure private link service and private endpoint pair per CDC source or target, with IP address mapping

**Method:** provision a dedicated private link service (PLS) and private endpoint (PE) pair for each CDC source or target. Use the following IP address mapping scheme for each CDC source or target, with standard address translation/resolution methods managed by each team.

|Entry Id.| Match                            | -> Map To     | Translation Method | Entry Managed By                            |
|---------|----------------------------------|---------------|--------------------|---------------------------------------------|
| 1a      | CDC source or target domain name | PE IP address | DNS Resolver       | Estuary Team (Private Link Consumer Tenant) |
| 1b      | PLS SNAT IP address              | CDC source or target domain name in landing zone VNet or on-prem network | Firewall DNAT | Firewall Team (Private Link Provider Tenant) |

* Good operationally, because mapping IP addresses one-to-one is less management overhead than alternative methods, such as using layer-4 TCP and UDP ports.
* Good reliability, because a simple mapping scheme is less prone to error and leads to a more robust system.
* Bad cost optimisation and operationally inefficient, because of the need to deploy multiple PLSs and PEs for multiple CDC sources or targets. Note, additional load balancer costs would also be incurred when exceeding eight CDC sources or targets due to the [Azure limit of 8 private link services per load balancer](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-private-link-limits).

### Single Azure private link for all CDC sources and targets, with TCP/UDP port to IP mapping

**Method:** provision a single PLS and a single PE (single shared private link) for all CDC sources and targets. Define a scheme that maps unique layer-4 TCP and UDP ports to each CDC source or target IP address.

* Bad operationally, because maintaining a layer-4 port to layer-3 IP address mapping scheme increases management overhead compared to alternative methods. <!-- to-do: check with Estuary team if specifying ports is even possible, e.g., inside the Flow UI -->
* Neutral reliability, because effort to coordinate a more complex mapping scheme between Estuary users and firewall admins could lead to a more brittle system. I.e., complexity is increased where both layer-4 port and layer-3 address translation are involved.
* Good cost optimisation and operational efficiency, because a single PLS and a single PE for all CDC sources and targets is economical use of Azure resources.

### Single Azure private link service and dedicated private endpoint per CDC source or target, with TCP Proxy v2

**Method:** provision a single PLS for all CDC sources and targets, and multiple PEs, one for each CDC source or target. Use [TCP Proxy v2](https://learn.microsoft.com/en-us/azure/private-link/private-link-service-overview#getting-connection-information-using-tcp-proxy-v2) to identify the PE IP address or link ID in each TCP session

* Good operationally, because a scheme that maps PE link IDs to CDC source or target IP addresses is relatively low management overhead, and a single PLS is efficient use of Azure resources.
* Bad operationally, because a proxy server needs to be maintained and supported, such as [NGINX](https://docs.nginx.com/nginx/admin-guide/load-balancer/using-proxy-protocol/).
* Bad performance, because UDP is not supported.

## More Information

Refer to [ADR-0002 More Information](0002-use-private-link-services-in-hub-vnet.md#more-information) for a reference design and a conceptual design.
