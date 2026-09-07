# Band structure

A band-structure calculation shows how electronic-state energies change along a chosen path in reciprocal space. It can help you see dispersion, band width and the position of occupied and unoccupied bands. It is a property of a checked parent wavefunction, not a separate geometry optimisation.

## What you will learn

You will learn how to prepare a BAND property from a converged parent, which output files to retain, and what can and cannot be concluded from the resulting plot.

## The project input

```text
ATOMOPT1_BAND.d3

NEWK
[NEWK settings]
BAND
2D slab band structure around Fermi level
[band range and path settings]
[reciprocal-space path]
END
```

The input records a two-dimensional slab path and the band range used for this plot. The selected path determines the plotted route through reciprocal space, so it must be retained with the figure. Read the [official properties tutorial](https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut) before changing numerical fields; the syntax and suitable path depend on the system.

The project supervision notes also recommend selected sections of Hoffmann's [How Chemistry and Physics Meet in the Solid State](https://doi.org/10.1002/anie.198708461) for the concepts behind Bloch functions, k-space, band structures, band width and density of states.

## Prepare and submit

Confirm that the parent files exist:

```bash
ls ATOMOPT1.f9 ATOMOPT1.f98 ATOMOPT1_BAND.d3
```

The properties command in the working qsub file names both the property task and its parent:

```text
/rds/.../runpropP ATOMOPT1_BAND ATOMOPT1
```

After checking the edited qsub file, submit it:

```bash
qsub ATOMOPT1.qsub
```

```bash
qstat -u $USER
```

## Check the result

The completed output reported:

```text
TOP OF VALENCE BANDS ...
BOTTOM OF VIRTUAL BANDS ...
INDIRECT ENERGY BAND GAP: ...
* BAND STRUCTURE *
```

Locate these lines in the actual output:

```bash
grep "BAND" ATOMOPT1_BAND.out
```

Then open the output around the reported lines with `less`. Retain `ATOMOPT1_BAND.BAND` and `ATOMOPT1_BAND.f25` as the data files used for plotting.

## Plot and interpret

Open the supported BAND data in [CrySPLOT](https://crysplot.crystalsolutions.eu/index.html). Keep the original `.d3`, `.out`, `.BAND` and `.f25` files with the exported figure. The plot is derived from the selected path: a feature absent from that path may still occur elsewhere in reciprocal space. Read the reported valence-band top, virtual-band bottom and gap in the output before assigning a label to the plot.

## Checkpoint

Before sharing a band plot, record the parent calculation, BAND input, reciprocal-space path, output filename and the reported gap statement. This gives another student enough information to reproduce the plot or check its interpretation.

## Next

Continue to [Density of states](09-density-of-states.md).
