# Your first CRYSTAL23 job

_Estimated time: 45 minutes plus queue time | Difficulty: Beginner | Validated local input required_

---

This exercise runs one small `.d12` input from its own directory. You will copy a tested example, submit it using the method approved by your group and decide whether the result is usable.

## 🎯 Learning goals

By the end of this page, you should be able to:

- prepare a run without changing the shared source file;
- submit through the local `qcry23` wrapper or a supplied PBS script;
- find the output after the job leaves the queue; and
- record the SCF result and files needed for later work.

## 📦 Get a tested example

Ask your supervisor or group for:

| Required item | Why you need it |
| --- | --- |
| A small, tested `training.d12` | The expected calculation is already known |
| The current CX3 submission instructions | Wrapper arguments and PBS resources change between environments |
| A working `.qsub` template, if used | It contains the approved CRYSTAL23 executable and resource request |
| The expected success message or output | You need something concrete to compare against |

Do not begin with a large production model. A short training job makes input, software and queue problems easier to separate.

## 1. Create the run directory

Log in to CX3, then create a directory in your home area:

```bash
cd ~
mkdir -p crystal23-training/first_job
cd crystal23-training/first_job
pwd
```

Copy the approved input. Replace the source path with the one your group gives you:

```bash
cp /path/to/approved-example/training.d12 .
```

The final dot means “the current directory”. If the workflow uses a supplied PBS script, copy that too:

```bash
cp /path/to/approved-example/training.qsub .
```

Check the result before continuing:

```bash
ls -lah
less training.d12
```

Press `q` to leave `less`. At this point, `ls` should show the copied `.d12` file and, when required, the `.qsub` file.

## 2. Make a run note

Record the source before submitting:

```bash
cat > run-note.txt <<'EOF'
Purpose: first CRYSTAL23 training job
Input source: /path/to/approved-example/training.d12
Submission method: [qcry23 / qsub]
Expected result: [copy from group example]
EOF
```

Reopen the note with `vi run-note.txt` and replace the bracketed text. This note prevents a copied file from losing its origin.

## 3. Submit by the approved route

### Route A: the CX3 `qcry23` wrapper

Check that the wrapper exists:

```bash
command -v qcry23
```

Use the argument format confirmed by your group. For example, an earlier project used:

```bash
qcry23 training.d12 64 1:00
```

Treat `64 1:00` as an environment-specific example, not a recommended resource request. After submission, write the printed job ID and the exact command into `run-note.txt`.

### Route B: a supplied PBS script

Read the script before running it:

```bash
less training.qsub
grep -n "PBS\|runcry\|crystal" training.qsub
qsub training.qsub
```

Do not replace executable paths or PBS resource lines by guessing. Use the current working group template.

## 4. Monitor the job

```bash
qstat -u "$USER"
```

While it is queued, wait. While it is running, list the directory occasionally:

```bash
ls -rtl
```

If an output file exists, inspect its last lines:

```bash
tail -n 40 training.out
```

Use the actual filename shown by `ls` if the wrapper chose a different name. Do not resubmit merely because the output is initially empty.

## 5. Decide whether it worked

When the job no longer appears in `qstat`, run:

```bash
ls -lah
grep -n -i "scf\|converg\|error\|maxcycle" training.out
tail -n 80 training.out
```

A successful first run must meet all of these conditions:

- the output is not empty or truncated at startup;
- the final SCF section explicitly reports convergence;
- a final energy is present;
- the job did not stop at an error or `MAXCYCLE`; and
- any expected restart or wavefunction files were produced.

An output file and a completed PBS job are not enough by themselves.

## 6. Complete the record

Add the following information to `run-note.txt`:

```text
Submission command: [exact command]
PBS job ID: [ID]
Output file: [name]
SCF status: [converged / not converged]
Final energy: [value and units exactly as printed]
Restart or wavefunction files: [names]
Warnings: [none, or short description]
Next action: [continue / diagnose / ask for help]
```

Keep the `.d12`, `.qsub` if used, `.out`, scheduler logs, wavefunction files and `run-note.txt` together. Do not rename only one member of a file set if the local wrapper expects matching base names.

## 🔧 If something fails

| What you see | First check |
| --- | --- |
| `qcry23: command not found` | You are on the expected CX3 host and have loaded the group environment |
| `qsub: command not found` | You are logged in to CX3 rather than typing on your own computer |
| Job stays in `Q` | PBS has accepted it; wait or inspect the scheduler reason |
| Job disappears with no useful `.out` | Read scheduler error files and the `.qsub` executable path |
| Output ends at `MAXCYCLE` | The SCF did not converge; continue to the SCF chapter |
| Output is converged but expected restart files are missing | Check the approved wrapper/template and output paths |

Keep the failed attempt. It is the evidence needed to diagnose the problem.

## ✅ First-job checkpoint

- [ ] I know the absolute path of the run directory
- [ ] I know where the input came from
- [ ] I recorded the exact submission command and job ID
- [ ] I found explicit SCF convergence in the output
- [ ] I recorded the final energy and wavefunction files

## 🚀 Next step

Continue to [Reading CRYSTAL23 input and output](03-reading-input-and-output.md). You will connect the keywords in `training.d12` to the evidence in `training.out`.
