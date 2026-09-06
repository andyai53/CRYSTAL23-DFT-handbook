# Reading CRYSTAL23 input and output

_Estimated time: 35 minutes | Difficulty: Beginner | Last verified: 2026-09-05_

---

CRYSTAL input files are compact, but each block answers a different scientific question. Read the input from top to bottom, then inspect the output in an order that prevents common false conclusions.

## 🎯 Learning goals

- Identify the structural, methodological and numerical choices in a `.d12` file
- Explain what a `.d3` properties input is connected to
- Find the final SCF and geometry status in an `.out` file
- Record the choices that affect reproducibility

## 🧩 Read the input in layers

Read the input as a chain of decisions, not as a wall of keywords:

```mermaid
flowchart LR
    accTitle: CRYSTAL23 Input Layers
    accDescr: A CRYSTAL23 input moves from the periodic structure through the electronic method and numerical sampling to convergence and optimisation controls.

    structure[Structure: cell and atoms] --> basis[Basis set]
    basis --> method[Hamiltonian and XC treatment]
    method --> sampling[Brillouin-zone sampling]
    sampling --> controls[SCF and optimisation controls]
    controls --> output[Expected output and restart files]

    classDef primary fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#1e3a5f
    classDef output_state fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#14532d
    class structure,basis,method,sampling,controls primary
    class output output_state
```

### Structure

Check the formula, dimensionality, lattice parameters, atom count and coordinate convention. For a slab, also check the vacuum direction and confirm that periodicity is intended in two dimensions.

### Basis and Hamiltonian

The basis set and Hamiltonian are part of the model. Copy them into the calculation note exactly as written. Changing either one creates a new calculation branch.

### Sampling and numerical controls

Record the k-point sampling, smearing, SCF threshold, mixing, maximum cycles and any restart option. These settings can determine whether a metallic or near-metallic calculation reaches a stable solution.

### Properties input

A `.d3` file is not a second geometry optimisation. It tells `properties` what to analyse from a wavefunction generated earlier. BAND, DOSS, ANBD and related analyses are meaningful only when that wavefunction belongs to the intended converged calculation.[^1]

## 🔍 Inspect the output in order

Use this order for every output:

1. **Identity:** confirm the structure, basis, Hamiltonian and k-point setup match the input you intended to run.
2. **Execution:** confirm the expected executable started and that the output is not truncated at the beginning.
3. **SCF:** inspect the final iterations and look for an explicit convergence message.
4. **Geometry:** if optimisation was requested, check the final forces, displacements and optimisation status.
5. **Artifacts:** confirm the wavefunction/restart files needed by later properties runs exist and belong to this calculation.

Useful searches for a text output are:

```bash
grep -n "SCF ENDED\|SCF CONVERGENCE\|OPT END\|CONVERGED" calculation.out
grep -n "TOTAL ENERGY\|FINAL ENERGY\|LATTICE" calculation.out
tail -n 80 calculation.out
```

The wording varies with the CRYSTAL version and local wrapper. Treat these strings as search hints, then read the surrounding lines.

## ✅ A defensible completion record

Do not write only "job finished". Record a compact status like this:

```text
Material: training system
Input: inputs/training.d12
Hamiltonian/basis: [copy exactly from input]
SCF: converged at cycle [N], final energy [value]
Geometry: [not requested / converged / not converged]
Wavefunction: [file names and timestamp]
Properties-ready: [yes / no, with reason]
```

This record lets another student understand the run without guessing from a directory full of files.

## ⚠️ Common reading errors

### "The output file exists, so the run worked"

An output file can be created before the executable fails. Check the last lines, scheduler error log and explicit SCF/geometry status.

### "SCF converged, so the structure is optimised"

SCF convergence refers to the electronic state for one geometry. Geometry convergence is a separate test over forces, displacements and energy changes.

### "The BAND plot looks reasonable, so the path must be correct"

The path is part of the physical interpretation. For bulk and two-dimensional slabs, use the reciprocal-space convention appropriate to the model and record the high-symmetry points in the calculation note. [CrySPLOT](https://crysplot.crystalsolutions.eu/index.html) can help you inspect the resulting data, but it cannot decide whether the path is physically appropriate.[^2]

## 🚀 Next step

Continue to [SCF convergence](04-scf-convergence.md) to learn how to recover a difficult calculation without changing several scientific assumptions at once.

## References

[^1]: CRYSTAL Solutions. (n.d.). *Properties tutorial*. https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut
[^2]: CRYSTAL Solutions. (n.d.). *CrySPLOT*. https://crysplot.crystalsolutions.eu/index.html
