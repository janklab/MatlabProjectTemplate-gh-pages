---
title: User Guide
---

## Starting a project

To create a new project using MatlabProjectTemplate, go to [the GitHub repo](https://github.com/janklab/MatlabProjectTemplate) and click the green "Use this template" button near the upper right of the page.

Name your new repo after your project name. This will be visible to your end users, so pick a good name!

Once the new repo is created, clone it to your local machine, and edit the `project_settings.sh` file to define your project's basic properties and metadata.

Then open Matlab, `cd` to the repo, and run `init_project_from_template`.

Have a look around the modified source tree, and if things look good to you, commit the changes with `git add -A; git commit -a -m 'Project initialization from MatlabProjectTemplate` and do a `git push`.

You're ready to start developing! Next steps:

* Put your main Matlab source code in `Mcode/`.
* Put your example scripts in `examples/`.
* Edit the files in `doc-project/` to reflect your plans.
* Hack away!

## What not to do

Do not _fork_ the MatlabProjectTemplate repo. That will make your project's repo a child fork of MatlabProjectTemplate in the GitHub "fork tree", instead of a "canonical" repo that is the root of its own fork tree. You don't want that. You want your project to be a standalone, canonical repo on GitHub.

Do not _clone_ the MatlabProjectTemplate repo. That will leave your local repo pointing to the wrong "origin" repo.

Use the "Use this template" button!

## More info

See also these pages:

* [Project Layout](ProjectLayout.html)
* [Writing Documentation](WritingDocumentation.html)
* [Creating Releases](Releasing.html)
* [Automatic Package Initialization](AutoInitialization.html)
* [FAQ](FAQ.html)
* [Using on Windows](Windows.html)

## More stuff to go here

TODO: add more content
