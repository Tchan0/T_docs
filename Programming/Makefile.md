# Makefiles

Used to automate the compilation of applications

## Variables
```
VAR1 = /path/to/bin
export VAR2 = /path/to/file.txt
export VAR3 = $(shell du -sb ${VAR2} | cut -f1)
```
* TODO: use: $(foo)

## Rules
* generic layout:
```
target: dependency
<tab> command1
<tab> command2
```
* If 'make' is invoked without arguments, the first target will be executed

* .PHONY is used for target names that are not the names of a real file, to be sure the rule is executed, even if by accident a file with that same target name exists in the folder, and is unmodified
```
.PHONY : clean
clean: rm-elf
```
* TODO: include ../Makefile.cfg

* TODO: Macros can be defined on the command line.
– E.g. make DEBUG_FLAG=-g

## Pre-defined macros
* “make -p” to display a listing of all the macros, suffix rules and targets in effect for the current build.
* current target name: $@
* 1st prerequisite: $<
* list of the prerequisites: $^


## Example
```
# Filename of the output binary
TARGET = main

# .c files to be compiled, converted to ".o"
OBJS = $(basename $(TARGET)).o

# LIBS to be included when linking
# LIBS = -lgl

.PHONY : all
all: rm-target $(TARGET)

.PHONY : clean
clean: rm-objs rm-target

.PHONY : rm-objs
rm-objs:
	-rm -f $(OBJS)

.PHONY : rm-target
rm-target:
	-rm -f $(TARGET)

$(TARGET): $(OBJS)
	gcc -o $(TARGET) $(OBJS) $(LIBS)

%.o: %.c
	cc $(CFLAGS) -I$(C_INCLUDE_PATH) -c $< -r -o $@

.PHONY : asm
asm: $(TARGET)
	objdump -d -S $(TARGET) > $(TARGET).asm

.PHONY : dist
dist: $(TARGET) rm-objs
	strip $(TARGET)
```

## References
* [Make](https://en.wikipedia.org/wiki/Make_(software))
* [GNU Make](https://www.gnu.org/software/make/manual/html_node/)
* [A Short Introduction to Makefile](https://www3.nd.edu/~zxu2/acms60212-40212/Makefile.pdf)
