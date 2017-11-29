---
layout: post
title: iTerm2 Finder Droplet
---

Like most developers I spend alot of time in Terminal and recently switched back to [iTerm2](https://www.iterm2.com/) in hopes of increasing productivity. Unfortunately iTerm doesn't come with any Finder services to quickly launch into folders like Terminal. I find alot of applications will let you open a project folder in Finder but lack terminal support so I end up using this feature quite a bit.

After thinking about it a little bit, I figured a toolbar application for Finder would probably be faster than trying to click on a line in a nested context menu. I found an old AppleScript app I wrote back in 2012 and slightly tweaked it.

![_config.yml]({{ site.baseurl }}/images/iterm2-finder-app.png) 

Still need to work on the icon a bit but I'm pretty happy with how it turned out. I was able to give it a few keyboard modifiers as well for more flexibility with how iTerm should open the location. [Check it out on Github.](https://github.com/peterldowns/iterm2-finder-tools)