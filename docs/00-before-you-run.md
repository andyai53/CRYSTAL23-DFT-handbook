# Before you run anything

_Estimated time: 20 minutes | Difficulty: Beginner | Last verified: 2026-09-05_

---

This page gives you the mental model needed to follow the rest of the handbook. You do not need to understand every keyword yet. You do need to know which files are inputs, which files are evidence, and what "finished" means.

## 🎯 Learning goals

By the end of this page, you should be able to:

- explain what a periodic DFT calculation is trying to solve;
- distinguish SCF convergence from geometry convergence;
- identify the files that must be preserved for a reproducible result; and
- decide whether a calculation is ready for BAND, DOSS or ANBD.

## 🧱 The CRYSTAL23 mental model

CRYSTAL represents a periodic solid using a repeating unit cell, a basis set and an electronic-structure method. It first solves the electronic problem for a fixed structure. During geometry optimisation, it then updates the cell and/or atomic coordinates and repeats the electronic calculation until the chosen force, displacement and energy criteria are met.[^1]

```mermaid
flowchart TD
    accTitle: CRYSTAL23 Calculation States
    accDescr: A CRYSTAL23 calculation moves from a structural and methodological input to an SCF wavefunction, then optionally through geometry optimisation and property analysis.

    input[Input: cell, atoms, basis, Hamiltonian] --> scf[SCF solution]
    scf --> scf_ok{SCF converged?}
    scf_ok -->|No| scf_fix[Adjust or diagnose SCF settings]
    scf_fix --> scf
    scf_ok -->|Yes| geometry{Geometry optimisation requested?}
    geometry -->|Yes| relax[Update cell or coordinates]
    relax --> scf
    geometry -->|No| wavefunction[Trusted wavefunction]
    relax --> opt_ok{Geometry converged?}
    opt_ok -->|No| relax
    opt_ok -->|Yes| wavefunction
    wavefunction --> properties[Run BAND, DOSS or ANBD]

    classDef input_state fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#1e3a5f
    classDef decision fill:#fef9c3,stroke:#ca8a04,stroke-width:2px,color:#713f12
    classDef output_state fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#14532d

    class input,scf,scf_fix,relax,properties input_state
    class scf_ok,geometry,opt_ok decision
    class wavefunction output_state
```

## 🔍 Three meanings of "done"

| State | What it means | Evidence to look for |
| --- | --- | --- |
| Job completed | The scheduler process stopped and produced an output file | Queue entry disappears; output and error logs exist |
| SCF converged | The electronic density and energy met the SCF criteria | A clear SCF-convergence message and a sensible final energy |
| Geometry converged | The structure met the optimisation criteria after repeated SCF cycles | A clear optimisation-convergence message, final forces and displacements |

> ⚠️ **Important:** A job can complete without being scientifically usable. Always check the output, not only the queue status.

## 🗃️ Files you will meet

File names vary between local scripts and cluster wrappers, but the roles are stable:

| File or pattern | Role | Preserve it? |
| --- | --- | --- |
| `*.d12` | Main CRYSTAL input: structure, basis, Hamiltonian, k-points and SCF/optimisation settings | Yes |
| `*.d3` | Properties input used by `properties` for BAND, DOSS, ANBD and related analyses | Yes |
| `*.out` | Human-readable calculation output and the first place to inspect convergence | Yes |
| `fort.9`, `fort.98` | Wavefunction/restart files needed by many properties calculations; exact use depends on the run and wrapper | Yes |
| `*.f25`, `*.f98` or site-specific property files | Machine-readable property or wavefunction data produced by a particular calculation | Yes, if used by the analysis |
| `*.qsub` | PBS submission script describing resources and execution commands | Yes |

Do not assume that a file is interchangeable merely because its name looks similar. A BAND or DOSS calculation must use the wavefunction from the intended, converged parent calculation.

## ✅ Pre-run checkpoint

Before submitting a job, record these six items in a short calculation note:

1. Material and structural model
2. Hamiltonian and basis set
3. k-point sampling
4. SCF and optimisation thresholds
5. Expected output files
6. The scientific question the calculation is meant to answer

If you cannot fill in item 6, do not submit a large production job yet. Start with a small validation calculation or ask your supervisor which decision the run should support.

## 🚀 Next step

Continue to [Linux and PBS essentials](01-linux-and-pbs.md). It explains the terminal commands and scheduler actions used in every later page.

## References

[^1]: CRYSTAL Solutions. (n.d.). *CRYSTAL properties tutorial*. https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut
