# Density of states

_Estimated time: 40 minutes | Difficulty: Intermediate | Syntax source: official tutorial_

---

The density of states (DOS) counts electronic states as a function of energy. A total DOS gives the overall distribution. A projected DOS (PDOS) separates contributions from selected atoms or orbitals, so plan the labels before running the calculation.

## 🎯 Learning goals

By the end of this page, you should be able to:

- distinguish total DOS from atom- and orbital-projected DOS;
- build a projection table before editing the input;
- align the energy axis consistently; and
- describe a DOS feature without turning a projection into a unique chemical assignment.

## ✅ Check the parent calculation first

Use a DOS calculation only when the parent calculation is accepted:

- [ ] SCF convergence is explicit in the parent output
- [ ] Geometry convergence is explicit when optimisation was requested
- [ ] The restart or wavefunction file matches the accepted parent structure
- [ ] The k-point sampling is recorded
- [ ] The energy reference is defined

The [CRYSTAL properties tutorial](https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut) gives the exact DOSS syntax and options.[^1]

## 🧾 Plan the projections

Decide what each curve should answer before you create the `.d3` file. Record atom numbers and orbital groups from the parent structure, not from the order in which curves appear in a plot.

| Curve label | Atoms or region | Orbitals | Question |
| --- | --- | --- | --- |
| Total | All atoms | All included states | What is the overall distribution? |
| Ti | Ti atoms or selected layer | [orbitals] | Which Ti states contribute? |
| C | C atoms | [orbitals] | Which C states contribute? |
| Termination | H/O/F/OH or other group | [orbitals] | Does the termination add states in this energy range? |

Keep this table with the input and use the same labels in the final figure. If you cannot explain a projection in one sentence, simplify it before running the job.

## 🧪 Run one DOS calculation

1. Create a new properties directory from the validated parent record.
2. Copy the matching restart files and a working local DOSS template.
3. Set the total or projected curves described in your projection table.
4. Record the k-point sampling, energy range and broadening settings.
5. Submit the job and inspect the output before plotting.

Run related projections from the same parent wavefunction when you need a direct comparison. Changing the parent method or structure creates a different calculation, not a different curve set.

## 📈 Inspect the plot with CrySPLOT

[CrySPLOT](https://crysplot.crystalsolutions.eu/index.html) can display supported CRYSTAL property data.[^2] Use it to check the exported curves, then save the figure with the source data and `.d3` file.

| Item | What to check |
| --- | --- |
| Energy axis | Units and reference are stated, for example `E - E_F (eV)` |
| Zero of energy | The same reference is used across figures you compare |
| Curve labels | Each label maps to one row in the projection table |
| Broadening | The value and units are recorded; broadening is not physical temperature |
| k-point sampling | The mesh is recorded and suitable for the model |

> 📌 **Keep the raw data:** A screenshot is not a substitute for the original property data and input.

## 🧠 What a DOS can support

A DOS peak can show that states from a selected projection occur in an energy range. It does not identify a unique reaction mechanism, charge-transfer pathway or magnetic interaction by itself. Compare the DOS with the structure, band plot and, where relevant, charge or bonding analysis.

Use wording that matches the evidence:

```text
The [projection] contributes states near [energy range] in this model.
This assignment is based on the selected projection scheme and does not by itself prove [stronger claim].
```

## 🚀 Next step

Use [Convergence as evidence](06-convergence-as-evidence.md) to test whether the DOS feature is stable when you change the relevant numerical setting.

## References

[^1]: CRYSTAL Solutions. (n.d.). *Properties tutorial*. https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut
[^2]: CRYSTAL Solutions. (n.d.). *CrySPLOT*. https://crysplot.crystalsolutions.eu/index.html
