---
title: Project Layout
---

## Overview

Once you have initialized your project from the template (using `./init_project_from_template.sh`), you'll have a directory structure that looks like this:

```text
├── CHANGES.txt
├── LICENSE
├── Makefile
├── MatlabProjectTemplate/
├── Mcode/
│   └── +mycoolpackage/
│       ├── +examples/
│       ├── +internal/
│       ├── +logger/
│       ├── +test/
│       ├── Settings.m
│       └── globals.m
├── MyCoolProject.prj.in
├── README.md
├── VERSION
├── azure-pipelines.yml
├── .circleci/
├── .travis.yml
├── build/
├── dist/
├── dev-kit/
├── docs/
├── doc/
├── doc-project/
│   ├── Description for File Exchange.txt
│   ├── Developer Notes.md
│   ├── Release Checklist.md
│   └── TODO.md
├── examples/
├── info.xml
├── lib/
│   ├── java/
│   └── matlab/
├── mycoolpackage_toolbox_info.m
├── project_settings.sh
└── src/
    ├── c/
    └── java/
```

The main bits are:

* `Mcode/` – Your Matlab source code goes here!
* `CHANGES.txt` – A [changelog](https://keepachangelog.com/en/1.0.0) for your project
* `LICENSE` – Documents the licensing terms for your project
* `Makefile` – Defines how your project is built
* `MatlabProjectTemplate` – Doco about MatlabProjectTemplate (not your project)
* `MyCoolProject.prj.in`, `info.xml`, `mycoolpackage_toolbox_info.m` – Config files for packaging your project as a Matlab Toolbox
* `VERSION` – Central record of what version your project is on
* `azure-pipelines.yml`, `.circleci`, `travis.yml` – Config files for [Continuous Integration](https://www.mathworks.com/solutions/continuous-integration.html) providers
* `build/` – Where your intermediate build products go
* `dist/` –  Where your final build products for distribution go
* `dev-kit/` – Developer tools for working on your project itself
* `docs/` – The _source_ for your project documentation
* `doc/` – Where your _generated_ project documentation goes
* `doc-project/` – Documentation for internal use by your project's developers
* `examples/` – Code examples to go with your project
* `lib/` – Third-party libraries you depend on
* `project_settings.sh` – Settings used to initialize your project from the template
* `src/` – Your non-Matlab custom source code

I'm really sorry for having both `doc` and `docs`; that's confusing. I had to use the name `docs` to be compatible with GitHub Pages. And `doc` is the only thing that makes sense to me for the final built documentation that goes into the distribution.

## Details

### `Mcode`

This is the core of your project: where your Matlab source code goes! This is what will end up on the Matlab path for people using your project.

### `Mcode/+mycoolpackage`

The top-level package for your project. All your code should go inside a package, to prevent name collisions with other people's code. This makes it feasible to use multiple projects in a Matlab environment.

The code that users of your package will use – that is, the public API of your package – goes directly in here. If you have a really large package, you might want to break it out in to subpackages.

### `Mcode/+mycoolpackage/+examples`

Example code that ships with your package. This is different from the top-level `/examples/` in that code here is stuff you want to always be available at run time when someone has your package loaded in to Matlab. The `/examples` stuff is more documentation-oriented, and the user has to pull that in separately.

### `Mcode/+mycoolpackage/+internal`

Code for internal use by your package. This is a safe space to put stuff that is not part of your public API, and is undocumented and subject to change at any time, and you don't want users calling directly.

### `Mcode/+mycoolpackage/+logger`

Support for [SLF4M](https://github.com/janklab/SLF4M)-compatible logging that's built in to your package. We do it this way so you don't have to take a dependency on SLF4M, because managing dependencies in Matlab is kind of a pain, and can lead to DLL Hell.

### `Mcode/+mycoolpackage/+test`

Your unit tests go here. You're going to write unit tests, right?

Author your unit tests using the [Matlab Unit Test Framework](https://www.mathworks.com/help/matlab/matlab-unit-test-framework.html).

### `Mcode/+mycoolpackage/globals.m`

Global state, settings, and info about your package. This is a central class to store an run-time settings and global state your package may have. It also allows clients of the package to programmatically query its version and location at run time.

`Mcode/+mycoolpackage/Settings.m` is a structure for your package's settings that lives in a field on `globals`. It has to be a separate class because Matlab doesn't support mutable static class properties, only immutable `Constant` ones. So we use the trick of defining a separate mutable `handle` class for the settings structure, and sticking that in a `Constant` field on `globals`.

### `MyCoolProject.prj.in` – Toolbox Packaging

The `MyCoolProject.prj.in`, `info.xml`, and `mycoolpackage_toolbox_info.m` files are used for packaging your project as a [Matlab Toolbox](https://www.mathworks.com/help/matlab/matlab_prog/create-and-share-custom-matlab-toolboxes.html).

The project definition is supplied as a `.prj.in` file instead of a `.prj` file, because Matlab bakes _absolute_ file paths into its `.prj` files when you use the Toolbox packager. This is a flaw that makes `.prj` projects unsuitable for sharing between multiple developers, or even for use in different repo locations or on different OSes by a single developer. So we define a `.prj.in` file and then munge it into a `.prj` file at each build time.

### `README.md`

Summary info about your project. This is what any user will read first. It should have a summary of what your project does, how to install and use it, a quickstart guide and maybe some examples, and links to where to get more info and help.

### `dev-kit`

These are the development tools for working with and building your project itself. They are for the internal use of your project's developers, and are not included in your package distribution.

Most of the stuff in here is used by calling `make` instead of running the scripts directly.

What's in `dev-kit`:

* `package_mycoolpackage_toolbox`, `batch_package_mycoolpackage_toolbox.m` – Code for packaging your project as a Matlab toolbox. Used by the `make toolbox` target.
* `build_mycoolpackage` – Does the build for distribution. Matlab isn't a compiled language, so there's no compile step required, but there is P-coding and maybe some other code munging stuff used to prepare M-code for distribution.
* `buildallmexfiles_in_mycoolpackage.m` – Just what it sounds like. Searches your `Mcode/` tree for MEX source files and compiles them all.
* `load_mycoolpackage.m` – Loads the package. This is just used for bootstrapping the package for stuff like `make build` or `make test` runs.
* `locate_matlab.sh` – Shell support for locating Matlab in environments where it's not on the `$PATH` by default. (That is, Macs.)
* `make_release` – Does a release of your package! Takes care of updating `VERSION`, doing tests and builds, and tagging your release in Git.

Building the MEX files is done manually by the developer at code authoring time, not as part of the package build process. This is because, unlike binary artifacts in many programming languages, MEX files should actually be kept in the source tree and checked in to the Git repo, so that your program can be run directly from the repo without going through a build step. Many users, and even many developers, may not have an environment capable of easily building MEX files.

### `dist/`

This is where the final packaged files ("release artifacts") for distribution show up. Your project's zip files and Matlab Toolbox `.mltbx` files will show up here.

### `doc/`

The built documentation for your project. This is what will be presented to your users, and is included in the distribution files.

You shouldn't edit files in here directly. They are generated from the doc source files in `docs/` by the `make doc` target.

See [Writing Documentation](WritingDocumentation.html) for more info.

I'm really sorry for having both `doc` and `docs` directories; that's confusing. I had to use the name `docs` to be compatible with GitHub Pages. And `doc` is the only thing that makes sense to me for the final built documentation that goes into the distribution.

### `docs/`

Source files for the project documentation. This is the stuff you should edit.

This contains Markdown, AsciiDoc, and other document formats used by Jekyll or mkdocs to build the stuff in doc.

See [Writing Documentation](WritingDocumentation.html) for more info.

### `doc-project/`

This is where you put internal developer-facing documentation for people working on your project itself. Things like code style guides, developer notes, a release checklist, and anything else documenting your development process go here.

### `examples/`

Code examples for presentation to your users.

Because examples are useful for inclusion in your documentation, this folder is automatically copied into `docs/` by the `make doc-src` target.

### `lib/`

Third-party libraries that your package depends on.

If your project has custom Java code, its JAR files will also go here, just as if it were an external library. (Because really, it kind of is.)

### `lib/java`

The `lib/java/` subdirectory contains Java libraries. Each Java library should be in a `lib/java/<libname>` subdirectory, with all its `.jar` files immediately in that `<libname>` subdirectory. If you're using MatlabProjectTemplate's automatic library initialization feature, all the jars in all the libs here will be automatically added to the Matlab `javaclasspath` for you.

### `lib/matlab`

External non-Toolbox Matlab libraries that you depend on and are redistributing with your package go here.

Each Matlab library should be in a `lib/matlab/<libname>` subdirectory here.

There's no standard layout or loading mechanism for non-Toolbox Matlab libraries (until now! 😉), so the package initialization code uses some heuristics to guess where the M-code in these libraries is located and get it on the Matlab path. Basically, if you take a submission from File Exchange, unzip it, and drop the resulting directory in here, it'll probably work.

### `lib/c`

C/C++ or other "native" libraries will go here.

I haven't defined any further structure for this directory or how its contents will be loaded when your package is initialized. You'll have to write custom library-loading code in your package initialization for now. Suggestions are welcome!

### `project_settings.sh`

This is the configuration file you edit before running `init_project_from_template.sh` to define your basic project properties and metadata. It's not used after that, so you can throw it away once your project is initialized, but I'd keep it around just in case, because I'm like that. Who knows, maybe you'll need to re-run the project initialization if MatlabProjectTemplate is improved over time?

### `src/`

This is all your project's custom source code in languages besides Matlab.

### `src/java`

Your project's custom Java code.

Your Java code is contained in a `MyCoolProject-java` directory here which contains a [Maven](https://maven.apache.org) project.

To build your Java code and install it in to your project's `lib/java`, run `make java` in your repo root, or cd in to `src/java/MyCoolProject-java`, run `mvn package`, and copy the resulting `.jar` file over manually.

Building your Java code should be done at code authoring time, not at project build time, because your M-code needs that JAR to run, and you should be able to run your code directly from the repo. For this same reason, the JAR for your custom Java code in `lib/java/MyCoolProject-java` _should_ be checked in to your Git repo.

### `src/c`

Source code for your C/C++ and other "native" libraries or programs will go here.

I haven't defined any further structure for this directory or how its contents will be built. You'll have to come up with your own solution and build files for now. Suggestions are welcome!
