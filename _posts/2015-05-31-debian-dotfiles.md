---
layout: post
title:  "Managing Debian Dotfiles"
date:   2015-05-31 12:55:25 +10:00
updates:
    - date: 2016-03-19 22:20:00 +10:00
      change: Fixed a typo in the xdg-utils package
categories:
    - debian
    - dot files
    - management
tags:
    - debian
    - dot files
---

Managing dot files has long been a problem across multiple machines.  For me
this is more of an issues cross my virutal machines from my desktop to my
tablet.  When setting up my development environment this time round I
remembered seeing something about managing dot files so I went exploring.

After doing some reading I decided to use [dots][dots].  This entry covers how
to set up all my dots files.

## References
[dots]: https://github.com/EvanPurkhiser/dots "Dots"
[dots-tmpl]: https://github.com/EvanPurkhiser/dots-template "Dots Template"
[doychi-tmpl]: https://github.com/doychi/dots-personal "Dots Personal Template"
[xdg]: http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html "XDG Standard"

1. [Dots][dots]
1. [Dots Template][dots-tmpl]
1. [Dots - Doychi's Template][doychi-tmpl]
1. [XDG Configurations][xdg]

## Tasks

The tasks for using Dots are covered by the [readme][doychi-tmpl] file in my dots repo, but essentially is:

1. `aptitude install xdg-user-dirs xdg-utils`
1. Follow the [readme][doychi-tmpl]
    1. Clone the repo.
    1. Initialise the local environment.
    1. Set the groups to apply for the machine.
    1. Install the configuration for the machine.
    1. Configure the machine for [XDG][xdg].
