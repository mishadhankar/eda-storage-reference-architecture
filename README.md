# EDA Storage Reference Architecture

A vendor-neutral technical project for evaluating storage, data placement, hybrid-cloud architecture, cost, and cyber-resilient recovery for semiconductor Electronic Design Automation (EDA) environments.

## Overview

Modern semiconductor design depends on highly parallel Electronic Design Automation (EDA) workloads that create, read, modify, and move large numbers of engineering files across substantial computing environments.

Storage and data infrastructure can materially affect the performance of these workloads. Adding computing capacity alone does not necessarily improve design throughput when computing resources are waiting for the data required to perform their work.

At the same time, semiconductor infrastructure teams must make decisions involving more than storage performance alone. They must determine:

- where design data should reside;
- how closely data should be positioned to computing resources;
- when data should be cached or moved in advance of a workload;
- how different classes of design data should be stored;
- how candidate architectures should be evaluated under realistic workload conditions;
- how infrastructure cost should be weighed against compute utilization and engineering productivity; and
- how critical engineering data should be protected and recovered following a disruption.

These decisions are interdependent. A storage option with a lower acquisition cost may increase job runtime or consume additional computing and EDA-software capacity. Conversely, using maximum-performance infrastructure for every dataset may create unnecessary cost where that level of performance is not required.

The purpose of this project is to develop a repeatable methodology for evaluating these tradeoffs together.

## Project Objective

The project develops vendor-neutral methodologies and reference architecture patterns for semiconductor design and EDA infrastructure.

The work focuses on five questions:

1. **How does the workload behave?**  
   Characterize file activity, metadata intensity, concurrency, latency sensitivity, data lifecycle, compute proximity, security sensitivity, and recovery requirements.

2. **Where should data reside?**  
   Evaluate on-premises, cloud, hybrid, caching, tiering, and pre-staging approaches based on workload requirements.

3. **How should candidate architectures be evaluated?**  
   Use workload-relevant testing criteria rather than relying solely on isolated performance specifications.

4. **What is the overall technical and economic tradeoff?**  
   Evaluate storage performance, compute utilization, data movement, infrastructure cost, operational complexity, and recovery together.

5. **How should critical semiconductor design data be protected?**  
   Incorporate cyber-resilient recovery, protected recovery points, isolation, recovery prioritization, and controlled restoration into architecture planning.

## Why EDA Requires Workload-Specific Evaluation

Semiconductor design is not a single uniform workload.

Different stages of design and verification can have significantly different characteristics. Some activities involve large numbers of small files and metadata operations. Others involve larger sequential transfers, highly parallel access, temporary simulation outputs, reusable design libraries, or data that must remain protected for long periods.

A useful infrastructure architecture therefore begins with workload behavior rather than with a particular storage product.

This project develops methods for translating those workload characteristics into infrastructure requirements and architecture decisions.

## Architecture Decision Flow

The project uses the following high-level decision process:

```text
Characterize workload behavior
        ↓
Define performance, placement, lifecycle, security,
and recovery requirements
        ↓
Identify candidate architecture patterns
        ↓
Evaluate candidates under representative EDA conditions
        ↓
Compare performance, compute utilization, data movement,
cost, operational complexity, and resilience
        ↓
Document the architecture decision
