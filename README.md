# MPI Scatter and Gather Program

## Aim

To write and execute an MPI program that demonstrates the use of **MPI_Scatter()** and **MPI_Gather()**.

## Description

This program uses 4 MPI processes.

* Process 0 creates an array containing `1, 2, 3, 4`.
* `MPI_Scatter()` distributes one value to each process.
* Each process multiplies its received value by `2`.
* `MPI_Gather()` collects the processed values back into Process 0.
* Process 0 displays the final gathered values.

## Input

The program does not require user input.

The initial array is:

```text
1 2 3 4
```

## Working

### Step 1: Initialize MPI

```c
MPI_Init(&argc, &argv);
```

Starts the MPI environment.

### Step 2: Get Process Information

```c
MPI_Comm_rank(MPI_COMM_WORLD, &rank);
MPI_Comm_size(MPI_COMM_WORLD, &size);
```

* `rank` identifies the current process.
* `size` gives the total number of processes.

### Step 3: Create Data

Process 0 creates:

```text
1 2 3 4
```

### Step 4: Scatter

```c
MPI_Scatter(data, 1, MPI_INT, &recv, 1, MPI_INT, 0, MPI_COMM_WORLD);
```

The data is distributed among the 4 processes:

```text
Process 0 → 1
Process 1 → 2
Process 2 → 3
Process 3 → 4
```

### Step 5: Process the Data

Each process multiplies its value by 2:

```text
1 × 2 = 2
2 × 2 = 4
3 × 2 = 6
4 × 2 = 8
```

### Step 6: Gather

```c
MPI_Gather(&recv, 1, MPI_INT, data, 1, MPI_INT, 0, MPI_COMM_WORLD);
```

The results are collected by Process 0:

```text
2 4 6 8
```

## Compilation

Open PowerShell and go to the project folder:

```powershell
cd "C:\Users\Karthik R\Downloads\pc lab"
```

Compile the program:

```powershell
gcc 8.c -o 8.exe -I"C:\Program Files (x86)\Microsoft SDKs\MPI\Include" -L"C:\Program Files (x86)\Microsoft SDKs\MPI\Lib\x64" -lmsmpi
```

## Execution

Run the program using 4 MPI processes:

```powershell
mpiexec -n 4 .\8.exe
```

## Expected Output

```text
Process 0 received 1
Process 1 received 2
Process 2 received 3
Process 3 received 4
Gathered values: 2 4 6 8
```

The order of the `Process` output lines may vary because MPI processes execute independently.

## MPI Functions Used

| Function          | Purpose                  |
| ----------------- | ------------------------ |
| `MPI_Init()`      | Starts MPI               |
| `MPI_Comm_rank()` | Gets process rank        |
| `MPI_Comm_size()` | Gets number of processes |
| `MPI_Scatter()`   | Distributes data         |
| `MPI_Gather()`    | Collects data            |
| `MPI_Finalize()`  | Terminates MPI           |

## Result

The MPI program was successfully executed using 4 processes. `MPI_Scatter()` distributed the input values, each process doubled its value, and `MPI_Gather()` collected the results as:

```text
2 4 6 8
```
