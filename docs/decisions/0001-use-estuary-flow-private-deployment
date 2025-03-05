---
status: "proposed"
date: 2025-03-05
decision-makers:
consulted:
informed:
---

# Use Estuary Flow Private Deployment

## Context and Problem Statement

We want to move away from an [Estuary Flow Public Deployment](https://docs.estuary.dev/getting-started/deployment-options/#public-deployment) so that data and processing remains within our private network, offering improved protection.
Which deployment option should we choose?

## Considered Options

* [Private Deployment](https://docs.estuary.dev/getting-started/deployment-options/#private-deployment)
* [BYOC (Bring Your Own Cloud)](https://docs.estuary.dev/getting-started/deployment-options/#byoc-bring-your-own-cloud)

## Decision Outcome

Chosen option: "Private Deployment", because it offers the security and control of dedicated infrastructure while retaining the operational simplicity of a managed and immutable service.

## Pros and Cons of the Options

### Private Deployment

* Good **security**, because data and processing remains within our private network and dedicated (compute) data plane, offering improved protection, segmented from other tenants.
* Good **operational simplicity**, because we can do away with (explicit) SSH tunnelling over the internet thanks to private peering options.
* Good **immutable infrastructure**, because security and maintenance updates are seamlessly integrated by Estuary without disruption.
* Good **data movement**, because it allows for seamless data migration between regions.

### BYOC

With BYOC, we can deploy Estuary Flow directly within our own cloud environment.

* Good **security**, because data and processing remains within our private network and dedicated (compute) data plane, offering improved protection, away from other tenants.
* Good **operational simplicity**, because we can do away with (explicit) SSH tunnelling over the internet thanks to private peering options.
* Good **cost savings**, because of potential to reduce costs by using our existing cloud infrastructure and negotiated pricing.
* Bad **operational simplicity**, because our HPE GreenLake private cloud is not supported. Therefore, updates and maintenance are unavailable as a fully managed service.
