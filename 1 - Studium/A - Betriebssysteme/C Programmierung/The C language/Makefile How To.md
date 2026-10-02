https://www.gnu.org/software/make/manual/make.html#Introduction


### 3.3 Including Other Makefiles


The `include` directive tells `make` to suspend reading the current makefile and read one or more other makefiles before continuing. The directive is a line in the makefile that looks like this:

include filenames…

filenames can contain shell file name patterns. If filenames is empty, nothing is included and no error is printed.

Extra spaces are allowed and ignored at the beginning of the line, but the first character must not be a tab (or the value of `.RECIPEPREFIX`)—if the line begins with a tab, it will be considered a recipe line. Whitespace is required between `include` and the file names, and between file names; extra whitespace is ignored there and at the end of the directive. A comment starting with ‘#’ is allowed at the end of the line. If the file names contain any variable or function references, they are expanded. See [How to Use Variables](https://www.gnu.org/software/make/manual/make.html#Using-Variables).

For example, if you have three .mk files, a.mk, b.mk, and c.mk, and `$(bar)` expands to `bish bash`, then the following expression

include foo *.mk $(bar)

is equivalent to

include foo a.mk b.mk c.mk bish bash

When `make` processes an `include` directive, it suspends reading of the containing makefile and reads from each listed file in turn. When that is finished, `make` resumes reading the makefile in which the directive appears.

One occasion for using `include` directives is when several programs, handled by individual makefiles in various directories, need to use a common set of variable definitions (see [Setting Variables](https://www.gnu.org/software/make/manual/make.html#Setting)) or pattern rules (see [Defining and Redefining Pattern Rules](https://www.gnu.org/software/make/manual/make.html#Pattern-Rules)).

Another such occasion is when you want to generate prerequisites from source files automatically; the prerequisites can be put in a file that is included by the main makefile. This practice is generally cleaner than that of somehow appending the prerequisites to the end of the main makefile as has been traditionally done with other versions of `make`. See [Generating Prerequisites Automatically](https://www.gnu.org/software/make/manual/make.html#Automatic-Prerequisites).

If the specified name does not start with a slash (or a drive letter and colon when GNU Make is compiled with MS-DOS / MS-Windows path support), and the file is not found in the current directory, several other directories are searched. First, any directories you have specified with the ‘-I’ or ‘--include-dir’ options are searched (see [Summary of Options](https://www.gnu.org/software/make/manual/make.html#Options-Summary)). Then the following directories (if they exist) are searched, in this order: prefix/include (normally /usr/local/include [1](https://www.gnu.org/software/make/manual/make.html#FOOT1)) /usr/gnu/include, /usr/local/include, /usr/include.

The `.INCLUDE_DIRS` variable will contain the current list of directories that make will search for included files. See [Other Special Variables](https://www.gnu.org/software/make/manual/make.html#Special-Variables).

You can avoid searching in these default directories by adding the command line option `-I` with the special value `-` (e.g., `-I-`) to the command line. This will cause `make` to forget any already-set include directories, including the default directories.

If an included makefile cannot be found in any of these directories it is not an immediately fatal error; processing of the makefile containing the `include` continues. Once it has finished reading makefiles, `make` will try to remake any that are out of date or don’t exist. See [How Makefiles Are Remade](https://www.gnu.org/software/make/manual/make.html#Remaking-Makefiles). Only after it has failed to find a rule to remake the makefile, or it found a rule but the recipe failed, will `make` diagnose the missing makefile as a fatal error.

If you want `make` to simply ignore a makefile which does not exist or cannot be remade, with no error message, use the `-include` directive instead of `include`, like this:

-include filenames…

This acts like `include` in every way except that there is no error (not even a warning) if any of the filenames (or any prerequisites of any of the filenames) do not exist or cannot be remade.

For compatibility with some other `make` implementations, `sinclude` is another name for `-include`.

