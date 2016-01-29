# Extract dependencies between fortran files

Fortran files can define "modules". If a file containing a module gets
compiled, this compilation process generates two files: a X.mod file and
a Y.o file. Here X is the name of the defined module, where Y is the input
file name. Note that a single file can even contain multiple modules.

Modules can also be referenced in Fortran code, think of it as a ``#include``
statement in C. If the module file does not exist, the code will not compile.

This creates the following problem: Assume you have a large number of Fortran
files and you would like to write a Makefile for compiling them. Now, you
cannot compile all .f90 files in a random order, because maybe when compiling
the file foo.f90 the compiler will complain that the module bar could not be
found. Now you need to search through your code for the definition of module
bar. This can be in a file named my_module.f90. Now you need to add a make-rule
that my_module.f90 must be compiled before foo.f90.

This perl script generates these rules for you. Just copy it into the source
directory and execute it using perl.
