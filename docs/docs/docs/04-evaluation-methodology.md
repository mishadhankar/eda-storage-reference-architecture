# EDA Architecture Evaluation Methodology

## 1. Purpose

This document defines a repeatable methodology for evaluating candidate storage and data architectures for semiconductor Electronic Design Automation (EDA) workloads.

The objective is not to identify a universally "best" storage system.

The objective is to determine which architecture is most appropriate for a defined workload based on measurable technical, operational, economic, and recovery requirements.

The evaluation process begins with workload characteristics and then compares candidate architectures under conditions intended to represent the workload being supported.

## 2. Evaluation Principles

The methodology follows several principles.

### Workload Before Product

Candidate technologies should be evaluated against documented workload requirements rather than selected primarily from product specifications.

### Measure the Entire Workflow

Infrastructure should be evaluated using outcomes that matter to the workload, such as job completion time and productive compute utilization, rather than storage metrics alone.

### Test Representative Conditions

A test should reproduce important workload characteristics such as:

- file population;
- metadata activity;
- concurrency;
- read/write behavior;
- burst patterns;
- compute proximity; and
- data movement.

### Compare Like with Like

Candidate architectures should be tested using equivalent workload conditions whenever possible.

### Separate Measurement From Interpretation

Measured observations should be documented separately from analytical conclusions or recommendations.

### Evaluate Tradeoffs Together

Performance, compute utilization, data movement, infrastructure cost, operational complexity, and resilience should be considered together.

Improving one dimension may create additional cost or constraints elsewhere.

## 3. Inputs to the Evaluation

Each evaluation should begin with a workload profile produced using the methodology described in:

[`02-workload-characterization.md`](02-workload-characterization.md)

At minimum, the evaluation should identify:

- design stage or workload type;
- approximate file population;
- file-size distribution;
- metadata intensity;
- concurrency;
- I/O pattern;
- latency sensitivity;
- compute location;
- current data location;
- access frequency;
- security classification;
- lifecycle requirements; and
- recovery priority.

The evaluation should also state the problem being investigated.

Examples include:

- jobs are taking longer as concurrency increases;
- cloud compute is available but data remains on-premises;
- a project requires more predictable storage performance;
- existing infrastructure is approaching capacity limits;
- infrastructure cost is increasing faster than workload value; or
- recovery requirements are not adequately addressed by the existing architecture.

## 4. Define the Evaluation Objective

An evaluation should answer a specific decision question.

For example:

> Which architecture provides the best balance of job performance, productive compute utilization, data-movement requirements, cost, and recovery capability for a defined verification workload?

A good evaluation objective should identify:

1. the workload;
2. the architecture decision being considered;
3. the constraints; and
4. the outcomes that will determine success.

Avoid objectives such as:

> Which storage product is fastest?

That question is usually too narrow to support an infrastructure architecture decision.

## 5. Define Candidate Architectures

Each candidate architecture should be described functionally before comparing commercial implementations.

For example:

### Candidate A — High-Performance On-Premises

```text
EDA Compute
    ↓
High-performance shared storage
    ↓
Protected recovery copy
```

### Candidate B — Tiered On-Premises

```text
EDA Compute
    ↓
Performance tier
    ↓
Capacity tier
    ↓
Protected recovery copy
```

### Candidate C — Hybrid Cloud with Cache

```text
On-premises data
       ↓
Cache / staging layer
       ↓
Cloud EDA compute
       ↓
Results synchronized back
```

### Candidate D — Cloud-Native Working Dataset

```text
Cloud EDA compute
       ↓
Cloud performance storage
       ↓
Capacity / object tier
       ↓
Protected recovery copy
```

Actual commercial products can later be mapped to these functional patterns.

This separation helps prevent the evaluation from becoming vendor-specific before workload requirements are understood.

## 6. Establish Test Conditions

Candidate architectures should be evaluated under equivalent conditions wherever practical.

Document the following before testing:

| Test Condition | Description |
| --- | --- |
| Workload | EDA activity being evaluated |
| Dataset | Size and characteristics of test data |
| File count | Approximate number of files |
| File-size distribution | Small, medium, large, or mixed |
| Concurrency | Number of simultaneous jobs or workers |
| Compute configuration | Cores, instances, or nodes used |
| Storage configuration | Capacity and architecture |
| Network configuration | Relevant bandwidth and latency |
| Cache state | Warm, cold, or mixed |
| Test duration | Length of evaluation |
| Repetitions | Number of test runs |
| Data location | On-premises, cloud, hybrid |
| Recovery configuration | Protection used during evaluation |

Any material differences among candidates should be documented.

## 7. Representative EDA Test Scenarios

A complete evaluation may require more than one workload scenario.

### Scenario 1 — Metadata-Intensive Activity

Purpose:

Evaluate an architecture under workloads involving large file populations and frequent metadata operations.

Potential observations include:

- file-open latency;
- file creation rate;
- directory traversal behavior;
- metadata operations per second;
- job runtime; and
- behavior as concurrency increases.

