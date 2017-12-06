---
layout: post
title: Buddybuild Privacy Changes
---

Yesterday BuddyBuild sent out an email yesterday basically stating they are no longer collecting user data unless the users explicitly opt-in. This also means a new SDK and some big changes coming: 

> On December 22nd:
> 
> * Buddybuild will no longer accept Feedback from apps using the previous version of the SDK
> * Buddybuild will strip user data portions of Crash Reports from apps using the previous version of the SDK. User data in this context includes: email address, metadata provided through the buddybuild SDK API, logs, device type, IP address, screen size
> * All existing Feedback generated with the previous version of the SDK will be deleted
> * All existing Crash Reports generated with the previous version of the SDK will be stripped of user data 


Personally I've only used Buddybuild on a handful of projects, avoiding the SDK where posible. It has some useful features like keeping track of installations, but the majority of isn't neccesarily things you'd want to have attached to your deployment service and can be easily developed in-house.

I wonder what sparked this decision because they are getting rid of alot of useful data. For reference this is what you would see on a crash report with the old details in place:

![_config.yml]({{ site.baseurl }}/images/buddybuild-privacy.png
) 

I don't fully understand some of the changes like email (wouldn't the developer know this already since they send the invite their?). Eliminating logs, device type and screensize is a bit of a deal breaker. If your app doesn't have a backend component there's no way to collect this data which is invaluable in certain cases when debugging crashes.

Generally when sending out a beta distribution you want to collect the kind of user data which is now optional. This means your crash logs and feedback are going to be a mixture of useful reports and potentially useless ones as well. I'm also concerned about the amount of testers who will now opt-out accidently or just by reflex without thinking.

A much better solution would be to provide an opt-in-only release and explicitly state what's being collected.