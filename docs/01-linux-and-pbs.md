# Working on CX3

This page contains the small set of terminal commands used repeatedly in the project.

## What you will learn

You will practise the commands needed to reach a project directory, inspect a file, create a new version and submit a job. The commands are deliberately shown one at a time so that you can see what each one does.

## Connect to Imperial and CX3

When working off campus, follow Imperial's [Unified Access instructions](https://www.imperial.ac.uk/admin-services/ict/self-service/connect-communicate/remote-access/unified-access/). Students may need the ICT Service Desk to enable access.

Open a terminal and log in with your own username:

```bash
ssh your_username@login.cx3.hpc.ic.ac.uk
```

After login, confirm the current location:

```bash
pwd
```

Replace `your_username` with your Imperial username.

## Move through the project

```bash
cd /path/to/project
pwd
ls -rtl
```

- `cd` changes directory.
- `pwd` prints the current directory.
- `ls -rtl` lists files by modification time, with the newest files at the bottom.

To list only CRYSTAL output files:

```bash
ls *.out
```

## Create, copy and rename

```bash
mkdir Tutorials
cd Tutorials
mkdir LiF
```

Copy an existing input before changing it:

```bash
cp EXP.d12 OPT0.d12
```

Rename a file without changing its content:

```bash
mv old_name.d12 new_name.d12
```

Compare two versions:

```bash
diff EXP.d12 OPT0.d12
```

No output from `diff` means the files are identical.

## Read and edit text files

Open a file for editing:

```bash
vi OPT0.d12
```

The minimum `vi` commands are:

| Key | Action |
| --- | --- |
| `i` | Insert text |
| `Esc` | Leave insert mode |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |

Display a short file:

```bash
cat OPT0.qsub
```

Open a long output for reading:

```bash
less OPT0.out
```

Press `q` to leave `less`.

## Submit and monitor

The project used `qcry23` to create and submit a CRYSTAL job:

```bash
qcry23 HF.d12 24 1:00
```

This is the command recorded in the project notes. The core count and walltime are calculation-specific and should be confirmed before reuse. Other completed qsub files requested 64 cores and a two-hour walltime, which shows why the values must remain tied to the run record.

Check your jobs:

```bash
qstat -u $USER
```

Submit an existing PBS script:

```bash
qsub OPT0.qsub
```

Stop a job only after checking its job ID:

```bash
qdel 1234567
```

`1234567` is an example. Replace it with the job ID shown by `qstat`.

## After submission

Use these commands separately:

```bash
qstat -u $USER
```

```bash
ls -rtl
```

```bash
ls *.out
```

The commands are shown in separate blocks because each answers a different question: whether the job is queued, which files changed, and which CRYSTAL outputs exist.

## Checkpoint

You are ready for the next page when you can answer these questions without guessing:

- Which directory am I in?
- Which input will be submitted?
- Which command creates the PBS job?
- Which command shows my job?
- Which file will I inspect after the job ends?

## Next

Continue to [Creating and submitting a calculation](02-first-crystal23-job.md).
