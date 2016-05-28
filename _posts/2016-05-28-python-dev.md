---
layout: post
title:  "Python Development Environment"
date:   2016-05-28 16:34:01 +1000
categories:
    - debian
    - python
    - development
tags:
    - debian
    - python
    - development
excerpt_separator: <!--excerpt-->
---

I'm thinking about a change of jobs and what that job might look like.  I have
been doing some training in [Splunk](http://www.splunk.com) and it has made me
think about perhaps getting into supporting Splunk. I think to that to be able
to do this properly I will need to learn [Python][p].

So, this post is about me learning and setting up for developing in
[Python][p].

<!--excerpt-->

## References
[pyenv]: http://www.deadp0rk.com/2015/03/26/setup-python-on-debian-7-wheezy/ "Seup Python on Debian 7 (wheezy)"
[p]: https://www.python.org "Python Language Home"

1. [Setup Python on Debian 7][pyenv]
1. [Python][p]

## Overview
As I'm still working through learning [Python][p] and what a good development environment looks like for [Python][p].  What does this mean for this entry?  Well I expect it means that it will have quite a few updates as I find what I think are better ways to do things.

So, what did I do?  At the moment I have only installed [pyenv][pyenv] so that I can use the version of [Python][p] that I select on my projects. Currently this looks like:

1. Install pyenv, with pip.
1. Configure the environment.
1. Install Python 3.5.1, as this is the version I want to start with.

## Install Pyenv
~~~ bash
 $ pip3 install --egg pyenv
~~~

## Configure the Environment
Because I use [Dots](https://github.com/EvanPurkhiser/dots/blob/master/README.md), this is done by:

1. Creating a news directory in `~/.local/etc`
1. Adding a bashrc file with the environment configuration
1. Re-run the dots install

### Create the Dots entry

~~~ bash
$ mkdir -p ~/.local/etc/dev-langs/python
~~~

### The content of the `bashrc`
~~~ bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
~~~

## Install Python 3.5.1
~~~ bash
 $ pyenv install 3.5.1
~~~

## Wrap Up

* Don't forget to commit the changes
