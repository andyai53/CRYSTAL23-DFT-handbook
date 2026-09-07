# Managing calculation versions

The project contains variants because each calculation answers a different question or continues a previous calculation. Treat every variant as a named record.

## What you will learn

You will practise comparing two inputs without losing the earlier version. The aim is to make the reason for a new calculation visible to a future reader.

## Variant table

| Name | Parent or relation | Change visible in the input |
| --- | --- | --- |
| `OPT0` | Starting optimisation route | `OPTGEOM` |
| `OPT1` | Follows `OPT0` | `ATOMDISP`, `ELASTIC`, coordinate reporting |
| `ATOMOPT0` | Starting atomic-only route | `OPTGEOM`, `ATOMONLY` |
| `ATOMOPT1` | Follows `ATOMOPT0` | `BREAKSYM`, `ATOMDISP`, `ATOMONLY` |
| `ATOMOPT1_BAND` | Property of `ATOMOPT1` | `.d3` with `BAND` |
| `ATOMOPT1_DOSS` | Property of `ATOMOPT1` | `.d3` with `DOSS` |

## Create a variant without losing the source

```bash
cp ATOMOPT0.d12 ATOMOPT1.d12
cp ATOMOPT0.d12 ATOMOPT1.d12.beforeINSDISP
vi ATOMOPT1.d12
diff ATOMOPT0.d12 ATOMOPT1.d12
```

The backup documents the pre-edit state. The diff documents the intended change.

## Keep the same base name across the job

If the input is `ATOMOPT1.d12`, the generated submission script and output should use `ATOMOPT1`:

```text
ATOMOPT1.d12
ATOMOPT1.qsub
ATOMOPT1.out
ATOMOPT1.f9
ATOMOPT1.f98
```

For a derived property:

```text
ATOMOPT1_BAND.d3
ATOMOPT1_BAND.out
ATOMOPT1_BAND.BAND
```

In the completed directory, the properties command was held in `ATOMOPT1.qsub`. The active `runpropP` line records the property name and the `ATOMOPT1` parent.

## What a good variant record says

```text
New calculation: ATOMOPT1
Parent: ATOMOPT0
Reason:
Input change:
Files retained:
PBS job ID:
Output status:
Next use:
```

The `Reason` and `Input change` fields are the important project-management information. A version number alone is not an explanation.

## A small exercise

Choose `ATOMOPT0.d12` and `ATOMOPT1.d12` from a project copy. Run `diff`, then write one sentence describing each changed block. Do not interpret a block whose purpose has not been confirmed; write “purpose to be confirmed” and keep the input as the source.

## Scope

This page does not define a numerical convergence study. A formal basis, k-point or slab-thickness study can be added when the project records and acceptance criteria are available.

## Next

Continue to [Properties calculations](07-properties-overview.md).
