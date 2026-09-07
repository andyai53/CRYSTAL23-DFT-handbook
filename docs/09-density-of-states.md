# Density of states

A density-of-states (DOS) calculation groups electronic states by energy. A total DOS shows how many states occur at each energy; a projected DOS selects the states associated with chosen atoms or orbitals. In this workflow, `ATOMOPT1_DOSS` is a property derived from the converged `ATOMOPT1` wavefunction.

## What you will learn

You will learn how DOSS inputs define a question about selected states, how to check the resulting files, and why the projection definition must travel with every figure.

## The project inputs

The first DOSS input contains:

```text
ATOMOPT1_DOSS.d3

NEWK
[NEWK settings]
DOSS
[energy range and sampling settings]
[projection group 1]
[projection group 2]
END
```

A second input changed the projection grouping:

```text
ATOMOPT1_DOSS_2.d3

DOSS
[revised energy range and sampling settings]
[revised projection groups]
END
```

The files are kept as separate versions because they ask for different projections. A projected curve only represents the atom or orbital groups explicitly selected in the `.d3` input. Use the [official properties tutorial](https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut) to interpret the numeric syntax before changing it.

## Prepare and submit

Confirm the parent wavefunction and DOSS input:

```bash
ls ATOMOPT1.f9 ATOMOPT1.f98 ATOMOPT1_DOSS.d3
cat ATOMOPT1_DOSS.d3
```

The properties command in the working qsub file names both the property task and its parent:

```text
/rds/.../runpropP ATOMOPT1_DOSS ATOMOPT1
```

Submit and monitor:

```bash
qsub ATOMOPT1.qsub
```

```bash
qstat -u $USER
```

## Check and retain the result

The completed job produced:

```text
ATOMOPT1_DOSS.out
ATOMOPT1_DOSS.DOSS
ATOMOPT1_DOSS.f25
```

Check that the output contains a DOSS section:

```bash
grep "DOSS" ATOMOPT1_DOSS.out
```

Keep the `.d3`, `.out`, `.DOSS` and `.f25` files together. Open the supported data in [CrySPLOT](https://crysplot.crystalsolutions.eu/index.html) and retain the source files with the figure.

## Interpret the selection

A projection shows the states included by the selected atom or orbital grouping. State the grouping in the figure caption, together with the parent calculation and energy reference used in the plot. Comparing the total DOS with the selected projections can show which chosen groups contribute in a given energy range; it does not by itself prove a complete chemical explanation.

## Checkpoint

Before sharing a DOS plot, record the parent calculation, `.d3` input, selected projection groups, output filename and the energy range shown. Another student should be able to identify exactly what each curve includes.

## Next

The workflow currently ends here. Bonding analysis and a formal interpretation guide can be added after the project inputs and scientific questions are documented.
