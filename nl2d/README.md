# Minimal example

## Compulsory files

Running a simulation requires 4 compulsory files:

### case.box

This file contains the number of dimension, number of fields, elements in each
direction, boundary condition.

With a minus sign behind the number of dimensions, we do not need any further
file. If the file does not have the minus sign here, it requires a #.rea file
which we define the name on the first line of this file.

A minus sign behind the number of elements, means we want a uniform spacing
between elements.

### case.par

In this file we define the parameters for running the simulation such as type
of problem (incompressible Navier-Stokes, low-Mach Navier-Stokes, etc) and so
on.

### case.usr

This file contains Fortran code with user-defined subroutines which can be used
by Nek5000 to define specific initial conditions, boundary conditions, output
and so on.

### SIZE

The size of the problem is specified in this file. It contains the order of
polynomial, total number of elements, number of processors, and so forth.

## Compile and launch

1. The program `genbox` can be built by doing:

    ```bash
    cd Nek5000/tools
    ./maketools genbox
    ```

    Then, one can launch it with the command `genbox`. The program asks for an
    input file. Here, one has to answer `cbox.box`. `genbox` produces a binary
    file `box.re2` which has to be renamed as `cbox.re2` with `mv box.re2 cbox.re2`.

2. The program `genmap` creates the `cbox.ma2` file which is a binary file
containing the map of elements for MPI ranks. `genmap` queries the user for an
input. Here, one has to answer `cbox`. The input file is the `cbox.re2` file.
Afterwards, the program also queries a number characterizing the quality of the
mesh ("mesh tolerance", default = 0.2, smaller gives a better mesh).

3. The main program is compiled with the command `makenek`.

4. The simulation can be launched with different commands like `nekmpi` (or
`nekbmpi`, for running in backgrand) with:

```bash
nekmpi cbox 4
```

The first argument is the case name and the second the number of processors.

## Clean all files:

```bash
make clean
rm  -f cbox.ma2  cbox.re2  makefile build.log
```

## Visualization

One needs to initialize the 3D visualization with `visnek cbox`. This program
produces something like the following output:

```raw
 Found 66 field file(s)
 Generating metadata file cbox.nek5000 ...

 Now run visit -o cbox.nek5000 or paraview --data=cbox.nek5000
```
