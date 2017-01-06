---
layout: post
title:  "Setting Up Caddy & NSSM"
date:   2016-01-24 12:55:50 +11:00
categories:
    - web server
    - windows
    - blog
tags:
    - web server
    - windows
    - blog
update:
    - 2016-06-03 23:33: Updated the syntax highlighting for config file.
---

I have a private diary that I want to write in [markdown][md].  The problem is
I haven't found any good way to do so under Windows and read it in HTML quickly
and easily, so I set out to set up something simple.

This, for now has ended up using the Go language web server [Caddy][caddy] and
[MDWiki][mdwiki].

## References 
[md]: https://daringfireball.net/projects/markdown "Markdown"
[mdwiki]: https://dynalon.github.io/mdwiki "MDWiki"
[caddy]: https://caddyserver.com "Caddy"

1. [MDWiki][mdwiki]
1. [Markdown][md]
1. [Caddy webserver][caddy]

## Tasks

1. Follow the instructions for developing a [MDWiki][mdwiki].  This essentially breaks down to downloading the MDWiki file and then adding markdown files to a directory (or directory structure).
1. Follow the instructions for installing [Caddy][caddy].
    1. I drop the Caddy executable into the into the same folder as the top level MDWiki.
    1. The basic configuration was pretty simple:

~~~ perl
             # Local Diary configuration
             Localhost:xxxx
             
             gzip
             # I don't want to enable directory browsing over the 
             # directories as this is a private site.
             #browse 
             ext .html
             # Log access requests.  Remember that "/" can be used
             # as the path separator.
             log "<log location>" {
                rotate {
                    size 1
                    age 180
                    keep 10
                }
            }
            # Log errors.  Remember that "/" can be used
            # as the path separator.
            errros {
                log "<log location>" {
                    rotate {
                        size 1
                        age 180
                        keep 10
                    }
                }
            }
~~~

This gives a nice simple setup with a low overhead on the system, which is only
available on the home address.

