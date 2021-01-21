---
title: Motivation
---

Why does MatlabProjectTemplate exist?

Creating a nontrivial Matlab software project, especially one intended for distribution to other users, is hard. Matlab's a great tool, but its developer toolchain is kind of anemic, so Matlab projects need a fair amount of _stuff_ or plumbing to get working. MatlabProjectTemplate aims to provide that for you, and to establish a common way of doing it.

What it addresses:

* As a programming language, Matlab's missing some important software-engineeringy features (like logging and polymorphic display customization) that each project needs to fill in themselves.
* Working with library dependencies in Matlab is hard because there's not much language support for it and no real project manager.
* Matlab "libraries" traditionally don't provide any structure for incorporating them in other projects.
* These days, there's a bunch of useful (often free) services like Continuous Integration and web page publishing that are very useful for software projects, but they take some work to set up.
* Matlab doesn't provide hooks for package initialization, so you have to jump through some hoops to ensure the packages requiring initialization (beyond just getting their M-code files on the Matlab path) are done correctly.
* Matlab's Toolbox creating tool is broken for sharing between multiple users or multiple repo copies.

If you look on MathWorks File Exchange, most submissions use "just a pile of M-files and maybe a README" as their project structure. That's not great, even for small packages. And is maybe part of why no open source development community has sprung up. I'd like to see that happen, and maybe it would if it were easier to create and use Matlab packages. (Especially now that there's a cheap-ish [Matlab Home license] available!)
