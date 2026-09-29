# EDA Workload Characterization Methodology

## 1. Purpose

Infrastructure architecture should begin with the behavior of the workload rather than with a particular storage technology.

The purpose of workload characterization is to create a structured description of how a semiconductor design workload interacts with data.

That description can then be translated into performance, placement, lifecycle, security, and recovery requirements.

## 2. Workload Characterization Dimensions

The methodology evaluates a workload across several dimensions.

### 2.1 Design Stage

Identify the stage of the semiconductor design process.

Examples may include:

- RTL development;
- simulation;
- functional verification;
- regression testing;
- synthesis;
- physical design;
- design-rule checking;
- timing analysis;
- signoff;
- tape-out preparation; and
- post-design archival.

Different stages may have substantially different infrastructure characteristics.

### 2.2 File Population

Record:

- approximate number of files;
- typical file sizes;
- distribution of small and large files;
- directory depth;
- rate of file creation and deletion; and
- growth of the dataset over time.

Large-file throughput alone may not describe a workload containing millions of small files.

### 2.3 Metadata Activity

Measure or estimate operations such as:

- file lookup;
- open and close;
- create;
- delete;
- rename;
- directory traversal;
- permission checks; and
- attribute queries.

Metadata behavior can materially affect workloads that repeatedly access large file populations.

### 2.4 Concurrency

Characterize:

- number of simultaneous jobs;
- number of compute cores accessing shared data;
- number of users;
- degree of parallel file access; and
- peak versus typical concurrency.

Infrastructure that performs well at low concurrency may behave differently when thousands of operations occur simultaneously.

### 2.5 I/O Pattern

Identify:

- sequential versus random access;
- read/write ratio;
- temporary versus persistent writes;
- repeated access to shared files;
- checkpoint behavior;
- burst periods; and
- sustained versus intermittent activity.

### 2.6 Latency Sensitivity

Classify the degree to which delays in data access affect job completion.

A simple classification can be:

```text
High
Medium
Low
```

Latency sensitivity should be considered together with workload concurrency.

### 2.7 Compute Proximity

Identify where computing resources run relative to the data.

Examples include:

- same on-premises environment;
- different on-premises site;
- same cloud region;
- different cloud region;
- cloud compute accessing on-premises data; or
- hybrid execution across multiple locations.

Distance between data and compute can affect both performance and data-movement cost.

### 2.8 Access Frequency

Classify data as:

- continuously active;
- frequently accessed;
- periodically accessed;
- rarely accessed; or
- archival.

Access frequency can help determine whether data belongs on high-performance infrastructure, capacity-oriented storage, object storage, or archive.

### 2.9 Reuse Value

Some datasets are repeatedly reused across projects.

Examples may include:

- design libraries;
- intellectual-property blocks;
- technology files;
- reusable verification environments; and
- reference datasets.

High-reuse data may justify different placement and protection decisions from temporary output.

### 2.10 Security Sensitivity

Classify data according to sensitivity.

Possible categories include:

```text
Routine engineering data
Internal project data
Sensitive design intellectual property
Critical release or tape-out artifacts
```

Actual classifications should follow the organization's security policies.

### 2.11 Recovery Priority

Identify:

- how quickly data must be restored;
- acceptable data-loss interval;
- dependency relationships;
- which datasets must be restored first; and
- whether restoration requires additional validation or approval.

Recovery priority should be determined before an incident occurs.

### 2.12 Lifecycle

Determine how workload requirements change over time.

A dataset may move through stages such as:

```text
Active
  ↓
Reference
  ↓
Inactive
  ↓
Archive
```

The appropriate infrastructure may change as the dataset moves through its lifecycle.

## 3. Example Workload Profile

A workload profile may use a structure such as:

| Characteristic | Example |
| --- | --- |
| Design stage | Verification |
| File population | Very high |
| Metadata activity | High |
| Concurrency | Very high |
| Read/write pattern | Mixed |
| Latency sensitivity | High |
| Compute location | Cloud |
| Primary data location | On-premises |
| Access frequency | High |
| Reuse value | Medium |
| Security sensitivity | High |
| Recovery priority | High |

This table is illustrative.

Actual profiles should be based on measured or observed workload behavior.

## 4. From Characterization to Requirements

Workload characteristics should be translated into infrastructure requirements.

For example:

```text
High metadata activity
        ↓
Need strong metadata performance

High concurrency
        ↓
Need scalable parallel access

Cloud compute + on-premises data
        ↓
Evaluate caching, replication, or pre-staging

Low-access historical data
        ↓
Evaluate lower-cost capacity or archive tier

High recovery priority
        ↓
Protected recovery copy + tested restoration
```

The methodology intentionally separates **workload requirements** from **vendor selection**.

Vendor or product evaluation occurs only after the requirements are understood.

## 5. Telemetry and Evidence

Where available, characterization should rely on measured information rather than assumptions.

Possible evidence includes:

- file-system telemetry;
- storage performance metrics;
- scheduler records;
- job-runtime histories;
- application logs;
- cloud monitoring;
- network transfer statistics;
- capacity trends;
- recovery history; and
- interviews with infrastructure and engineering teams.

No single metric should be treated as sufficient to describe the workload.

## 6. Role of AI-Assisted Classification

Where sufficient historical data exists, machine-learning or AI-assisted techniques may help identify recurring workload patterns.

Potential uses include:

- identifying recurring workload classes;
- detecting changes in access behavior;
- classifying data by access frequency;
- identifying likely burst periods;
- recommending candidate placement policies; and
- highlighting workloads whose behavior differs from historical patterns.

AI-assisted recommendations should remain explainable and subject to human validation.

AI is therefore a supporting technique within the methodology rather than a substitute for workload measurement or engineering judgment.

## 7. Output

The output of this stage is a structured workload profile that can be used as input to:

- architecture selection;
- data-placement decisions;
- benchmark design;
- TCO analysis;
- cloud-burst planning; and
- recovery architecture.
