# Creating and submitting a calculation

This page shows how to turn an existing CRYSTAL input into a traceable CX3 job.

## What you will learn

You will make a working copy of an input, inspect the generated qsub file, submit one job and record enough information for another student to find the same result.

## 1. Go to the calculation directory

```bash
cd /path/to/project
pwd
ls -rtl
```

Check the printed path before editing or submitting anything.

## 2. Create the next input

The project notes record a first calculation created from an existing LiF input. Keep the source and make a new working file:

```bash
cp lif.d12 HF.d12
```

Edit the copy:

```bash
vi HF.d12
```

Compare it with its source:

```bash
diff lif.d12 HF.d12
```

The difference should match the purpose of the new calculation. If several unrelated sections changed, stop and check the input before submission.

## 3. Submit with `qcry23`

```bash
qcry23 HF.d12 24 1:00
```

This command is the recorded small-job example. In the completed project, other runs produced matching qsub files with different resource requests. The resource values are part of the calculation record, not universal defaults.

Inspect the generated script:

```bash
cat HF.qsub
```

The important links are:

```text
#PBS -N HF
...
runcryP HF
```

The PBS job name, executable argument and `.d12` base name should agree.

## 4. Record the PBS job

```bash
qstat -u $USER
```

Record the job ID. The finished calculation may contain scheduler files such as:

```text
HF.o1234567
HF.e1234567
```

`1234567` is an example job ID. Replace it with the number returned by PBS. These names connect the scheduler record to the submitted calculation.

## 5. Check the returned files

After the job leaves the queue:

```bash
ls -rtl
```

```bash
ls HF*
```

For the completed optimisation, the file set included `.d12`, `.qsub`, `.out`, scheduler logs, wavefunction files and structure outputs. The exact set depends on the calculation.

Read the PBS error file if it contains text:

```bash
cat HF.e1234567
```

Use the actual job number in the filename.

Then check the CRYSTAL output using the procedures in the next two pages. A job leaving the queue does not prove that the calculation converged.

## Checkpoint

Before continuing, your directory should contain the input, qsub file, scheduler record and CRYSTAL output. You should also know the job ID and be able to state whether the input was a new version of an earlier calculation.

## Submission record

Keep this information with the calculation:

```text
Calculation:
Parent input:
Change made:
Submission command:
PBS job ID:
CRYSTAL output:
Status:
Next calculation:
```

## Next

Continue to [Reading a CRYSTAL23 input and output](03-reading-input-and-output.md).
