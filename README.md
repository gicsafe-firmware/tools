# Tools
Files related to development tools 

## Contents

- [Uncrustify](#uncrustify)
- [Static Code Analyzers](#static-code-analyzers)
- [Ceedling](#ceedling)
- [Deploy](#deploy)
- [Doxygen](#doxygen)
- [Git](#git)
------------------------------------------------------------------------------
## Uncrustify
### Running the program
Here are ways to run it:
```bash
# simple
$ uncrustify -c uncrustify.cfg module/*.h -l c

# with backup
$ uncrustify -c uncrustify.cfg module/*.h -l c --replace

# without backup
$ uncrustify -c uncrustify.cfg module/*.h -l c --no-backup
```
The `-c` flag selects the configuration file.

Alternatively multiple or single files that should be processed can be
specified at the command end without flags.
If the flag `--no-backup` is missing, every file saved with the initial
name and an additional suffix (can be changed with --suffix).

For more options descriptions call:
```bash
$ uncrustify -h
```
Or [Uncrustify official](https://github.com/uncrustify/uncrustify/blob/master/README.md#running-the-program)
### Some 3rd party tools
To ease the process a bit:
- [Universal Indent GUI](http://universalindent.sourceforge.net/) - A
  cross-platform graphical configuration file editor for many code
  beautifiers, including Uncrustify.
- [uncrustify_config](https://github.com/CDanU/uncrustify_config) - A web
  configuration tool based on Uncrustifys emscripten interface.
- [UncrustifyX](https://github.com/ryanmaxwell/UncrustifyX) - Uncrustify
  utility and documentation browser for Mac OS X

## Static code analyzers

## Ceedling
### Folder structure for Ceedling
Each module should be created according with the [template](https://github.com/gicsafe-firmware/tools/tree/master/ceedling/template), resulting in a structure like the following:
```bash
.
└── moduleUnderTest
    ├── build
    ├── inc
    │   └── module.h
    ├── project.yml
    ├── src
    │   └── module.c
    └── test
        ├── support
        └── test_module.c

```

### Creating a new module
The folder structure of the project should be like the following:
```bash
.
├── dimba
│   ├── dimba
│   ├── doc
│   ├── third-party
│   └── tools
├── dimbaUML
│   └── modelConcept
├── docs
├── templates
└── tools
    ├── analyzer
    ├── ceedling
    ├── deploy
    ├── doxygen
    ├── git
    └── uncrustify
```

So, when creating a new module a simple *cp* can fulfill the task (with some renaming afterwards). e.g.:
```bash
~dimba/dimba$ cp -r ../../tools/ceedling/template/moduleUnderTest/ ./newModule
~dimba/dimba$ cd newModule/
~dimba/dimba/newModule$ tree
.
├── build
├── inc
│   └── module.h
├── project.yml
├── src
│   └── module.c
└── test
    ├── support
    │   └── rkhcfg.h
    └── test_module.c

~dimba/dimba/newModule$ mv inc/module.h inc/newModule.h
~dimba/dimba/newModule$ mv src/module.c src/newModule.c
~dimba/dimba/newModule$ mv test/test_module.c test/test_newModule.c
~dimba/dimba/newModule$ tree
.
├── build
├── inc
│   └── newModule.h
├── project.yml
├── src
│   └── newModule.c
└── test
    ├── support
    │   └── rkhcfg.h
    └── test_newModule.c

```
Next, the individual files should be modified to replace every occurrence of the name _module_ for the new name _newModule_. e.g.:

replacing
```C
/**
 *  \file   module.c
 *  \brief  Implements the specifications.
 */
```
 for
```C
/**
 *  \file   newModule.c
 *  \brief  Implements the specifications.
 */
```
Likewise, in test_newModule.c but **also modifying the included header file module.h for newModule.h**
```C
/**
 *  \file   test_newModule.c
 *  \brief  Unit test for this module.
 */

/* -------------------------- Development history -------------------------- */
/*
 */

/* -------------------------------- Authors -------------------------------- */
/*
 *  RiGr  Rick Grimes  rick.grimes@twd.com
 */

/* --------------------------------- Notes --------------------------------- */
/* ----------------------------- Include files ----------------------------- */
#include "unity.h"
#include "newModule.h"
```

and in the header file, replacing
```C
/**
 *  \file   module.h
 *  \brief  Specifies this module.
 */

/* -------------------------- Development history -------------------------- */
/*
 */

/* -------------------------------- Authors -------------------------------- */
/*
 *  RiGr  Rick Grimes  rick.grimes@twd.com
 */

/* --------------------------------- Notes --------------------------------- */
/* --------------------------------- Module -------------------------------- */
#ifndef __MODULE_H__
#define __MODULE_H__
```
for
```C
/**
 *  \file   newModule.h
 *  \brief  Specifies this module.
 */

/* -------------------------- Development history -------------------------- */
/*
 */

/* -------------------------------- Authors -------------------------------- */
/*
 *  RiGr  Rick Grimes  rick.grimes@twd.com
 */

/* --------------------------------- Notes --------------------------------- */
/* --------------------------------- Module -------------------------------- */
#ifndef __NEWMODULE_H__
#define __NEWMODULE_H__
```

Of course, you also should complete the descriptions and modify the author in each file.

### Usage
```bash
$ cd module
$ ceedling test:module
```

## Deploy

## Doxygen
### Usage
```bash
$ cd docs
$ doxygen Doxyfile
```

## Git
