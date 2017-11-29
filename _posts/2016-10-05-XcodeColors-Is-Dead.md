---
layout: post
title: XcodeColors Is Dead :(
---

So it looks like Apple's [killed XcodeColors](https://github.com/robbiehanson/XcodeColors/issues/88)</a> in Xcode8 (as well as virtually every other plugin), breaking the ability to have coloured log messages in the console. This is a huge letdown as colors helped to differentiate between different log levels when using  [CocoaLumberjack](https://github.com/CocoaLumberjack/CocoaLumberjack)!

![](https://camo.githubusercontent.com/b82c866e805f4b037e5cd0b8f2626bc169c02604/687474703a2f2f6661726d342e737461746963666c69636b722e636f6d2f333735352f393537363132303038375f626632613363616539315f632e6a7067)

Browing through an [issue on Github](https://github.com/robbiehanson/XcodeColors/issues/88) gave me an idea to use emojis as a temporary solution:

![_config.yml]({{ site.baseurl }}/images/Screen-Shot-2016-10-05-at-4.47.19-AM-300x87.png
) 

![_config.yml]({{ site.baseurl }}/images/Screen-Shot-2016-10-05-at-4.47.37-AM.png
) 


Wasn't a huge fan of the lack of colour variation but I think I'm happy with this set:

![_config.yml]({{ site.baseurl }}/images/Screen-Shot-2016-10-05-at-5.33.53-AM.png
) 


This is what my custom formatter looks like now:

```objc
- (NSString*)formatLogMessage:(DDLogMessage *)logMessage
{
    NSString *path = logMessage-&gt;_file;
    NSString *fileName = [path lastPathComponent];
    NSString *dateAndTime = [self stringFromDate:(logMessage-&gt;_timestamp)];
    
    NSString *logLevel;
    switch (logMessage-&gt;_flag) {
        case DDLogFlagError    : logLevel = @""&#x1f4d5;""; break;
        case DDLogFlagWarning  : logLevel = @""&#x1f4d2;""; break;
        case DDLogFlagInfo     : logLevel = @""&#x1f4d8;""; break;
        case DDLogFlagDebug    : logLevel = @""&#x1f4d7;""; break;
        default                : logLevel = @""&#x1f4d3;""; break;
    }
    
    return [NSString stringWithFormat:@""%@%@%@ %@:%lu %@"", logLevel, dateAndTime, logMessage-&gt;_function, fileName, (unsigned long)logMessage-&gt;_line, logMessage-&gt;_message];
}
```

While not nearly as good as what we had before there is one advantage: since emojis are being used it means that they'll copy over when the text is copied.