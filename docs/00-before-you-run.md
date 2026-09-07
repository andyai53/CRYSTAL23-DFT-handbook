# Plan a calculation and keep its record

Before running a calculation, decide how it will be identified and what you will need to check afterwards. This prevents a directory of similar files from becoming impossible to interpret later, and saves time when a supervisor or another student needs to understand the result.

## What you will learn

By the end of this page, you should be able to explain the difference between an input, a job record, an output and a property file. You should also be able to trace a derived result back to the parent calculation that produced its wavefunction.

## One base name for one calculation

CRYSTAL23 files with the same base name belong to one calculation:

```text
ATOMOPT0.d12
ATOMOPT0.qsub
ATOMOPT0.out
ATOMOPT0.o1873029
ATOMOPT0.e1873029
ATOMOPT0.f9
ATOMOPT0.f98
```

The base name `ATOMOPT0` connects the input, PBS script, CRYSTAL output, scheduler logs and wavefunction files. The number in `.o1873029` and `.e1873029` is the PBS job ID recorded by this run.

## Name related calculations

The completed project uses names that expose relationships:

```text
OPT0 -> OPT1
ATOMOPT0 -> ATOMOPT1
ATOMOPT1 -> ATOMOPT1_BAND
ATOMOPT1 -> ATOMOPT1_DOSS
```

`OPT` and `ATOMOPT` distinguish two optimisation routes. The number records the next version. The suffix `_BAND` or `_DOSS` identifies a property derived from a named parent.

This naming pattern is more useful than names such as `new`, `final` or `test2`, because it preserves the calculation history.

## Minimum record

Before submission, record:

| Item | Example |
| --- | --- |
| Calculation name | `ATOMOPT1` |
| Purpose | Continue the atomic-coordinate workflow |
| Parent | `ATOMOPT0` |
| Main change | Insert the recorded atomic displacements |
| Input | `ATOMOPT1.d12` |
| Expected output | `ATOMOPT1.out` and matching wavefunction files |

After the run, add the job ID, completion status and next calculation.

## Files to retain

| File | Project role |
| --- | --- |
| `.d12` | Main CRYSTAL input |
| `.qsub` | PBS resources, environment and executable |
| `.out` | CRYSTAL output used to check the result |
| `.o<job-id>` | PBS standard output and saved-file report |
| `.e<job-id>` | PBS error output |
| `.f9`, `.f98` | Wavefunction files used by later properties jobs |
| `.xyz`, `.gui`, `.cell`, `.frac` | Structure-related outputs when produced |
| `.d3` | Properties input |
| `.BAND`, `.DOSS`, `.f25` | Property data used for analysis or plotting |

Do not decide that a job succeeded from the presence of files alone. Later pages show which output lines were used in this project.

## What remains to be added

Future versions can add a formal calculation register and a data-retention policy. They should be based on the final group workflow rather than invented for completeness.

## Checkpoint

Before moving on, choose one real calculation and write down its base name, parent (if any), input file, output file and intended next use. If one of these is unknown, leave it blank and resolve it before submission.

## Next

Continue to [Working on CX3](01-linux-and-pbs.md).
