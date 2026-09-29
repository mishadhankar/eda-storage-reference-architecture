
Notice that here I used **“hypothetical 100,000-core environment.”** That is more appropriate for an open technical repository than making it sound like a project performance claim.

Later, in `references.md`, we will cite NetApp, SPEC, Dell, Pure, etc.

---

# 7. `docs/02-workload-characterization.md`

Use:

```markdown
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
- open/close;
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
