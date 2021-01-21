---
title: Automatic Package Initialization
---

Some Matlab packages will require initialization before they'll work, beyond just getting their M-code on the Matlab path. This could include adding Java JARs to the Matlab `javaclasspath`, loading native DLLs, discovering initial setting from their environment, and so on.

Matlab does not provide a mechanism for code outside Toolboxes to do load-time initialization, so MatlabProjectTemplate provides support for it using a trick that lets your library auto-initialize, with nothing required from your users besides getting your `Mcode/` on their path. It does require some work on your part, though.

## The trick

The trick is to use `Constant` class properties, object inheritance, and a couple initialization functions together to make the initializer code run whenever your code is used.

Here's how to do the trick:

Define an `initializePackage` function that does the low-level initialization (like path and javaclasspath setting). It must be coded with *no* dependencies on any of your package's other code. This function will run _once_ at package startup. Have it set an appdata to indicate that it has run, and short-circuit if it's called again after that initial call.

Define a `LibraryInitializer` class that calls your `initializePackage()` in its constructor.

Define `MyPackageBase` and `MyPackageBaseHandle` classes that will be base classes for all the other classes in your package. `MyPackageBaseHandle` inherits from `handle`; `MyPackageBase` does not. Both of them create a `LibraryInitializer` using `Constant` properties:

```matlab
  properties (Constant, Hidden)
    initializer = mycoolpackage.internal.LibraryInitializer;
  end
```

Then have all the other code in your package which depends on library initialization be implemented in classes which inherit, either directly or indirectly, from `MyPackageBase` or `MyPackageBaseHandle`.

If you supply functions as part of your package, they need to be written as wrappers that call static methods on classes that inherit from `MyPackageBase(Handle)`, and have the actual implementation code live in those static methods.

Then, define a `globals` class and a `Settings` class. The `Settings` class holds all your package-wide run-time settings, and must inherit from `handle`. Define a static `Settings.discover()` method which discovers your default settings from the environment. And then add this to `globals`:

```matlab
  properties (Constant)
    % Global settings for mycoolpackage.
    settings = mycoolpackage.Settings.discover
  end
```

We split this discovery stuff out from the low-level initialization in `initializePackage` so that your package can survive a `clear classes` and automatically rediscover its default settings after `clear classes` happens. The `initializePackage` code only runs once at package first use time; the `Settings` code needs to run again _automatically_ each time a `clear classes` happens.

All this code should go in your `+internal` subpackage, except for `globals` and `Settings`, which go in your top-level package, because those are user-visible.

## Sheesh, that's a lot!

Yep. Sorry. But I haven't come up with a better way of doing it yet.

## Toolboxes

This isn't needed for Matlab Toolboxes, because they have hooks for startup code to run when the Toolbox is loaded. But you don't want your code to run _only_ as a Toolbox, do you? That would mean you needed to do a build and install step every time you changed your code and wanted to test it out! Not acceptable. So use this auto-initialization trick instead of Toolbox startup code.
