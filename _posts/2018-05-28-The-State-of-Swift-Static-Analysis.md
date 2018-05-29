---
layout: post
title: The State of Swift Static Analysis 
---

Static analysis is an essential technique for ensuring delivery of quality and secure code throughout the SDLC. Since this type of analysis is performed without the need of a compiled binary, it means developers can analyze their code while it's being written and checked in to source control.

#### Required Functionality

- Tight integration within the SDLC 
- Ease of use for developers while providing valuable information
- Gentle prodding to encourage usage, and the ability to enforce it if needed
- Reporting, ideally with the ability control presentation based  on audience (ie:  higher level management, team leads, developers)

#### Open Source vs Closed Source/Services

There's arguments for both sides but I will only looking at open source solutions. This is for a number of (opinionated) reasons:

- I don't like the idea of transmitting source code or any data to servers I don't control
- No risk of compromised credentials, social engineering, data breaches, or any other means of gaining unauthorized access to any data unless the security of the local network has been breached
- Ability to extend with custom functionality or remove unwanted/insecure features
- Reliance on a service which may be discontinued or fails to meet requirements in the future
- Reliance on 3rd party support for issues which could be resolved with access to the source

So what are the options?

## [Clang Static Analyzer](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/debugging_with_xcode/chapters/static_analyzer.html)

By far the most useful static analyzer is the one built directly into Xcode, and part of the technology compiling the code! In 2005 Apple hired the primary author of LLVM and the Clang project to prepare LLVM for production, which included integrating the analyzer into Xcode. Over the last decade Chris Lattner directed the Developer Tools department and built out Apple's core developer tools technologies. He continued personally developing many of the features in LVVM and lead the development of Swift until 2017.

The Clang Static Analyzer is the reason there aren't that many third party options, it's able to catch thousands of flaws and just like Clang it employs advanced algorithms for high efficiency. Xcode integration means it's easy to set up for automatic analysis in the project scheme, and issues are displayed right in the source editor where they occur.

## [SonarQube](https://www.sonarqube.org/) + [Sonar-Swift](https://github.com/Backelite/sonar-swift)

While there's some great tools out there for analysis, they present a bit off challenge to effectively integrate into the SDLC. Tools like Tailor, Lizard, and SwiftLint either output plaintext to the command line or generate various formats of reports. It takes some trial and error to configure them and automate their execution, as well as storing the results. SonarQube used together with the Sonar-Swift plugin accomplishes these tasks and in addition allows:

- Integration with various CI tools
- Effort estimations for discovered issues
- Gating to ensure no software is delivered unless certain quality controls  pass
- Access control for results
- Historical overviews and many options for data visualization
- Multi-project/language support

Setting up SonarQube can be a bit of an investment, though less effort than if the the same tools were setup and integrated individually.

[Tailor](https://github.com/sleekbyte/tailor) - Static analysis/linting. Ensures code style conventions. Can be integrated directly into Xcode.

[Lizard](https://github.com/terryyin/lizard) - Code complexity analyzer for a wide range of languages.

[SwiftLint](https://github.com/realm/SwiftLint) - Enforces Swift style and conventions. Hooks directly into Clang and SourceKit.

## [Swift-format](https://github.com/apple/swift/blob/master/docs/SwiftFormat.md) / [SwiftFormat](https://github.com/nicklockwood/SwiftFormat)

To be evaluated.