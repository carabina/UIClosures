# UIClosures [![CocoaPod][pd-bdg]][pd] [![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
by [ark](http://www.arkverse.com)
[pd-bdg]: https://img.shields.io/cocoapods/v/UIClosures.svg
[pd]: http://cocoadocs.org/docsets/UIClosures

A Swift closure library for UIKit that makes events significantly easier and cleaner. Currently only supports closures on `UIControl` events, but will be adding more closure support as we go along. Memory managed and written completely in Swift.

All the `UIControlEvents` are supported, and multiple closures can be added to the same event

Be sure to check out our [SwiftRecord](https://github.com/arkverse/SwiftRecord) library too!

## Installation

#### via [CocoaPods](http://cocoapods.org)
1. Edit your Podfile to use frameworks and add UIClosures:
		
		platform :ios, '8.0'
		use_frameworks!
	
		pod 'UIClosures', '~> 0.0.1'
2. run `pod install`

#### via Carthage

1. Just add UIClosures to your Cartfile:

	github "arkverse/UIClosures" >= 0.0.1
	
2. and run `carthage update`

#### Manual Installation
Drag and drop either `Classes/UIClosures.swift` or `UIClosures.framework` into your project

## Usage

1. `import UIClosures` into your file (if needed)
2. call `addListener` on your UIControl

	```swift
	let button = UIButton(frame: CGRect(x: 0, y: 0, width: 100, height: 40))
	button.center = self.view.center
	button.setTitle("Try Me", forState: UIControlState.Normal)
	button.setTitleColor(UIColor.blueColor(), forState: UIControlState.Normal)
	self.view.addSubview(button)

	// Make sure you set your capture list to break your class-closure strong reference loop
	button.addListener(UIControlEvents.TouchUpInside, listener: { [unowned self] (sender) -> Void in
		self.title = "New ViewController Title!"
		let button = sender as! UIButton
		button.titleLabel?.font = UIFont.systemFont
	})
	// Can add another closure to the same event
	button.addListener(UIControlEvents.TouchUpInside, listener: {[weak button = button] (sender) -> Void in
		button.setTitleColor(UIColor.redColor(), forState: UIControlState.Normal)
	})
	```
3. Note that you most likely need your capture list for each closure

##Roadmap

- add more closures
- testing

## License

UIClosures is available under the MIT license. See the LICENSE file
for more information.

Check out [ark](http://www.arkverse.com) for more about us and check out our other Swift libraries