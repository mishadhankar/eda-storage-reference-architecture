# EDA Storage Reference Architecture

**A vendor-neutral reference architecture and evaluation methodology for storage infrastructure supporting semiconductor Electronic Design Automation (EDA) workloads.**

---

## About this project

This repository is the working home of the **Semiconductor Design Storage Acceleration Platform (SDSAP)** — an ongoing effort to produce a vendor-neutral technical architecture and evaluation methodology addressing a documented infrastructure constraint in United States semiconductor design environments: storage architecture and data-management performance can materially affect Electronic Design Automation (EDA) job throughput, workflow turnaround time, and the productivity of the semiconductor engineering workforce.

The project produces **technical documentation and evaluation methodology**, not a software product. Its outputs are analogous in kind to industry-recognized architectural frameworks such as the AWS Well-Architected Framework, the Storage Networking Industry Association (SNIA) reference architectures, and the National Institute of Standards and Technology (NIST) reference architectures. Software code may be used as an illustrative or supporting tool where appropriate, but software development is not the objective.

---

## Personal capacity notice

This is a personal project maintained by Misha Dhankar in an individual capacity. It is not affiliated with, endorsed by, or produced by any current or former employer. Views expressed here are the author's own. The reference architecture and evaluation methodology are intentionally vendor-neutral and are designed to be usable by semiconductor design organizations regardless of storage vendor, cloud provider, or on-premises versus hybrid deployment choice.

---

## The problem this project addresses

Modern semiconductor design workloads have distinctive characteristics that generic enterprise storage architectures are not optimized for:

- Highly concurrent, small-file-heavy workflows spanning many parallel processes
- Metadata-intensive operations (approximately 60% of the configured operation mix in the standardized SPEC EDA front-end benchmark is metadata-oriented rather than file-data reads and writes)
- Petabyte-scale data volumes with heterogeneous data classes (active verification data, reusable design libraries, sensitive intellectual property blocks, tape-out artifacts, archived project directories)
- Bursty, deadline-driven access patterns tied to tape-out cycles, regression campaigns, and design signoff milestones
- Strict cyber-resilience requirements for high-value semiconductor design intellectual property

The storage bottleneck in EDA workflows is independently documented by:

- The **Standard Performance Evaluation Corporation (SPEC)**, in the SPECstorage Solution 2020 benchmark documentation
- **Dell Technologies**, in its 2025 technical article on the limitations of existing commercial EDA storage benchmarks
- **Google Cloud**, in its published EDA storage documentation
- **Pure Storage**, in its published EDA workload testing
- **NetApp**, in Technical Report TR-4944 on EDA workloads
- **Amazon Web Services**, in its published guidance for scaling EDA on cloud infrastructure
- Independent semiconductor industry publications

Even so, existing commercial EDA storage benchmarks are incomplete. Dell publicly acknowledges that current benchmarks fail to capture the twenty to thirty individual EDA tools used in modern designs, front-end versus back-end workload differences, production-scale testing conditions, and modern job scheduler effects. This gap creates the space this project aims to fill.

---

## What this repository contains

SDSAP is organized around **five components**, each addressed in a dedicated document under [`/docs`](./docs):

1. **[Workload Characterization](./docs/02-workload-characterization.md)** — how semiconductor EDA workloads exercise storage: workflow phases, data classes, access patterns, and the resulting workload taxonomy.
2. **[Reference Architecture](./docs/03-reference-architecture.md)** — a vendor-neutral technical architecture describing the component layers, data flow, and deployment options across on-premises, cloud, and hybrid environments.
3. **[Evaluation Methodology](./docs/04-evaluation-methodology.md)** — an extended methodology addressing gaps in existing commercial EDA storage benchmarks, covering AI-enhanced EDA workflows, hybrid-cloud data staging, cyber-resilient recovery workflows, and workload behavior at emerging process nodes.
4. **[TCO Decision Framework](./docs/05-tco-decision-framework.md)** — an analytical framework for evaluating on-premises, cloud, and hybrid economics for semiconductor storage infrastructure over multi-year horizons.
5. **[Cyber-Resilience Pattern](./docs/06-cyber-resilience-pattern.md)** — a vendor-neutral architectural pattern for protecting high-value semiconductor design intellectual property, aligned with the cybersecurity principles reflected in the draft NIST Internal Report 8546 (Cybersecurity Framework 2.0 Semiconductor Manufacturing Profile, Initial Public Draft).

