---
title: User Guide
---

## Starting a project

To create a new project using MatlabProjectTemplate, go to [the GitHub repo](https://github.com/janklab/MatlabProjectTemplate) and click the green "Use this template" button near the upper right of the page.

Name your new repo after your project name. This will be visible to your end users, so pick a good name!

Once the new repo is created, clone it to your local machine, and edit the `project_settings.sh` file to define your project's basic properties and metadata.

Then open up a shell session in a terminal, and run `./init_project_from_template`.

Have a look around the modified source tree, and if things look good to you, commit the changes with `git add -A; git commit -a -m 'Project initialization from MatlabProjectTemplate` and do a `git push`.

You're ready to start developing!

## More info

See also these pages:

* [Project Layout](ProjectLayout.html)
* [Writing Documentation](WritingDocumentation.html)
* [Creating Releases](Releasing.html)
* [Automatic Package Initialization](AutoInitialization.html)
* [FAQ](FAQ.html)

## More stuff to go here

TODO: add more content
