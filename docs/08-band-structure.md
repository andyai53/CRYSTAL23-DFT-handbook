# Band structure

_Estimated time: 40 minutes | Difficulty: Intermediate | Syntax source: official tutorial_

---

A band structure shows how calculated electronic energies change along a chosen path through reciprocal space. The path is part of the calculation, so a plausible-looking plot is not enough: record the path and check that it matches the model.

## 🎯 Learning goals

By the end of this page, you should be able to:

- distinguish a reciprocal-space path from a DOS k-point mesh;
- choose whether the bulk or slab convention applies;
- record the path, number of points and energy reference; and
- describe a gap or crossing without claiming more than the calculation shows.

## ✅ Check the parent calculation first

Start a BAND run only when all of these are true:

- [ ] The parent SCF calculation is converged
- [ ] The geometry is converged, if it was optimised
- [ ] The restart or wavefunction file belongs to that parent calculation
- [ ] The dimensionality is clear: three-dimensional bulk or two-dimensional slab
- [ ] The scientific question needs a band path

If any box is unchecked, return to [Properties overview](07-properties-overview.md).

## 🧭 Choose and record the path

The path joins selected high-symmetry points in the Brillouin zone. A bulk cell and a slab do not necessarily use the same path. Before editing a `.d3` file, write this short record:

```text
Model: [bulk / slab]
Reciprocal-space convention: [source or group convention]
Path: [ordered list of points]
Points between labels: [number]
Energy window: [range and units]
Reference energy: [Fermi level or other stated reference]
Reason for this path: [one sentence]
```

Use the [CRYSTAL properties tutorial](https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut) for the exact BAND input syntax.[^1] This handbook supplies the checks around the syntax; it does not replace the version-specific reference.

## 🧪 Run one BAND calculation

Keep the properties run separate from the parent calculation:

1. Copy the matching restart files into a new properties directory.
2. Copy a working local BAND template.
3. Change only the path, point count and energy window needed for this figure.
4. Submit the properties job through the local PBS wrapper.
5. Keep the `.d3`, submission script, output and generated data together.

Do not change the parent Hamiltonian, basis set or geometry while preparing a BAND run. If those choices change, create a new parent calculation and record it as a separate branch.

## 🔍 Inspect the output and plot

Before looking at the plot, check the output for errors and confirm that the requested path was accepted. Then use [CrySPLOT](https://crysplot.crystalsolutions.eu/index.html) to inspect supported CRYSTAL data files.[^2]

Check the following items in the plot:

| Item | What to check |
| --- | --- |
| Horizontal axis | Labels appear in the requested order and are separated at the correct points |
| Vertical axis | Units and reference energy are stated, for example `E - E_F (eV)` |
| Energy range | The window contains the feature you are discussing |
| Bands | Lines are continuous and do not stop because of a parsing or export error |
| Comparison | Bulk and slab plots use compatible conventions before you compare them |

> 📌 **Plotting is the last step:** CrySPLOT displays the data supplied to it. It does not prove that the parent wavefunction converged or that the path is physically appropriate.

## 🧠 What the plot can support

A band plot can support statements about features along the selected path, such as a visible crossing or a gap between the highest occupied and lowest unoccupied bands on that path. It cannot, by itself, establish transport, device performance or a complete band gap if the path does not sample the relevant extrema.

Write the interpretation next to the figure:

```text
Feature: [crossing, gap, flat band, or other feature]
Where: [path segment and energy]
Evidence: [data file and figure name]
Limit: [what this path cannot establish]
```

## 🚀 Next step

Continue to [Density of states](09-density-of-states.md) to learn how total and projected states complement a band plot.

## References

[^1]: CRYSTAL Solutions. (n.d.). *Properties tutorial*. https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut
[^2]: CRYSTAL Solutions. (n.d.). *CrySPLOT*. https://crysplot.crystalsolutions.eu/index.html
