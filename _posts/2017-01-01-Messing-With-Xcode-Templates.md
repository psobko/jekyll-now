---
layout: post
title: Messing With Xcode Templates
---

*This is an updated version of my 2016 post for Xcode9*

A neat trick I picked up working on a project this year was removing the Xcode boilerplate copyright text. The seven lines  which gets prependedd to every file you create and in many scenarios serve no purpose other than wasting space.

![_config.yml]({{ site.baseurl }}/images/template_default.png) 

Xcode doesn't make it very easy to mess around with it's file templates, but the only real tricky part is finding where they're located:

`$ cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File\ Templates/Source/`


You need to do a little more digging to find a specific template, though before you do any editing I would strongly suggest making a backup. For starters you can find all the common file templates inside `Cocoa Touch Class.xctemplate/`. This is what a Swift `NSObject` subclass template looks like:


```
//___FILEHEADER___

import UIKit

class ___FILEBASENAMEASIDENTIFIER___: ___VARIABLE_cocoaTouchSubclass___ {

}
```

`___FILEHEADER___` is what will print the top comments. We can remove it completely and it will look like this:

![_config.yml]({{ site.baseurl }}/images/template_custom.png) 

Previous versions of Xcode didn't use `___FILEHEADER___` but you can replace it with your own version if you wanted to keep some of the text. All the same variables are still available:

```
// ___FILENAME___
// ___PROJECTNAME___
// ___FULLUSERNAME___
// ___DATE___
// ___COPYRIGHT___
import UIKit

class ___FILEBASENAMEASIDENTIFIER___: ___VARIABLE_cocoaTouchSubclass___ {

}
```

Which would give you something like:

![_config.yml]({{ site.baseurl }}/images/template_custom_short.png) 