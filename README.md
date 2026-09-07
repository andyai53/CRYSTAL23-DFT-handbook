# CRYSTAL23 starter handbook for CX3

This handbook helps new group members prepare, submit and check CRYSTAL23 calculations on Imperial College London's CX3 cluster. It focuses on the practical steps that make a calculation understandable to its author and reusable by the next student: which file to edit, which command to run, what to check afterwards, and what to keep.

It is not a substitute for the CRYSTAL23 manual or project-specific scientific guidance. The examples come from completed group calculations, but they illustrate a workflow rather than prescribe a method, functional, basis set or resource request.

## What you will learn

- how to move safely through a CX3 project directory;
- how to create and submit a named CRYSTAL23 calculation;
- how `.d12`, `.qsub`, `.out` and scheduler files fit together;
- how to check SCF and geometry optimisation completion separately;
- when `ATOMONLY` changes a geometry optimisation;
- how BAND and DOSS calculations depend on a converged parent; and
- how to leave a clear record for the next person who needs the result.

## How to use this handbook

Read the pages in order for a first calculation. Each page introduces a small task, gives only the commands needed for that task, and ends with a checkpoint. Keep the file names in the commands as examples: replace them with your own calculation name after confirming the intended input with your supervisor or project guidance.

The command and file relationships were checked against completed group work. Unverified details are deliberately left to the official documentation or local supervision rather than filled in by guesswork.

## Start here

Read the pages in order:

1. [Plan a calculation and keep its record](docs/00-before-you-run.md)
2. [Working on CX3](docs/01-linux-and-pbs.md)
3. [Creating and submitting a calculation](docs/02-first-crystal23-job.md)
4. [Reading a CRYSTAL23 input and output](docs/03-reading-input-and-output.md)
5. [Checking SCF completion](docs/04-scf-convergence.md)
6. [Managing geometry optimisation](docs/05-geometry-optimisation.md)
7. [Managing calculation versions](docs/06-convergence-as-evidence.md)
8. [Properties calculations](docs/07-properties-overview.md)
9. [Band structure](docs/08-band-structure.md)
10. [Density of states](docs/09-density-of-states.md)

## Reference sources

- [CRYSTAL23 documentation](https://www.crystal.unito.it/documentation.html)
- [CRYSTAL Basis Sets Library](https://www.crystal.unito.it/basis_sets.html)
- [CRYSTAL properties tutorial](https://tutorials.crystalsolutions.eu/tutorial.html?td=properties&tf=properties_tut)
- [CrySPLOT](https://crysplot.crystalsolutions.eu/index.html)
- [Imperial Unified Access](https://www.imperial.ac.uk/admin-services/ict/self-service/connect-communicate/remote-access/unified-access/)
- [Dovesi et al. (2020), The CRYSTAL code, 1976-2020 and beyond](https://doi.org/10.1063/5.0004892)

## Scope

This handbook does not prescribe universal core counts, walltimes, convergence controls or production settings. Those choices depend on the system, current CX3 configuration and research question. Ask for project guidance when a decision affects the model or calculation settings.
