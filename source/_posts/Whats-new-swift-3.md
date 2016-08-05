---
title: What's new in Swift 3
date: 2016-08-05 17:15:46
tags:
---
## What's new & what's gone
To be honest Swift 3 has lot of changes. If you compile in Xcode 8 beta, it will complain at your code. Apple integrated Swift 3 into Xcode 8 beta at WWDC 2016. Swift 3 is coming later this year. If you haven’t been following the Swift Evolution [project](https://github.com/apple/swift-evolution) closely, you may wonder what are the new changes and how it will affect your code, and when you should start porting your code to Swift 3. This article can help you with that.

<!-- more -->

## Getting hands on
So where do we run Swift 3 and experiment with it ? Swift 3 preview is available in Xcode 8 beta which developers can download and try now. As Swift 3 is not officially released by Apple yet, developers have to wait till the year's end before they can publish an app to the store that is written in Swift 3.

As of now along with Xcode 8 beta, Apple has included Swift 2.3 & Swift 3. Swift 2.3 is the same as Swift 2.2 but with support for many of the new SDKs and Xcode features announced at WWDC 2016. Once Xcode 8 comes out of beta, you will be able to submit apps using Swift 2.3 if you have not yet migrated your code to Swift 3.

Its a good thing that Apple will include Swift 2.3 also in Xcode 8 stable release not creating problems for people who aren't learning Swift 3 yet. They have really made the migration process smooth and easy. Apple has also included a Migration Assistant in Xcode to port your existing applications to Swift 3. I highly recommend you to create a new git branch and use that to get a feel of what has changed. But since you can’t release an app to the App Store until Xcode 8 is out of beta and Swift 3 is officially released, it is better to wait porting the codebase to Swift 3 until things calm down a bit.

Or if you would just like to experiment and try out the language now, I highly recommend the [IBM Sandbox](https://swiftlang.ng.bluemix.net/#/repl). Its a REPL that is available online in cloud to experiment with Swift 3.

The best news of all is that Swift 3 aims to be the last release with breaking source changes. So looking forward, you should be able to keep your Swift code from version to version. Swift core team has promised that if they do need to break source compatibility, they will offer long deprecation cycles. That means the language has achieved source stability that will encourage more conservative companies to adopt it.

## The changes
As I said earlier they are 2 broad categories of changes that have been made. The things that are gone as of Swift 2.3 & things that are new in Swift 3. Let’s start with the removed ones, since they are easier to understand and you may have encountered them before as warnings in Xcode 7.3.

## ++ & -- operators
The increment and decrement operator are there in almost many programming languages that allow to quickly increase or decrease a value by one.
```swift
var count = 0
++count
print(count) //1
--count
print(count) //0
```
However, things get a bit complicated for beginner's when deciding which one to choose. Each of them comes in two possible variations prefix and postfix. Under the hood its operator overloading in action, they are all functions that return values which you may use or neglect. Its easy for a programmer who has already worked with a C style language, but if you think about it, it's a bit overwhelming for the rookies, because ultimately the goal of writing neat code is that it must be simple and understandable to all. The Swift community felt that removing these operators and by encouraging the compound assignment operators instead of these, Swift can feel more natural and intuitive in nature.
```swift
//Same code written using compound assignment operators
var count = 0
count += 1
print(count) //1
count -= 1
print(count) //0
```
> If you would like to know more about the motivation behind this change, check out [Chris Lattner’s proposal](https://github.com/apple/swift-evolution/blob/master/proposals/0004-remove-pre-post-inc-decrement.md) on the removal of ++ and — operators.

## C style for loops
If you remember, while programming the frequent place where you would use the decrement and increment operator would be in for loops. 
```swift
var sum = 0
for (i = 1; i <= 10; i++) {
  sum += i
}
//Sum of the first 10 numbers
print(sum)
```
But now with the removal of the operators, it means that we need a change in how we write loops also. And yes, you we correct, we write for loops in a different way now. The ... is called as closed range operator. It includes all the number from start to end, unlike the half open range operator ..< that does not include the end value.
```swift
var sum = 0
for i in 1...10 {
  sum += i
}
//Sum of the first 10 numbers
print(sum)
```
Alternatively, you can also use the for-each loop style with closures and shorthand arguments.
```swift
var sum = 0
(1...10).forEach {
  sum += $0
}
//Sum of the first 10 numbers
print(sum)
```
> If you would like to know more about the motivation behind this change, check out [Erica Sadun’s proposal](https://github.com/apple/swift-evolution/blob/master/proposals/0007-remove-c-style-for-loops.md) on the removal of C-style for loop.

