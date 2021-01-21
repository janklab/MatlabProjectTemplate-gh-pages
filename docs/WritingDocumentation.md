---
title: Writing Documentation
---

This page describes how to author documentation for your project using MatlabProjectTemplate.

TODO: Fill me in

## Using GitHub Pages

MatlabProjectTemplate provides support for publishing your project's documentation to GitHub Pages. This provides a special Jekyll configuration that's compatible with GitHub Pages. To use this, select `gh-pages` as your `DOCSITETOOL` when initializing the repo.

Using GitHub Pages is convenient for small projects, but it doesn't work well for large projects: the themes and plugin limitations in GitHub Pages means it's okay for small sites, but not really suitable for the documentation of a larger project. Plus, GitHub Pages will only show the latest version of your doco. Really, the documentation for each specific version of your software should be available with that release (and maybe online, too), so users are always looking at documentation that's in sync with the code they're using.

For large or serious projects, we recommend you use the `jekyll` or `mkdocs` option for `DOCSITETOOL` and use it to build the local, version-specific documentation for your project, and put your project's GitHub Pages or other website in a separate repo.
