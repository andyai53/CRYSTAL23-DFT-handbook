# Geometry optimisation

_Estimated time: 35 minutes | Difficulty: Beginner to intermediate | Last verified: 2026-09-05_

---

Geometry optimisation searches for a structure that meets the force, displacement and energy criteria set in the input. Each optimisation step needs a converged electronic solution before the geometry can be updated.

## 🎯 Learning goals

- Distinguish a fixed-geometry SCF calculation from a relaxed structure
- Explain the difference between cell optimisation and atomic-coordinate optimisation
- Verify forces, displacements and the final optimisation status
- Keep slab constraints and symmetry choices explicit

## 🧭 Two layers of convergence

```mermaid
flowchart TD
    accTitle: Geometry Optimisation Loop
    accDescr: Each geometry step requires a converged SCF solution before forces and displacements are evaluated; the loop ends only when the geometry criteria are satisfied.

    geometry[Current geometry] --> scf[Converge the SCF density]
    scf --> forces[Evaluate energy, forces and displacements]
    forces --> criteria{Geometry criteria met?}
    criteria -->|No| update[Update cell and/or atomic coordinates]
    update --> geometry
    criteria -->|Yes| final[Accepted relaxed structure]

    classDef primary fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#1e3a5f
    classDef decision fill:#fef9c3,stroke:#ca8a04,stroke-width:2px,color:#713f12
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#14532d

    class geometry,scf,forces,update primary
    class criteria decision
    class final success
```

## 🧱 What is being optimised?

| Choice | What changes | Typical use |
| --- | --- | --- |
| Fixed-geometry SCF | Nothing in the structure | Final energy or properties at a specified geometry |
| Atomic-coordinate optimisation | Atomic positions within a fixed cell | Local relaxation, adsorption height, surface rumpling |
| Cell optimisation | Lattice parameters and often atomic positions | Bulk equilibrium structure |
| Constrained slab optimisation | Selected coordinates are fixed or restricted | Preserve a bulk-like centre while relaxing the surface |

The keyword and constraint syntax depends on the calculation. In your record, state whether the cell, atoms or both could relax. Also record frozen layers and symmetry restrictions.[^1]

## 🧪 Prepare an optimisation safely

Start from a converged fixed-geometry calculation and a working local optimisation example. Make a new directory so that the starting result remains intact:

```bash
cd ~/crystal23-training
mkdir -p geometry_opt
cp first_job/training.d12 geometry_opt/relaxed.d12
cp first_job/training.qsub geometry_opt/relaxed.qsub  # if a qsub template is used
cd geometry_opt
vi relaxed.d12
```

In a standard CRYSTAL input, an optimisation section begins with `OPTGEOM` and ends with `ENDOPT`. A minimal block may look like:

```text
OPTGEOM
ENDOPT
```

Its position and any options inside it must follow a tested input or the CRYSTAL23 manual. In particular, decide whether you are relaxing atomic coordinates, the cell, or both. Do not add `OPTGEOM` to a production input without checking this choice.

Compare the new input with its source:

```bash
diff -u ../first_job/training.d12 relaxed.d12
```

Submit through the approved route:

```bash
qcry23 relaxed.d12 <cores> <walltime>
```

If your workflow uses a supplied PBS script instead:

```bash
qsub relaxed.qsub
```

## 🔍 Inspect the final output

Search for the final optimisation block and then read the surrounding lines:

```bash
grep -n "OPT END\|CONVERGED\|FORCES\|DISPLAC" relaxed.out
tail -n 120 relaxed.out
```

A useful completion record contains:

```text
Optimisation type: [cell + coordinates / coordinates only / constrained slab]
SCF status at final step: converged
Final energy: [value and units as printed]
Maximum force: [value and units as printed]
Maximum displacement: [value and units as printed]
Geometry status: converged / not converged
```

`OPT END - CONVERGED` is a common CRYSTAL output marker. Read the surrounding force and displacement values as well. A job reaching walltime or lowering its energy once does not prove that the geometry converged.

## 🔄 Continue an unfinished optimisation

If the job reaches walltime or the optimisation cycle limit, first determine whether the last geometry step had a converged SCF solution:

```bash
grep -n -i "opt end\|converg\|maxcycle\|error" relaxed.out
tail -n 150 relaxed.out
```

Do not decide from a single trailing number: its meaning depends on the output line. To continue, use the final accepted geometry and restart files in the way required by the current CRYSTAL23 and CX3 template. Preserve the first attempt, create `geometry_opt_02`, and record which geometry and wavefunction were copied. A restart file from a different structure or method can invalidate the continuation.

The group note mentions adding an optimisation cycle limit such as `MAXCYCLE 100` inside the optimisation block. `MAXCYCLE` also appears in SCF contexts, so confirm the block and syntax in the manual before using it.

## ⚠️ Slab-specific checks

For a slab or surface model, check all of the following before using the relaxed structure:

- The vacuum spacing remains large enough to prevent unintended periodic-image interaction
- The intended number of layers is present after optimisation
- Frozen or constrained atoms were applied to the intended region
- The central layers remain sufficiently bulk-like for the scientific question
- The final surface geometry does not come from an unconverged SCF step

## ✅ Geometry checkpoint

Proceed to BAND, DOSS or ANBD only after the parent structure passes both convergence layers:

- [ ] Final SCF is converged
- [ ] Final geometry criteria are converged, if optimisation was requested
- [ ] The relaxed structure was saved separately from the starting input
- [ ] Constraints and optimisation type are recorded
- [ ] The wavefunction files correspond to the accepted final structure

## 🚀 Next step

Continue to [Convergence as evidence](06-convergence-as-evidence.md) to learn how to justify numerical choices rather than treating one successful run as proof of accuracy.

## References

[^1]: CRYSTAL Solutions. (n.d.). *CRYSTAL documentation*. https://www.crystal.unito.it/documentation.html
