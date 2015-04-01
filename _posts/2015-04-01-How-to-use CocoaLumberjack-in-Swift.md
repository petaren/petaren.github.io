---
layout: post
title: How to use CocoaLumberjack in Swift
---
#### Background
I have been struggling with this a bit and couldn't find a documented solution online. So upon solving the problem I decided to write this blog post just to share my findings with the world and hopefully help someone else. Please note that I used prerelease versions of both CocoaPods and CocoaLumberjack.

#### Prerequisites 
You need to have the release candidate of [CocoaPods](http://cocoapods.org) installed. I used version `0.36.0.rc.1`. To install the prerelease version type the following command into the terminal:
```
$ [sudo] gem install cocoapods --pre
```

You can check to see which version you have with the command: 
```
pod --version
```

#### Installing CocoaLumberjack
First we need to create a `Podfile` in the projects root folder. That is usually the same folder where your `.xcodeproj` file is. 

In the `Podfile` add the following text:

```
platform :ios, "8.1"

pod "CocoaLumberjack", '2.0.0-rc2'

use_frameworks!
```

Let's break this down a bit. The first line tells us if we're building an iOS or an OSX application and the system target version. In this case I'm targeting iOS 8.1.

The second line specifies that we want to install CocoaLumberjack and that we explicitly want the version `2.0.0-rc2`. You can find all available releases on CocoaLumberjacks github [https://github.com/CocoaLumberjack/CocoaLumberjack/releases]().

The last line tells CocoaPods that we want to use dynamic frameworks instead of static libraries.

After saving the `Podfile` to your project root, run this command inside your project root:  
```
$ pod install
```

When it is done you can close your Xcode project and open the newly created `.xcworkspace` file located in your project root, right next to your `.xcodeproj` file. Now this will not work entirely as expected.

#### Finishing the job

We need to help it out a bit by adding ```CocoaLumberjack.swift``` to the project that wasn't added. So go to your project root and navigate into `CocoaLumberJackTest/Pods/CocoaLumberjack/Classes`. There is a file called `CocoaLumberjack.swift`, drag that file into the `Pods` project, I suggest into the `Pods/CocoaLumberjack/Default` group. When XCode gives you options for adding the files make sure to leave `Copy items if needed` unchecked. Also uncheck it from the `Pods` target and check it to the `Pods-CocoaLumberjack` target. 

![](/img/posts/xcode add file options.png)

That's it, it should work now!

Go ahead and `import CocoaLumberjack` into your own swift files and DDLog all you want.

```swift
import Foundation
import UIKit
import CocoaLumberJack

class ViewController: UIViewController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        defaultDebugLevel = DDLogLevel.Info
    }
    
    override func viewDidAppear(animated: Bool) {
        super.viewDidAppear(animated)
        
        DDLogInfo("My view controller did appear!")
    }
    
}
```