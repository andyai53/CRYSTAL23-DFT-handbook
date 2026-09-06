# Your first CRYSTAL23 job

_Estimated time: 45 minutes | Difficulty: Beginner | Local example required_

---

This is the first complete run. Use a small input that your group has already tested. The aim is to learn the workflow, not to start a production calculation.

## 🎯 Learning goals

By the end of this page, you should be able to:

- copy an approved input without changing the source example;
- submit one job through PBS;
- follow the output while the job runs;
- find the final SCF energy and convergence message; and
- record the run so that another student can repeat it.

## 📦 Before you start

Ask your supervisor or group for these two files:

| File | Purpose |
| --- | --- |
| A small, tested `*.d12` input | Training calculation with a known expected outcome |
| A working `*.qsub` script | Local PBS resources and CRYSTAL23 executable setup |

Do not use a large Ti2C/Ti3C2 production model for this exercise. A small training system makes it easier to tell a cluster problem from a model or input problem.

> ⚠️ **Do not guess the input:** This repository leaves the example path open until the group has approved and tested the exact files. A first-job tutorial should never present an untested calculation as a copy-and-run example.

## 🗂️ Create a clean run directory

Run the following from the project root. Replace `/path/to/approved-example` with the directory supplied by your group:

```bash
mkdir -p training/first_job/{inputs,jobs,outputs,logs,notes}
cp /path/to/approved-example/training.d12 training/first_job/inputs/
cp /path/to/approved-example/training.qsub training/first_job/jobs/
cd training/first_job
```

Open the copied script and check its paths:

```bash
less jobs/training.qsub
```

The script should read `inputs/training.d12` and write the output to `outputs/training.out`, or use paths that are clearly equivalent. Do not edit the source example in place.

## 🚀 Submit and monitor the job

Submit from the directory that contains `inputs/`, `jobs/` and `outputs/`:

```bash
qsub jobs/training.qsub
qstat -u "$USER"
```

PBS returns a job identifier. Keep it in your notes. While the job is running, inspect the output occasionally:

```bash
grep -n "SCF\|converg\|ERROR" outputs/training.out
tail -n 40 outputs/training.out
```

The output may be empty while the job is waiting for a node. That is normal. Do not resubmit just because the file has not grown yet.

## ✅ Check the result

When the job leaves the queue, inspect the output and scheduler logs. A successful first run must pass all four checks:

- the output is not empty or truncated at startup;
- the final SCF block reports convergence;
- a final energy is present; and
- the job did not stop at `MAXCYCLE` or an error message.

Record the result in `notes/first-run.md`:

```text
Input: inputs/training.d12
PBS script: jobs/training.qsub
PBS job ID: [copy the ID]
Output: outputs/training.out
SCF status: [converged / not converged]
Final energy: [copy the value and units as printed]
Problems or warnings: [none, or describe them]
Next action: [continue / ask for help / diagnose]
```

> 📌 **Checkpoint:** Before moving on, you should be able to answer which input ran, which PBS job ID it used, where the convergence message appears and which files must be kept.

## 🚫 If the run fails

Keep the failed input, script, output and scheduler log. Write one sentence explaining what happened. Then return to [Linux and PBS essentials](01-linux-and-pbs.md) or [SCF convergence](04-scf-convergence.md). Do not overwrite the only copy and do not change several controls at once.

## 🚀 Next step

Continue to [Reading CRYSTAL23 input and output](03-reading-input-and-output.md). You will learn what each input block controls and how to read an output in a fixed order.
