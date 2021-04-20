
1. `genbox`. The program asks for an input file. Here, one has to answer
`cbox.box`. `genbox` produces a binary file `box.re2` which has to be renamed
as `cbox.re2` with `mv box.re2 cbox.re2`.

2. The program `genmap` creates the `cbox.ma2` file which is a binary file
containing the map of elements for MPI ranks. `genmap` queries the user for an
input. Here, one has to answer `cbox`. The input file is the `cbox.re2` file.
Afterwards, the program also queries a number characterizing the quality of the
mesh ("mesh tolerance", default = 0.2, smaller gives a better mesh).

3. The main program is compiled with the command `makenek`.

4. The simulation can be launched with different commands like `nekmpi` (or
`nekbmpi`, for running in backgrand) with:

```bash
nekmpi cbox 2
```
