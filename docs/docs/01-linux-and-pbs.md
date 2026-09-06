# Linux and PBS essentials

_Estimated time: 45 minutes | Difficulty: Beginner | CX3 notes included_

---

This page takes you from your own computer to a calculation directory on CX3. Work through the commands in order. Text inside angle brackets, such as `<username>`, is a placeholder: replace it and remove the brackets.

## 🎯 Learning goals

By the end of this page, you should be able to:

- connect to Imperial services and log in to CX3;
- tell which directory you are in and what files it contains;
- copy, rename, inspect and edit a file without losing the original;
- submit a PBS job and follow it in the queue; and
- find the output that must be checked after the job ends.

## 1. Connect from outside Imperial

Some Imperial services require an approved remote-access route when you are off campus. Imperial's [Unified Access guide](https://www.imperial.ac.uk/admin-services/ict/self-service/connect-communicate/remote-access/unified-access/) explains how Zscaler Private Access is installed and used.[^1] Students must request Unified Access from the ICT Service Desk before following those instructions.

Remote access only provides the network route. It does not log you in to CX3 or submit a calculation.

## 2. Open a terminal and log in to CX3

Open Terminal on macOS or Linux. On Windows, use the SSH client recommended by Imperial. Then run:

```bash
ssh <username>@login.cx3.hpc.ic.ac.uk
```

Use your own Imperial username. Enter your password and complete MFA if prompted. Password characters normally do not appear while you type.

After login, check where you are:

```bash
hostname
whoami
pwd
```

`hostname` should identify a CX3 login host, `whoami` should print your username, and `pwd` should print your current directory. The text before the cursor is the **shell prompt**; do not copy it as part of a command.

> 📌 **Login node rule:** Use the login node to manage files, read text and submit jobs. Run CRYSTAL23 through PBS on compute nodes.

## 3. Learn the commands used in this handbook

Start with commands that only display information:

```bash
pwd                  # show the current directory
ls                   # list names in the current directory
ls -lah              # include hidden files, sizes and dates
ls -rtl              # list oldest to newest; the newest file is last
ls -1 *.out          # list .out files, one per line
```

Move between directories:

```bash
cd /path/to/project  # go to an absolute path
cd ..                # go up one directory
cd ~                 # return to your home directory
```

Create and copy files:

```bash
mkdir -p ~/crystal23-training/first_job
cp example.d12 example_backup.d12
mv old_name.d12 new_name.d12
```

`cp` leaves the source in place. `mv` renames or moves it. `rm` deletes files from the command line and may not provide an easy way to recover them, so it is not needed in the exercises below.

### Paths with spaces

Put a path in quotes when it contains spaces:

```bash
cd "My Project/first calculation"
```

Press `Tab` to complete a partly typed path. Press the up arrow to recall recent commands.

## 4. Inspect a file before editing it

Use `less` for an output or any file you only need to read:

```bash
less calculation.out
```

Inside `less`:

| Key | Action |
| --- | --- |
| `Space` | Move down one page |
| `b` | Move up one page |
| `/SCF` then `Enter` | Search forward for `SCF` |
| `n` | Go to the next match |
| `G` | Go to the end |
| `q` | Quit |

Use `cat` only for a short file:

```bash
cat short-note.txt
```

## 5. Edit a copied input

Make a backup first, then open the working copy:

```bash
cp training.d12 training_before_edit.d12
vi training.d12
```

The minimum `vi` commands are:

| Key | Action |
| --- | --- |
| `i` | Start inserting text |
| `Esc` | Return to command mode |
| `gg` | Go to the first line |
| `G` | Go to the last line |
| `$` | Go to the end of the current line |
| `x` | Delete the character under the cursor |
| `r1` | Replace the character under the cursor with `1` |
| `dgg` | Delete from the current line to the start of the file |
| `dG` | Delete from the current line to the end of the file |
| `:wq` then `Enter` | Save and quit |
| `:q!` then `Enter` | Quit without saving |

After saving, compare the two files:

```bash
diff -u training_before_edit.d12 training.d12
```

No output from `diff` means the files are identical. Lines beginning with `-` come from the old file; lines beginning with `+` come from the new file.

## 6. Understand PBS and local wrappers

PBS is the scheduler. It accepts a resource request, waits for suitable compute nodes and runs the job there. A plain PBS workflow uses:

```bash
qsub job.qsub
qstat -u "$USER"
```

CX3 research groups may provide a wrapper named `qcry23` that creates and/or submits the PBS job for CRYSTAL23. First check which commands are available:

```bash
command -v qcry23
command -v qsub
command -v qstat
```

If `qcry23` prints a path, use the current group instructions to confirm its arguments. A project note recorded this form:

```bash
qcry23 EXP.d12 64 1:00
```

Here `EXP.d12` is the input. Do not assume that `64` and `1:00` have the same meaning in every installation; confirm the current core-count and wall-time format from a working group example before submitting.

If your group supplies a `.qsub` file instead, read it and submit it directly:

```bash
less EXP.qsub
qsub EXP.qsub
```

The submission command should print a job ID. Record it immediately.

## 7. Follow the job

Use your username to show only your jobs:

```bash
qstat -u "$USER"
```

If you know the job ID, request its entry directly:

```bash
qstat <job-id>
```

Common queue states include `Q` for queued and `R` for running. When the job disappears from `qstat`, it may have completed, failed or been deleted. The queue alone does not tell you which occurred.

Return to the run directory and inspect the newest files:

```bash
pwd
ls -rtl
ls -1 *.out
tail -n 40 EXP.out
```

If the output name differs, use the name shown by `ls`. To watch a growing output:

```bash
tail -f EXP.out
```

Press `Ctrl-C` to stop watching. This does not stop the PBS job.

Search for likely completion or failure messages:

```bash
grep -n -i "converg\|error\|maxcycle" EXP.out
```

The line numbers help you reopen the relevant area with `less`. The exact CRYSTAL wording varies, so always read the surrounding lines.

## 8. Reuse commands carefully

This command searches your shell history:

```bash
history | grep qcry
```

In many shells, `!qcry23` reruns the latest history entry beginning with `qcry23`. It does not mean “submit the previous file”. Because it can immediately submit a job with old arguments, beginners should recall the command with the up arrow, inspect it and edit it before pressing `Enter`.

To stop a job after checking its ID:

```bash
qdel <job-id>
```

Keep the partial output and write down why you stopped it.

## ✅ Terminal checkpoint

Before starting the first CRYSTAL23 exercise, make sure you can complete each item:

- [ ] Log in and confirm the host with `hostname`
- [ ] Use `pwd`, `ls` and `cd` without losing track of the directory
- [ ] Copy an input and inspect the change with `diff -u`
- [ ] Open and leave `less`
- [ ] Identify whether your group uses `qcry23`, a supplied `.qsub`, or both
- [ ] Submit one test job and record its job ID
- [ ] Find the output and distinguish queue completion from CRYSTAL convergence

## 🚀 Next step

Continue to [Your first CRYSTAL23 job](02-first-crystal23-job.md). It turns these commands into one complete, repeatable calculation.

## References

[^1]: Imperial College London ICT. (n.d.). *Unified Access*. https://www.imperial.ac.uk/admin-services/ict/self-service/connect-communicate/remote-access/unified-access/
