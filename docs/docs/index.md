---
layout: default
title: CRYSTAL23 workflows
---

# CRYSTAL23 workflows for periodic materials

_A practical onboarding guide for reproducible computational research._

---

This site is for students learning CRYSTAL23, Linux/HPC operation and the checks needed to turn a calculation into defensible evidence.

## 📚 Choose a starting point

| I want to... | Read this |
| --- | --- |
| Understand the workflow | [Before you run anything](00-before-you-run.md) |
| Learn the cluster commands | [Linux and PBS essentials](01-linux-and-pbs.md) |
| Submit a first calculation | [Your first CRYSTAL23 job](02-first-crystal23-job.md) |
| Read a CRYSTAL input or output | [Reading input and output](03-reading-input-and-output.md) |
| Recover a difficult SCF run | [SCF convergence](04-scf-convergence.md) |
| Validate a relaxed structure | [Geometry optimisation](05-geometry-optimisation.md) |
| Design a convergence study | [Convergence as evidence](06-convergence-as-evidence.md) |
| Run electronic properties | [Properties overview](07-properties-overview.md) |
| Inspect a band structure | [Band structure](08-band-structure.md) |
| Interpret total or projected DOS | [Density of states](09-density-of-states.md) |

## 🧭 Recommended order

`00` -> `01` -> `02` -> `03` -> `04` -> `05` -> `06` -> `07` -> `08` -> `09`

The pages that need local examples will be completed with validated inputs from the target cluster. Until then, use the [official CRYSTAL properties tutorial](https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut) for exact keyword syntax and [CrySPLOT](https://crysplot.crystalsolutions.eu/index.html) when you need to inspect supported output files visually. The CRYSTAL code and its scope are described by [Dovesi et al. (2020)](https://doi.org/10.1063/5.0004892).

Before connecting from outside Imperial, follow the [Imperial Unified Access guide](https://www.imperial.ac.uk/admin-services/ict/self-service/connect-communicate/remote-access/unified-access/). When choosing a basis, consult the [CRYSTAL Basis Sets Library](https://www.crystal.unito.it/basis_sets.html) and record the exact basis used in the input.