Supporting materials:

- **[Problem Statement](./docs/01-problem-statement.md)** — a detailed articulation of the documented industry problem this project addresses
- **[Roadmap](./ROADMAP.md)** — the twelve-to-twenty-four-month execution plan, including future working artifacts (extended evaluation tooling, additional technical publications, standards contributions, and conference presentations)
- **[References](./docs/references.md)** — bibliography of cited public sources
- **[White Papers](./whitepapers/)** — technical writing addressing specific aspects of the endeavor

---

## Guiding principles

Four principles govern this work:

1. **Vendor-neutral by design.** Every technical output is written to be usable across storage vendors (NetApp, Pure Storage, Dell, WEKA, VAST, and others), cloud providers (Amazon Web Services, Microsoft Azure, Google Cloud, and others), and deployment models (on-premises, cloud, hybrid). No single vendor is preferentially positioned.

2. **Grounded in independent, publicly citable evidence.** Every substantive claim in this repository is anchored to public sources documented in the references file. Where quantitative results are drawn from vendor-published testing, they are presented as mechanism-level evidence that storage architecture can materially affect EDA workflow characteristics, not as predictions of what this project will produce.

3. **Written for practitioners.** The intended audience is semiconductor infrastructure architects, storage engineers, and technical decision-makers responsible for architecting semiconductor design environments. The documents are technical guidance, not marketing.

4. **Iterative and honestly scoped.** This is an initial release. The [roadmap](./ROADMAP.md) identifies specific future artifacts, and the state of each document reflects its current maturity. Signaling honest scope is preferred over overstating completeness.

---

## Roadmap summary

The full roadmap is in [ROADMAP.md](./ROADMAP.md). At a summary level, the twelve-to-twenty-four-month plan includes:

- Continued refinement of the reference architecture and evaluation methodology based on practitioner feedback
- Expansion of the evaluation framework into working analytical tooling and public benchmarking guidance
- Technical publications on industry platforms including IEEE Computer Society and the SNIA whitepaper series
- Conference presentations at industry venues including AWS re:Invent, the Design Automation Conference (DAC), and Flash Memory Summit
- Participation in the Institute of Electrical and Electronics Engineers (IEEE) Standards Association through storage-relevant working groups

---

## Contributing

Feedback, corrections, and technical discussion are welcome through GitHub Issues on this repository. See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidance on how to file substantive technical feedback.

Contributions of vendor-specific implementation guidance are not accepted; the intent is to keep the reference architecture and methodology vendor-neutral. Contributions that improve the accuracy of the workload characterization, the completeness of the evaluation methodology, or the quality of the analytical frameworks are welcome.

---

## License

This project is licensed under the Apache License 2.0. See [LICENSE](./LICENSE) for details.

---

## About the author

**Misha Dhankar** is a senior technical product manager focused on infrastructure and storage strategy for semiconductor and high-performance computing workloads. Prior to her current role, she led product strategy for enterprise all-flash and hybrid-flash storage product lines at NetApp, including the AFF C-Series, and contributed to NetApp's logically air-gapped cyber-vault reference architecture. She holds an MBA from the Foster School of Business at the University of Washington and an integrated Master of Technology in Biotechnology from Amity University.

She is a member of the Institute of Electrical and Electronics Engineers (IEEE) Standards Association and is developing this reference architecture and evaluation methodology in her individual capacity to make semiconductor storage architecture decisions more evaluable, more vendor-neutral, and more accessible across the United States semiconductor design ecosystem.

---

*Repository initialized: [publication date]. This is an initial release. See [ROADMAP.md](./ROADMAP.md) for planned refinements and future artifacts.*
