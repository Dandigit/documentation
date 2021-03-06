## Recipe file

A C2 project requires a `recipe` file (named *recipe.txt*). This file specifies:

* the target type (executable, shared library or static library)
* which options are used (compile time flags)
* which source files are used
* external dependencies

The recipe is written by the developers, but for big projects, the file could
be generated (for example by `make menuconfig`), especially if there are many
different configurations.

The exact format of the recipe file is still in progress, but it currently looks like:

```ini
# an example recipe file

executable hello
  $warnings no-unused
  sources/hello.c2
end

lib graphics static
  $export api
  sources/file1.c2
  file2.c2
  api/file3.c2
end
```
Note that the path to each c2 file is relative to the position of the __recipe file__, not
to that of the c2c binary.

### Target options

Inside a target, the following options are available:

 * *config [names]* - specify definitions for the preprocessor, like #define feature1
 * *export [modules]* - export the modules in libraries and generated headers
 * *generate-c* - enable generation of C code
 * *generate-ir* - enable generation of LLVM IR code
 * *warnings [list]* - enable/disable specific warnings during compilation
 * *deps [options]* - enable generation of dependency file with certain options
 * *refs* - generate reference file (used for jumping to definition)
 * *use [libs]* - depend on given libraries


