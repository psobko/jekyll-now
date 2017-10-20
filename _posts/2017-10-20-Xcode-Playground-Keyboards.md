---
layout: post
title: Using Keyboard Input in Xcode 9 Playgrounds
---

Xcode 9.0 makes keyboard input in playground Live Views almost impossible by not resizing the software keyboard based on the size of the window. The image below is the current behaviour of keyboard input.

![_config.yml]({{ site.baseurl }}/images/pg_keyboard_default.png) 

Since the simulator is running the standard iPad vertical orientation resolution (768 x 1024), an appropriately sized keyboard will display as well (0.0, 711.0, 768.0, 313.0). This means if your Live View has a height of less than 1024 you will only be able to see and interact with a portion of the keyboard. This is a huge limiting factor since:

* playgrounds display using the iPhone 6/7/8 size (375 x 667)
* the standard 15" Macbook resolution has a height of 900 
* hardware keyboard input cannot be captured which makes the software keyboard the only option

The only solution I've have until [this radar](http://www.openradar.me/33917909) is addressed involves undocking the keyboard and resizing the window of the underlying simulator. You would still need a width of 768 for the Live View if you want the full keyboard, but this will reduce the minimum height required to 420 which is far easier to work with.

**Before and After**

![_config.yml]({{ site.baseurl }}/images/pg_keyboard_full.png) 

![_config.yml]({{ site.baseurl }}/images/pg_keyboard_undocked.png)

**Code**

Just find this line near the bottom:

```swift
PlaygroundPage.current.liveView = MyViewController()
```

And change it to set a `UIWindow` to the *liveView* property:

```swift
let window = UIWindow(frame: CGRect(x: 0,
                                    y: 0,
                                    width: 768,
                                    height: 1024))
let viewController = MyViewController()
window.rootViewController = viewController
window.makeKeyAndVisible()

PlaygroundPage.current.liveView = window
```

After that you should be able to see the full window, scroll down until the bottom row of the keyboard is visible, then hold down the hide keyboard button until the "Undock" option is visible and tap it. It should look like this

![_config.yml]({{ site.baseurl }}/images/pg_keyboard_undock.png)

.... or just [download](https://github.com/psobko/ShowPlaygroundKeyboard) the Playground


