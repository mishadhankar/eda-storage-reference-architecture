# Project Roadmap

The EDA Storage Reference Architecture project is being developed incrementally.

The initial focus is on defining a repeatable methodology for evaluating semiconductor EDA storage and data architecture decisions. Later phases may introduce practical artifacts that assist infrastructure teams in applying the methodology.

## Phase 1 — Problem Definition and Workload Characterization

Status: In progress

Objectives:

- document the storage and data-management challenges associated with semiconductor EDA workloads;
- define workload characteristics relevant to infrastructure decisions;
- establish terminology for performance, data placement, lifecycle, security, and recovery requirements;
- identify representative architecture decision points.

Primary outputs:

- EDA infrastructure problem statement;
- workload characterization methodology;
- workload-profile structure;
- glossary and supporting references.

## Phase 2 — Vendor-Neutral Reference Architecture

Objectives:

- define reusable architecture patterns for semiconductor design environments;
- separate workload requirements from vendor-specific implementations;
- define relationships among compute, active storage, capacity storage, cloud resources, archive, and recovery infrastructure;
- document hybrid-cloud data placement principles.

Primary outputs:

- reference architecture documentation;
- data-placement decision patterns;
- hybrid-cloud architecture patterns;
- representative architecture diagrams.

## Phase 3 — Evaluation Methodology

Objectives:

- define how candidate architectures should be compared;
- develop evaluation criteria that reflect realistic EDA workload characteristics;
- incorporate concurrency, metadata behavior, workload phase, and compute proximity;
- establish a structured architecture decision process.

Primary outputs:

- evaluation methodology;
- workload-testing templates;
- architecture comparison worksheets;
- example evaluation criteria.

## Phase 4 — Technical-Economic Decision Framework

Objectives:

- evaluate infrastructure decisions across interconnected technical and economic dimensions;
- account for storage cost, compute utilization, data movement, operational complexity, and recovery requirements;
- distinguish workloads requiring premium infrastructure from workloads suited to capacity-optimized or lower-cost tiers.

Primary outputs:

- TCO decision framework;
- architecture decision matrix;
- economic sensitivity templates;
- example decision scenarios.

## Phase 5 — Cyber-Resilient Recovery Patterns

Objectives:

- integrate recovery requirements into architecture planning;
- classify design data by recovery priority and criticality;
- document patterns for protected recovery points, isolation, retention, and controlled restoration;
- define methods for testing recoverability.

Primary outputs:

- cyber-resilience architecture pattern;
- recovery-priority taxonomy;
- recovery validation checklist.

## Phase 6 — Practical Evaluation Artifacts

Potential future artifacts may include:

- workload-profile templates;
- machine-readable workload schemas;
- architecture evaluation worksheets;
- example datasets;
- lightweight analytical scripts;
- TCO calculators;
- decision-support models.

Software artifacts, where developed, will support the methodology rather than constitute the primary purpose of the project.

## Phase 7 — Validation and Community Development

Longer-term goals include:

- incorporating practitioner feedback;
- documenting representative non-confidential use cases;
- refining evaluation criteria based on technical review;
- publishing additional technical analysis;
- contributing findings to appropriate storage, cloud, semiconductor, or infrastructure forums.
