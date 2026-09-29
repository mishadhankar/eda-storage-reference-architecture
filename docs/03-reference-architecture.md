# Vendor-Neutral EDA Storage Reference Architecture

## 1. Purpose

This document describes a vendor-neutral architecture pattern for semiconductor Electronic Design Automation (EDA) environments.

The architecture is not intended to prescribe a particular storage system or cloud provider.

Instead, it defines functional infrastructure layers that can be implemented using different technologies depending on workload requirements.

## 2. Architecture Principles

The reference architecture follows several principles.

### Workload First

Architecture decisions should begin with measured or observed workload requirements.

### Data Near Compute When Necessary

Latency-sensitive workloads should have efficient access to the data required for execution.

### Different Data Requires Different Infrastructure

Active design data, reusable libraries, temporary outputs, historical projects, and recovery copies should not automatically use the same storage tier.

### Placement Is Dynamic

The appropriate location of data can change over the semiconductor design lifecycle.

### Performance and Cost Must Be Evaluated Together

Higher performance can reduce job runtime and improve compute utilization, but premium infrastructure should be used where workload behavior justifies it.

### Recovery Is Part of Architecture

Protection and recovery requirements should be considered during architecture design rather than after deployment.

## 3. Logical Architecture

A generalized architecture can be represented as:

```text
                    ┌─────────────────────────┐
                    │    EDA Compute Layer    │
                    │ simulation / verification│
                    │ physical design / etc.  │
                    └────────────┬────────────┘
                                 │
                      workload data access
                                 │
              ┌──────────────────▼──────────────────┐
              │   Active / Performance Data Layer  │
              │   latency-sensitive working data   │
              └──────────────────┬──────────────────┘
                                 │
                    lifecycle / placement policy
                                 │
              ┌──────────────────▼──────────────────┐
              │      Capacity / Shared Data Layer   │
              │    reusable and less-active data    │
              └─────────────┬───────────────┬────────┘
                            │               │
                     cloud mobility      lifecycle
                            │               │
                   ┌────────▼────────┐ ┌────▼───────────┐
                   │ Cloud / Hybrid │ │ Archive Layer  │
                   │   Data Layer   │ │ historical data│
                   └────────┬────────┘ └────────────────┘
                            │
                       protected copy
                            │
                   ┌────────▼───────────┐
                   │ Recovery / Cyber- │
                   │ Resilience Layer  │
                   └────────────────────┘
```

The specific implementation may combine or separate these functions depending on scale and operational requirements.

## 4. Compute Layer

The compute layer executes EDA workloads.

It may consist of:

- on-premises compute clusters;
- public-cloud compute;
- high-performance computing environments; or
- hybrid combinations.

Architecture decisions should consider:

- compute scale;
- job concurrency;
- burst demand;
- scheduler behavior;
- compute generation;
- regional availability; and
- data-access requirements.

The compute layer should not be evaluated independently of data location.

## 5. Active / Performance Data Layer

This layer supports workloads requiring frequent or latency-sensitive access.

Representative data may include:

- active project directories;
- current verification data;
- design libraries in active use;
- physical-design databases; and
- frequently accessed intermediate artifacts.

Important characteristics may include:

- low latency;
- high metadata performance;
- scalable concurrency;
- predictable performance; and
- close proximity to compute.

Not all project data needs to remain in this layer.

## 6. Capacity / Shared Data Layer

This layer supports data that remains useful but does not always require the highest-performance infrastructure.

Possible workloads include:

- shared engineering data;
- older project stages;
- reusable reference datasets;
- less-active design assets;
- backup staging data; and
- large capacity-oriented datasets.

The purpose of this layer is to balance accessibility with infrastructure economics.

## 7. Cloud / Hybrid Data Layer

This layer supports workloads in which compute and data may exist in different infrastructure environments.

Possible functions include:

- cloud bursting;
- temporary replication;
- caching near compute;
- dataset pre-staging;
- cross-region data placement; and
- controlled synchronization.

A hybrid architecture should answer:

1. What data needs to move?
2. When does it need to move?
3. How long will it remain near the compute environment?
4. What is the transfer cost?
5. What is the performance impact?
6. What happens to modified data after the workload completes?

These decisions should be made per workload rather than through a universal placement rule.

## 8. Archive Layer

Historical semiconductor project data may remain valuable for:

- regulatory or organizational retention;
- previous product support;
- derivative designs;
- troubleshooting;
- intellectual-property reuse; or
- future analysis.

Archive infrastructure should prioritize:

- cost efficiency;
- retention requirements;
- integrity;
- discoverability; and
- predictable restoration.

Archive data generally should not consume the same infrastructure resources as active design data unless business requirements justify it.

## 9. Recovery / Cyber-Resilience Layer

Critical semiconductor engineering data should have protected recovery mechanisms appropriate to its business value.

Potential architecture characteristics include:

- protected recovery points;
- immutable retention where appropriate;
- logical or administrative isolation;
- restricted recovery access;
- prioritized restoration;
- recovery testing; and
- documented recovery dependencies.

Recovery requirements should be derived from workload criticality.

## 10. Data Placement Decision

A simplified placement process is:

```text
Is the data latency-sensitive?
        │
        ├── Yes → Evaluate active / performance tier
        │
        └── No
             │
             ▼
Is it frequently accessed or reused?
        │
        ├── Yes → Evaluate shared / capacity tier
        │
        └── No
             │
             ▼
Does it require long-term retention?
        │
        ├── Yes → Evaluate archive tier
        │
        └── No → Evaluate deletion / expiration policy
```

Additional questions apply independently:

```text
Does cloud compute require the data?
        ↓
Evaluate caching / replication / pre-staging

Is the data business-critical?
        ↓
Define protected recovery requirements

Is the data highly sensitive?
        ↓
Apply appropriate security and access controls
```

## 11. Architecture Evaluation

No architecture should be selected solely because it achieves the highest individual benchmark result.

Candidate designs should be evaluated across:

- job completion time;
- metadata performance;
- concurrency;
- compute utilization;
- data-movement requirements;
- infrastructure cost;
- operational complexity;
- scalability;
- security; and
- recovery.

The detailed evaluation process will be documented in `04-evaluation-methodology.md`.

## 12. Vendor Mapping

Future versions may document how publicly available commercial technologies map to these functional architecture layers.

Such mapping will be descriptive rather than prescriptive and will not imply endorsement of any vendor.
