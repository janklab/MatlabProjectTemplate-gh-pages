---
title: Releasing
---

## Creating releases for your project

Any nontrivial project that's intended to be shared with other people should create releases of its software. These are distributions of specific states of your software, identified by version numbers, and typically bundled for easy downloading. Making releases means that your users can download stable, known-good (or at least hoped-good!) versions of your package, instead of just cloning your repo and getting whatever the current state of development is, which may well be buggy or incomplete.

## Choosing a versioning scheme

I highly recommend that you use [Semantic Versioning](https://semver.org/) for your versioning scheme. This is what GitHub and MathWorks File Exchange recommend, too.

For under-development code or prerelease software (such as alpha or beta releases), stick a `+` or `-<note>` suffix after your `x.y.z` version number. The `+` suffix in `x.y.z+` means "work done after version `x.y.z`". A `-` suffix indicates a prerelease for that release; i.e. `x.y.z-beta1` means the beta1 prerelease for version `x.y.z`. The `+` technique is easier for simple projects; the `-` technique is more powerful for complex projects.

## Release support in MatlabProjectTemplate

MatlabProjectTemplate contains support for marking releases in Git, building release distribution files ("tarballs" and Matlab Toolbox files), and publishing releases on GitHub using GitHub Releses.

The `doc-project/Release Checklist.md` file in the template describes how to do a release. The `dev-kit/make_release` script will automate most of the process of doing a release, including safety checks. Modify them to suit your needs, of course.

## Publishing to MathWorks File Exchange

I _strongly_ recommend that if you publish your project to File Exchange, you do so by:

* Linking your File Exchange post to your GitHub repo instead of directly uploading files, and
* Using their new Release-driven GitHub linkage. (This is what File Exchange themselves recommend, too.)

If you see File Exchange giving you a choice, and one of the choices has a bunch of green checkmarks and the other one doesn't, choose the one with all the green checkmarks.