### Scenario 2 — Highly Parallel Job Execution

Purpose:

Determine whether infrastructure performance remains stable as more compute workers access shared data.

Test at increasing concurrency levels such as:

```text
Low concurrency
      ↓
Moderate concurrency
      ↓
High concurrency
      ↓
Peak expected concurrency
```

Observe whether job completion time remains predictable as load increases.

### Scenario 3 — Large Data Transfer

Purpose:

Evaluate movement of substantial datasets between infrastructure locations or tiers.

Measure:

- transfer time;
- sustained throughput;
- network utilization;
- transfer cost where applicable; and
- time before compute can begin productive work.

### Scenario 4 — Hybrid-Cloud Execution

Purpose:

Evaluate workloads in which compute and primary data are located in different environments.

Compare possible approaches such as:

- direct remote access;
- caching;
- replication;
- pre-staging; or
- maintaining a persistent cloud working dataset.

Measure both data-movement time and workload execution time.

### Scenario 5 — Burst Workload

Purpose:

Evaluate infrastructure behavior during short periods of substantially increased demand.

Observe:

- time required to scale;
- performance stability;
- cache behavior;
- storage saturation;
- compute waiting; and
- recovery to normal operating conditions.

### Scenario 6 — Recovery

Purpose:

Evaluate whether critical project data can be restored within required operating objectives.

Measure:

- time to identify the required recovery point;
- time to make protected data available;
- restoration duration;
- validation time; and
- dependencies that delay workload restart.

## 8. Evaluation Metrics

Metrics should be grouped into several categories.

## 8.1 Workload-Level Metrics

These measure what the engineering workload experiences.

Examples:

- job completion time;
- jobs completed per hour;
- regression completion time;
- time to first useful result;
- failed or stalled jobs; and
- variability in job completion time.

These are often more meaningful than isolated infrastructure metrics.

## 8.2 Storage Metrics

Examples include:

- read latency;
- write latency;
- metadata latency;
- throughput;
- I/O operations per second;
- queue depth;
- cache hit rate; and
- storage utilization.

These metrics help explain workload-level results.

## 8.3 Compute Utilization Metrics

Examples include:

- productive compute utilization;
- idle compute time;
- CPU wait associated with data access;
- number of active workers;
- job queue duration; and
- compute-hours consumed per completed workload.

The purpose is to understand whether storage and data architecture are enabling effective use of expensive compute resources.

## 8.4 Data-Movement Metrics

Examples include:

- data transferred;
- transfer duration;
- network utilization;
- transfer frequency;
- synchronization duration;
- data-egress charges where applicable; and
- time between data movement and workload execution.

## 8.5 Economic Metrics

Examples include:

- storage cost;
- compute cost;
- data-transfer cost;
- capacity growth;
- infrastructure required for peak demand;
- operational effort; and
- cost per completed workload where it can be calculated reliably.

The detailed economic methodology is documented separately in:

[`05-tco-decision-framework.md`](05-tco-decision-framework.md)

## 8.6 Resilience Metrics

Examples include:

- recovery-point availability;
- recovery time;
- restoration success rate;
- isolation of protected data;
- frequency of recovery testing; and
- ability to restore workload dependencies in the required sequence.

## 9. Measure Scaling Behavior

Average performance alone may hide architecture limitations.

The evaluation should examine how results change as workload scale increases.

For example:

| Concurrency Level | Job Runtime | Storage Latency | Compute Utilization |
| --- | --- | --- | --- |
| Low | Measure | Measure | Measure |
| Medium | Measure | Measure | Measure |
| High | Measure | Measure | Measure |
| Peak | Measure | Measure | Measure |

The important question is not only:

> How fast is the architecture?

It is also:

> At what point does performance begin to degrade, and how does that degradation affect productive workload capacity?

## 10. Distinguish Bottleneck From Symptom

When a workload slows, storage should not automatically be assumed to be the cause.

Possible bottlenecks may include:

- compute saturation;
- memory constraints;
- storage latency;
- storage controller saturation;
- network congestion;
- scheduler behavior;
- application behavior;
- licensing limits; or
- data-placement inefficiency.

The evaluation should attempt to identify the limiting resource rather than attribute all delay to storage.

A useful diagnostic sequence is:

```text
Observe workload slowdown
        ↓
Check compute utilization
        ↓
Check storage latency and saturation
        ↓
Check network behavior
        ↓
Check scheduler / application behavior
        ↓
Identify likely limiting resource
        ↓
Validate by changing one variable where possible
```

## 11. Normalize Results

Results should be normalized where reasonable so that architectures can be compared fairly.

Possible normalized measures include:

```text
Cost per completed job

Compute-hours per completed workload

Storage capacity per active project

Data-transfer cost per workload

Recovery time per protected dataset
```

Normalized metrics are useful because the architecture with the lowest storage cost may not have the lowest total workload cost.

## 12. Evaluate Interdependent Tradeoffs

Evaluation should consider the interaction among metrics.

For example:

### Example A

Architecture A has:

- lower storage cost;
- longer job completion time; and
- higher compute consumption.

