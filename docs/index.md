---
layout: default
title: CRYSTAL23 starter handbook for CX3
---

# CRYSTAL23 starter handbook for CX3

This handbook is for students starting CRYSTAL23 work on CX3. Follow the workflow from top to bottom for a first calculation. At each stage, make a small record of what you changed and what the output shows; this is what allows you, a supervisor or a later student to understand the result without reconstructing the entire calculation.

## Workflow

| Stage | Page | Record produced |
| --- | --- | --- |
| Plan the calculation | [Plan a calculation and keep its record](00-before-you-run.md) | Calculation name and purpose |
| Work on the cluster | [Working on CX3](01-linux-and-pbs.md) | Known project location |
| Submit a job | [Creating and submitting a calculation](02-first-crystal23-job.md) | Input, qsub file and job ID |
| Check files | [Reading input and output](03-reading-input-and-output.md) | Input and output summary |
| Check electronic convergence | [Checking SCF completion](04-scf-convergence.md) | SCF status and energy |
| Track optimisation | [Geometry optimisation](05-geometry-optimisation.md) | Optimised structure and status |
| Compare versions | [Managing calculation versions](06-convergence-as-evidence.md) | Difference and reason for each version |
| Create derived jobs | [Properties calculations](07-properties-overview.md) | Parent-property relationship |
| Analyse results | [Band structure](08-band-structure.md) and [Density of states](09-density-of-states.md) | Plot data and interpretation |

## Before you start

You need access to CX3, a project directory, and an input or example approved for your project. The commands and file relationships here were checked against completed group calculations. They are examples for learning the workflow, not a replacement for checking the CRYSTAL23 manual and your group guidance.
