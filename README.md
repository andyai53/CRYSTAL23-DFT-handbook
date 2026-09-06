# CRYSTAL23 workflows for periodic materials

_A practical onboarding guide for reproducible computational research with CRYSTAL23._

---

This handbook is for a student who is new to Linux, HPC and periodic DFT. It follows one complete workflow: prepare a calculation, submit it through PBS, check that it converged, and then analyse properties such as BAND, DOSS and ANBD.

It complements the [official CRYSTAL properties tutorial][crystal-properties]. Use that tutorial when you need the exact keyword syntax. Use this handbook when you need to decide what to run, how to check it, how to inspect a plot and how to leave a calculation that someone else can reproduce.[^1]

## 📚 Start here

Choose the route that matches your goal:

| Goal | Start with | Outcome |
| --- | --- | --- |
| I have never used a cluster | [Before you run anything](docs/00-before-you-run.md) | Build the right mental model before running code |
| I need to submit a job | [Linux and PBS essentials](docs/01-linux-and-pbs.md) | Submit, monitor and inspect a first job |
| I want to run BAND or DOS | [Properties overview](docs/07-properties-overview.md) | Start from a trusted wavefunction and keep the analysis traceable |
| I am taking over an existing project | Project organisation *(under construction)* | Trace every figure back to its input and output |

## 🧭 The learning path

```mermaid
flowchart LR
    accTitle: CRYSTAL23 Learning Path
    accDescr: The handbook moves from basic cluster operation through validated electronic-structure calculations and finally to reproducible research outputs.

    start([Start here]) --> linux[Linux and PBS]
    linux --> first[First CRYSTAL23 job]
    first --> check{Did it converge?}
    check -->|No| diagnose[Diagnose and recover]
    diagnose --> first
    check -->|Yes| optimise[Geometry optimisation]
    optimise --> validate[Validate the structure]
    validate --> properties[Properties: BAND, DOSS, ANBD]
    properties --> record[Record and hand over]

    classDef primary fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#1e3a5f
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#14532d
    classDef warning fill:#fef9c3,stroke:#ca8a04,stroke-width:2px,color:#713f12

    class linux,first,optimise,properties primary
    class validate,record success
    class check,diagnose warning
```

## 🎯 What this handbook teaches

- How to distinguish a submitted job from a scientifically usable result
- How SCF convergence and geometry convergence are different checks
- How to organise inputs, outputs, wavefunctions and figures
- How to run properties only from a validated converged calculation
- How to make a reasoned choice about basis sets, k-points, smearing and slab thickness
- How to leave a calculation that another student can reproduce

## 🔒 Scope and safety

This handbook uses generic PBS examples. Resource names, module names, executable paths and wall-time limits are site-specific. Replace marked placeholders with values from your local HPC service. Never publish credentials, private paths, unpublished structures or raw data without your supervisor's approval.

The examples teach a workflow, not a universal production protocol. A successful command is not evidence that a model is physically adequate. Keep the input, output, convergence evidence and scientific reason for each choice together.

## 🗂️ Repository map

The entries below are clickable. GitHub does not make Markdown links inside a fenced `text` code block clickable, so the repository map is written as a nested list instead:

- [`README.md`](./README.md) — project entry page
- [`docs/`](./docs/) — step-by-step tutorials
  - [`00-before-you-run.md`](./docs/00-before-you-run.md)
  - [`01-linux-and-pbs.md`](./docs/01-linux-and-pbs.md)
  - [`02-first-crystal23-job.md`](./docs/02-first-crystal23-job.md)
  - [`03-reading-input-and-output.md`](./docs/03-reading-input-and-output.md)
  - [`04-scf-convergence.md`](./docs/04-scf-convergence.md)
  - [`05-geometry-optimisation.md`](./docs/05-geometry-optimisation.md)
  - [`06-convergence-as-evidence.md`](./docs/06-convergence-as-evidence.md)
  - [`07-properties-overview.md`](./docs/07-properties-overview.md)
  - [`08-band-structure.md`](./docs/08-band-structure.md)
  - [`09-density-of-states.md`](./docs/09-density-of-states.md)
  - [`index.md`](./docs/index.md) — GitHub Pages entry page

Planned directories such as `examples/`, `templates/` and `references/` will be added after their contents are validated. They are intentionally not linked yet, so the map does not point to empty or nonexistent paths.

Later modules will cover bonding analysis, bulk and slab workflows, the surface case study, project management and troubleshooting. They will be added with tested examples rather than empty placeholder pages.

## 📖 Official references

Use the [CRYSTAL properties tutorial][crystal-properties] for the detailed syntax of PPAN, ECHG, BAND, DOSS, COOP and COHP. Use [CrySPLOT][crysplot] to inspect or plot supported CRYSTAL output files. For a citable overview of the code and its development, see Dovesi et al.[^2]

[crystal-properties]: https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut
[crysplot]: https://crysplot.crystalsolutions.eu/index.html

[^1]: CRYSTAL Solutions. (n.d.). *Properties tutorial*. https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut
[^2]: Dovesi, R., Erba, A., Orlando, R., et al. (2020). *The CRYSTAL code, 1976–2020 and beyond: a long story*. The Journal of Chemical Physics, 152, 204111. https://doi.org/10.1063/5.0004892