Architecture B has:

- higher storage cost;
- shorter job completion time; and
- lower compute consumption.

The appropriate decision depends on the total economic and operational effect rather than storage price alone.

### Example B

Architecture A provides very high performance but requires all data to remain on premium storage.

Architecture B keeps active data on a performance tier while moving inactive data to a lower-cost capacity tier.

Architecture B may produce a better overall outcome if the performance difference for active workloads is small relative to the capacity cost difference.

### Example C

Cloud compute may provide rapid additional capacity, but a workload may still perform poorly if required data must be transferred after the compute resources have already been provisioned.

Pre-staging or caching may therefore provide more value than simply increasing compute capacity.

## 13. Architecture Evaluation Matrix

A comparison can be documented using a matrix such as:

| Evaluation Dimension | Candidate A | Candidate B | Candidate C |
| --- | --- | --- | --- |
| Job completion time | Measure | Measure | Measure |
| Metadata performance | Measure | Measure | Measure |
| High-concurrency behavior | Measure | Measure | Measure |
| Productive compute utilization | Measure | Measure | Measure |
| Data-movement requirement | Measure | Measure | Measure |
| Storage cost | Estimate | Estimate | Estimate |
| Compute cost | Estimate | Estimate | Estimate |
| Operational complexity | Assess | Assess | Assess |
| Scalability | Assess | Assess | Assess |
| Recovery capability | Assess | Assess | Assess |
| Security requirements | Assess | Assess | Assess |

The methodology does not prescribe universal scoring weights.

Weights should reflect the requirements of the specific workload and organization.

For example, a tape-out-related workload may assign greater importance to performance, predictability, and recovery than an archival workload.

## 14. Decision Criteria

Before testing, the organization should identify minimum acceptable requirements.

Examples:

```text
Maximum acceptable job runtime

Maximum acceptable latency

Minimum required concurrency

Maximum data-staging time

Maximum infrastructure budget

Required recovery objective

Required data-retention period
```

Candidates that fail mandatory requirements may be eliminated even if they perform well in other categories.

## 15. Document Assumptions and Limitations

Every evaluation should document important limitations.

Examples include:

- synthetic workload rather than production workload;
- limited dataset size;
- short test duration;
- vendor-provided test environment;
- different hardware generations;
- cache effects;
- incomplete cost information; and
- inability to reproduce full production concurrency.

A limitation does not invalidate an evaluation.

It defines how broadly the results should be interpreted.

## 16. Separate Measured Results From Projections

Evaluation reports should distinguish clearly among:

### Measured

Observed directly during testing.

Example:

> Median job completion time was 42 minutes across five test runs.

### Calculated

Derived mathematically from measured inputs.

Example:

> The tested workload consumed 420 compute-hours.

### Estimated

Based on documented assumptions.

Example:

> Estimated annual infrastructure cost is based on the published unit price and expected utilization.

### Projected

An expected future result.

Example:

> If workload volume grows by 20%, projected capacity requirements would increase accordingly.

This distinction helps prevent estimated or projected results from being represented as measured outcomes.

## 17. Evaluation Output

A completed evaluation should produce the following artifacts:

1. **Workload profile**
2. **Evaluation objective**
3. **Candidate architecture descriptions**
4. **Test configuration**
5. **Raw observations**
6. **Normalized metrics**
7. **Tradeoff analysis**
8. **Assumptions and limitations**
9. **Architecture decision**
10. **Conditions that would trigger reevaluation**

## 18. Architecture Decision Record

The final decision can be documented using a simple structure:

```text
Decision:
Selected architecture pattern

Workload:
Workload being supported

Primary requirements:
Performance / concurrency / cost / recovery / etc.

Alternatives evaluated:
Candidate A
Candidate B
Candidate C

Key findings:
Summary of measured and calculated results

Tradeoffs:
Benefits and disadvantages of the selected approach

Decision rationale:
Why the selected architecture best matches the workload

Assumptions:
Important assumptions used in the evaluation

Reevaluation triggers:
Conditions that would require the architecture to be reconsidered
```

## 19. Continuous Reevaluation

EDA infrastructure requirements can change over time due to:

- increasing design complexity;
- higher compute scale;
- changing file populations;
- new EDA tools;
- cloud adoption;
- hardware-generation changes;
- storage technology changes;
- cost changes; and
- new security or recovery requirements.

An architecture decision should therefore be treated as valid for a defined workload and period rather than as a permanent universal answer.

The same evaluation process can be repeated when workload behavior or infrastructure economics materially change.

## 20. Relationship to the Broader Framework

This evaluation methodology connects the other components of the EDA Storage Reference Architecture project:

```text
Workload Characterization
        ↓
Reference Architecture
        ↓
Evaluation Methodology
        ↓
Technical-Economic Analysis
        ↓
Data Placement Decision
        ↓
Cyber-Resilient Recovery Requirements
        ↓
Architecture Decision
```

The objective is to make infrastructure decisions traceable from observed workload behavior through technical evaluation to the final architecture choice.
