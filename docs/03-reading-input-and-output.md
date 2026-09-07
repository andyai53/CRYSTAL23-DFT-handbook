# Reading a CRYSTAL23 input and output

Read a calculation in two directions: read the input to understand what was requested, then read the output to confirm what actually ran. This page uses the structure of the completed slab inputs.

## What you will learn

You will learn a fixed reading order:

1. identify the structure and dimensionality;
2. identify the optimisation and electronic settings;
3. check the SCF completion line; and
4. check the optimisation or properties result separately.

This order prevents a successful scheduler job from being mistaken for a converged calculation.

## Input blocks used in the project

The early part of a project input contains the model:

```text
Ti2C-rev2
CRYSTAL
[dimensionality and centring]
[space-group entry]
[cell parameters]
[number of symmetry-independent atoms]
[atomic number and coordinates]
SLAB
[slab definition]
```

From this block, record:

| Block | Record |
| --- | --- |
| Title | The calculation label |
| `CRYSTAL` | The periodic CRYSTAL calculation type |
| Space-group and cell lines | The symmetry and cell definition used by the input |
| Atomic lines | Atomic numbers and positions |
| `SLAB` | The two-dimensional slab setup |

Do not rewrite the atomic coordinates in a project note. Record the input filename and preserve the input itself.

## Read geometry changes before submitting

The optimisation section in the completed files is:

```text
OPTGEOM
ENDOPT
ENDGEOM
```

`ATOMOPT0` adds `ATOMONLY`, so it represents an atomic-coordinate optimisation. `ATOMOPT1` adds `ATOMDISP` and `BREAKSYM` before the optimisation block. These are changes made for this project, not a universal template. The geometry-optimisation page explains the different purpose of `ATOMONLY` and `ATOMDISP`.

Use `diff` to inspect a version change:

```bash
diff OPT0.d12 OPT1.d12
```

The project record shows that the structure-related block changes between these versions. Before submitting a copied input, you should be able to say what each changed block is intended to do. The scientific reason for a displacement belongs in the calculation record.

## Electronic settings confirmed in these inputs

The later input section contains:

```text
SHRINK
8 16
DFT
B3LYP
XXLGRID
END
END
```

This confirms that the project used B3LYP, an XXLGRID setting and a recorded SHRINK entry. The handbook records these choices; it does not claim they are suitable for every system.

The completed inputs contain explicit basis-set definitions for Ti and C. The [CRYSTAL Basis Sets Library](https://www.crystal.unito.it/basis_sets.html) is the official place to inspect available element-specific definitions. This handbook does not select a basis for a new system.

## Output checks used in the project

For a fixed-geometry or optimisation output, search for the specific SCF completion line:

```bash
grep "SCF E" OPT0.out
```

The completed output contains a line of the form:

```text
== SCF ENDED - CONVERGENCE ON ENERGY E(AU) ...
```

For a geometry optimisation, search for the optimisation conclusion:

```bash
grep "OPT END" OPT0.out
```

The completed output contains:

```text
* OPT END - CONVERGED *
```

These are separate checks. An SCF convergence line confirms the electronic calculation at a geometry. `OPT END - CONVERGED` confirms the optimisation status.

## Output and scheduler files

The `.out` file is the CRYSTAL output. The `.o<job-id>` file records PBS information, including the input, output, wavefunction files and saved optimisation history. The `.e<job-id>` file is the PBS error stream.

Read them separately:

```bash
grep "SCF E" OPT0.out
```

```bash
less OPT0.out
```

```bash
cat OPT0.o1873025
```

Do not join these commands on one line. Each command reads a different file for a different purpose.

## What remains to be added

The exact meaning of every coordinate and basis-set line will be added when the project input conventions are formally documented. Until then, the input file remains the authoritative source.

## Checkpoint

For one output file, locate the SCF completion line and the final optimisation line (when optimisation was requested). Write both line names in your calculation record before using the wavefunction for properties.

## Next

Continue to [Checking SCF completion](04-scf-convergence.md).
