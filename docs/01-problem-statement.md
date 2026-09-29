# The EDA Storage and Data Infrastructure Problem

## 1. Introduction

Semiconductor chips are designed and validated through Electronic Design Automation (EDA) workflows before they are manufactured.

These workflows include activities such as simulation, verification, physical design, regression testing, signoff, and tape-out preparation.

Modern EDA environments can operate across very large pools of computing resources while repeatedly creating, reading, modifying, and deleting substantial numbers of engineering files.

In these environments, computing performance depends not only on the availability of processors but also on whether the required design data can be accessed at the speed, location, and concurrency required by the workload.

Storage and data architecture can therefore become a limiting factor in semiconductor design productivity.

## 2. Why EDA Workloads Are Different

EDA workloads can place unusual demands on storage infrastructure.

Representative characteristics include:

- very large numbers of files;
- frequent file-system metadata operations;
- highly parallel access;
- mixed file sizes;
- bursty demand during verification or regression activity;
- different workload behavior across design stages;
- shared access to common design libraries;
- substantial temporary and intermediate data;
- valuable intellectual property requiring strong protection; and
- large-scale compute environments accessing shared project data.

These characteristics mean that storage requirements cannot always be summarized by a single throughput or latency number.

A system that performs well for one stage of semiconductor design may perform differently for another stage.

## 3. Storage Can Limit Productive Compute Capacity

In a highly parallel design environment, additional processors provide value only when they can obtain the files and metadata required to perform their work.

If the data infrastructure cannot keep pace with the workload, computing resources may remain technically available while performing less productive work because jobs are waiting for data access.

For this reason, semiconductor infrastructure performance should be considered as a system involving:

```text
Compute
   +
Storage
   +
Data placement
   +
Network and data movement
   +
EDA workload behavior
