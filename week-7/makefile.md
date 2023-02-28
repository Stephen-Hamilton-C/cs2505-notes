# Making Makefiles
Stephen Hamilton
2-28-2023

- [Making Makefiles](#making-makefiles)
  - [Structure](#structure)
    - [all](#all)
    - [project1](#project1)
    - [main.o and zipData.o](#maino-and-zipdatao)
    - [package](#package)
    - [clean](#clean)


Makefiles are a really convenient tool for building your C projects.
Rather than having to type out
`gcc -g -lm -std=gnu11 -o project1 main.c zipData.c zipData.h`
every time you want to compile project 1,
you could just write a Makefile once and then run the `make` command.

## Structure
Makefiles are composed of three things:
- Targets
- Dependencies
- Rules

Targets tell `make` what set of dependencies and rules to use.
Dependencies are other targets that a target needs before it can run.
Rules are a list of commands for `make` to run.

This sounds really confusing without looking at a Makefile, so let's look at my Makefile from Project 1:
```makefile
GCC_OPTS = -Wall -Wextra -Werror -std=gnu11 -lm

all: project1

project1: main.o zipData.o zipData.h
	gcc -lm -o project1 main.o zipData.o

main.o: main.c
	gcc ${GCC_OPTS} -c main.c

zipData.o: zipData.c
	gcc ${GCC_OPTS} -c zipData.c

package: main.c zipData.h zipData.c
	tar -cvf project1.tar main.c zipData.h zipData.c

clean:
	rm *.o
	rm project1
```

### all
This is a lot, so let's take it piece by piece. Let's start with this bit:
```makefile
all: project1
```
`all` is the target, and `project1` is the dependency.
Every Makefile *usually* starts with an `all` target and 
its dependencies are the executables that can be built.
This target is what is run when you run the `make` command without any arguments.

In this case, the only executable we want to build is `project1`, so that is the only dependency for `all`.

### project1
Let's look at the next target:
```makefile
project1: main.o zipData.o zipData.h
    gcc -lm -o project1 main.o zipData.o
```
Here, `project1` is the target, and `main.o`, `zipData.o`, `zipData.h` are dependencies.
This will be explained later, but `zipData.h` is actually not a target, but a file.
Files can be used as dependencies.
This will simply tell `make` that the target needs to be run if the file
has been changed since it was last run.
However, `main.o` and `zipData.o` are indeed targets, described later in the Makefile.

Underneath the target is a single command.
This is the target's **rules**.
Rules are, as explained earlier, a list of commands.
For `project1`, this is only one command - the linking command.
It links the object files into the project1 executable.

These rules will only be run if the dependencies needed to run or have changed.

### main.o and zipData.o
Let's look at the next two targets:
```makefile
main.o: main.c
	gcc ${GCC_OPTS} -c main.c

zipData.o: zipData.c
	gcc ${GCC_OPTS} -c zipData.c
```
Here, the target `main.o` depends on the file `main.c`.
So, if `main.c` was changed since the last time `main.o`,
then the rules for `main.o` will be run.

The command here is just the compile step, indicated by the `-c`,
which generates object files to be linked later.
The linking is done in the `project1` target.

The `${GCC_OPTS}` is a bash variable.
You can see its declaration at the top of the Makefile.
Basically, bash variables will inject text into wherever you dereference them.
This allows you to easily change compiler options without having to change it
in multiple places.

### package
Let's take a look at this target:
```makefile
package: main.c zipData.h zipData.c
	tar -cvf project1.tar main.c zipData.h zipData.c
```
This doesn't do any compiling,
and in fact is not a dependency of any of the other targets.
So, in order for this target to run,
it must be explicitly called with `make package`.
All this target does is put the three files into a tar file for submission.

So, Makefiles can not only compile your code,
but also make shortcuts for common tasks that you might run in your project.

### clean
Most Makefiles have this target at the end:
```makefile
clean:
	rm *.o
	rm project1
```
This target simply deletes any build artifacts -
or anything created by the compiling or linking commands. 
