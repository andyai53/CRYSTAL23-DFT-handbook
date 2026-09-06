# Convergence as evidence

_Estimated time: 45 minutes | Difficulty: Intermediate | Last verified: 2026-09-05_

---

A convergence test is a controlled comparison. Change one numerical or modelling parameter at a time, measure a quantity relevant to your question and record the extra cost.

## 🎯 Learning goals

- Design a one-parameter-at-a-time convergence test
- Separate numerical convergence from model validation
- Compare accuracy, stability and computational cost
- Turn a group of runs into a traceable decision

## 🧪 The controlled comparison

```mermaid
flowchart LR
    accTitle: Convergence Test Workflow
    accDescr: A convergence study defines an observable, varies one parameter across several runs, extracts comparable values and selects a setting using both accuracy and cost.

    question[Define the observable] --> baseline[Choose a baseline]
    baseline --> vary[Vary one parameter]
    vary --> run[Run comparable calculations]
    run --> extract[Extract the same quantity]
    extract --> compare[Compare change and cost]
    compare --> decide{Stable enough for the question?}
    decide -->|No| vary
    decide -->|Yes| record[Record the decision]

    classDef primary fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#1e3a5f
    classDef decision fill:#fef9c3,stroke:#ca8a04,stroke-width:2px,color:#713f12
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#14532d

    class question,baseline,vary,run,extract,compare primary
    class decide decision
    class record success
```

## 📊 What to test

| Parameter | Example levels | Observable to compare |
| --- | --- | --- |
| Basis set | A small-to-larger sequence | Lattice parameter, bond length, energy difference |
| k-point sampling | Coarse-to-denser meshes | Total energy, Fermi-level states, band dispersion |
| SCF threshold | Moderate-to-tighter `TOLDEE` | Energy difference and property stability |
| Slab thickness | Increasing layer counts | Centre-layer structure and surface energy/property |
| Smearing or mixing | Several documented values | SCF stability and final electronic result |

Choose levels that suit the model. Keep the functional, basis, geometry, charge and k-point path fixed unless you are explicitly comparing methods.

## 🧮 Use a decision table

| Run | One changed parameter | Observable | Difference from previous run | Cost | Decision |
| --- | --- | --- | ---: | ---: | --- |
| 01 | Baseline | [value] | - | [time] | Reference |
| 02 | [parameter = level 2] | [value] | [delta] | [time] | Keep or continue |
| 03 | [parameter = level 3] | [value] | [delta] | [time] | Accept or reject |

"Converged" means stable for the selected observable and tolerance. It does not mean that every property is insensitive to the same setting. State what you tested and what you did not test.

## 📝 Calculation passport entry

For each accepted setting, keep a short note in `notes/calculation-passport.md`:

```text
Question: [what this calculation supports]
Observable: [quantity used for the convergence decision]
Parameter varied: [one parameter]
Levels tested: [list]
Acceptance criterion: [numerical criterion and reason]
Selected level: [value]
Evidence: [input/output/plot paths]
Known limitation: [what was not tested]
```

This note lets another student reproduce the comparison and understand why you selected the production setting.

## 🚀 Next step

Continue to [Properties overview](07-properties-overview.md) once the parent SCF and geometry settings are validated.
