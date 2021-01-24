---
title: MatlabProjectTemplate
---

[![Travis Build Status](https://travis-ci.com/janklab/MatlabProjectTemplate.svg?branch=main)](https://travis-ci.com/github/janklab/MatlabProjectTemplate)  [![CircleCI Build Status](https://circleci.com/gh/janklab/MatlabProjectTemplate.svg?style=shield)](https://circleci.com/gh/janklab/MatlabProjectTemplate) [![Azure Build Status](https://dev.azure.com/janklab/MatlabProjectTemplate/_apis/build/status/janklab.MatlabProjectTemplate?branchName=main)](https://dev.azure.com/janklab/MatlabProjectTemplate/_build/latest?definitionId=1&branchName=main) [![View MatlabProjectTemplate on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/85840-matlabprojecttemplate)

[MatlabProjectTemplate](https://github.com/janklab/MatlabProjectTemplate) ("MPT") is a template repo for creating Matlab library and application projects. It defines a "standard" project structure that should be suitable for many projects, including those intended for redistribution / open source. You can think of it as sort of a community-supported Reference Implementation for Matlab packages.

It is suitable for both libraries and applications, and includes coding and organizational conventions that make it safe to use this project's code in a Matlab environment that uses code from other projects, too. MPT follows [Janklab's](https://janklab.net) philosophy of treating Matlab as a serious programming language, instead of an overgrown interactive graphing calculator.

This template is based on the author's 20+ years of professionally building Matlab and other software, so it should be pretty good.

## Features

MatlabProjectTemplate supports the following features. You don't _have_ to use any of them; you can just ignore the ones you don't care about. But they're there if you need them!

* Collaboration between multiple developers
* Building [Matlab Toolboxes](https://www.mathworks.com/help/matlab/matlab_prog/create-and-share-custom-matlab-toolboxes.html)
* Matlab [Continuous Integration](https://www.mathworks.com/solutions/continuous-integration.html) and unit tests
* Distribution as both plain zip files and Matlab Toolbox `.mltbx` files
* Using ("vendoring") third-party Java JAR and Matlab libraries
* Writing nice documentation
* Custom Java code
* Library initialization
* _Automatic_ library initialization
* Logging, in an [SLF4M](https://github.com/janklab/SLF4M)/SLF4J/Log4j-compatible manner

## Usage

To create a new project from this template, go to [its repo on GitHub](https://github.com/janklab/MatlabProjectTemplate) and create a new repo by clicking the green "Use this template" button.

NOTE: Don't "fork" or "clone" the MatlabProjectTemplate repo. That will leave your project's Git repo set up wrong! Do the "Use this template" thing.

Then:

* Add a license file!
* Edit the variables `project_settings.m`.
* Run `init_project_from_template.m` in Matlab.
* Edit `.editorconfig` to reflect your preferred code style.
* Edit `<myproject>.prj.in` and put in all your contact and descriptive info and other stuff.

And then:

* Put your main Matlab source code in `Mcode/`.
* Put your example scripts in `examples/`.
* Edit the files in `doc-project` to reflect your plans.
* Hack away!

When you're developing code for your project, you should add the `dev-kit/` directory to your Matlab path.

See the [User Guide](UserGuide.md) for more information and details.

## Requirements

Just Matlab, for most of it.

Some features (some doc building/previewing, and custom Java code builds) only work on Mac and Linux. But don't worry! If you're on Windows, you can install [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and use that.

See [Using on Windows](Windows.html) for details.

## Unit tests

You should write unit tests for your project! Use the [Matlab Unit Test Framework](https://www.mathworks.com/help/matlab/matlab-unit-test-framework.html) and put your tests in `Mcode/+<myproject>/+test`. Run them with `make test` in the shell or with `dev-kit/launchtests.m` in Matlab.

## License

MatlabProjectTemplate is multi-licensed under all of: MIT License, BSD 2-Clause License, Apache License, and GPLv3. You can use it in any project with a license compatible with any of those licenses. This includes commercial and proprietary software.

If you have a licensing scenario which is not covered by the above (and jeez, what are you doing that would require _that_?), just contact me, and I'll probably add support for it. My intention is that _everybody_ can use MatlabProjectTemplate.

## More info

* [Motivation](Motivation.html)
* [User Guide](UserGuide.html)
* [Project Layout](ProjectLayout.html)
* [Writing Documentation](WritingDocumentation.html)
* [Creating Releases](Releasing.html)
* [Automatic Package Initialization](AutoInitialization.html)
* [FAQ](FAQ.html)

## About MatlabProjectTemplate

MatlabProjectTemplate was written by [Andrew Janke](https://apjanke.net). The project has a [web site](https://matlabprojecttemplate.janklab.net) and you can find a [repo on GitHub](https://github.com/janklab/MatlabProjectTemplate). You can get support, or even contribute to the project, there. Bug reports, feature requests, and other feedback are welcome.

MatlabProjectTemplate is part of the [Janklab](https://janklab.net) suite of libraries for Matlab.
