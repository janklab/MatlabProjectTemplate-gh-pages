---
title: Using on Windows
---

MatlabProjectTemplate mostly works out of the box on Windows. But some of its features don't, because base Windows lacks the Unix development tools 

## Building and previewing documentation

Unless you're using `gh-pages-raw` as your doc tool, the documentation build process requires Ruby/Bundler/Jekyll or mkdocs, which are oriented towards a Unix environment. These won't work out of the box.

You can install [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and manually do the previews and builds there, if you're familiary with Jekyll or mkdocs.

TODO: Figure out how to get these running on "plain" Windows, and document it.

## Building custom Java code

The custom Java code build process has two hitches on Windows: it requires Maven, which is a little tricky to install. And it can't be run while Matlab is running and has your library loaded, because Matlab locks `.jar` files which are loaded on the `javaclasspath`. So you need to the build externally using `make java`, and the `make` stuff doesn't work on plain Windows.

You can install [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and do the Java builds there using `make java`.

You can also do the Java build manually:

* Exit Matlab.
* Open the `src/java/myproject-java` Maven project in a Java IDE that supports Maven, like IntelliJ IDEA, Eclipse, or NetBeans.
* Rebuild the project.
* Copy the resulting `.jar` file in `src/java/myproject-java/target` to `lib/java/myproject-java`
* Restart Matlab.

TODO: Figure out how to do Java builds more easily on "plain" Windows, and document it.
