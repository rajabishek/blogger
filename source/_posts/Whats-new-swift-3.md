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
(1...10).forEach { sum += $0 }
//Sum of the first 10 numbers
print(sum)
```
> If you would like to know more about the motivation behind this change, check out [Erica Sadun’s proposal](https://github.com/apple/swift-evolution/blob/master/proposals/0007-remove-c-style-for-loops.md) on the removal of C-style for loop.

## No more var in function parameters
Function parameters are by default constants in Swift, since you don’t need to modify them in its body. However, there are certain cases when you need to modify the parameters inside the function and Swift 2 allowed for declaring them as variables with the `var` keyword. You can mark a function parameter as variable with the var keyword. Once the parameter is marked as var, it creates a local copy of the value so you can modify its value in the body of the function.
```swift
func primeNumbersInRange(var n1: Int, n2: Int) {
    
    while(n1 < n2){
        
        var flag = false
        
        for(var i=2; i<=n1/2; ++i)
        {
            if(n1%i == 0) {
                flag = true
                break
            }
        }
        
        if (!flag) {
            print(n1)
        }
        
        ++n1
    }
}
primeNumbersInRange(4, n2: 20)
```
The above is a simple program to find the prime numbers within a given range. In Swift 3 the above code would be a lot different the ++ operators would be removed, the for loop style will be different and most importantly the var key word cannot be used while declaring function parameters. 

Swift 3 no longer allows developers to set function parameters as variables as Swift developers may get confused between `var` and `inout`. So the latest version of Swift simply removes var from function parameters. Therefore, to write the same primeNumbersInRange function in Swift 3, it requires a different approach. You’ll need to save the values of the function parameters to local variables before you proceed.
```swift
func primeNumbersInRange(n1: Int, n2: Int) {
    
    //We have to make a local copy explicity, n1 & n2 will always remain as constants
    var start = n1;
    
    while(start < n2){
        
        var flag = false
        for i in 2...start/2 {
            
            if(start%i == 0) {
                flag = true
                break
            }
        }
        
        if (!flag) {
            print(start)
        }
        
        start += 1
    }
}

primeNumbersInRange(n1: 4, n2: 20)
```

If you would like to know more about the motivation behind this change, check out the [proposal](https://github.com/apple/swift-evolution/blob/master/proposals/0003-remove-var-parameters.md) on the removal of var keyword while declaring function parameters.

## Consistent label behavior for function parameters
In Swift 2 we would call the above function that we defined like this.
```swift
primeNumbersInRange(4, n2: 20)
```
Under the scenes function parameter lists are tuples, so you can also create a tuple and pass it as an argument. The tuple's structure needs to match the function prototype.
```swift
let argument = (4, n2: 20)
primeNumbersInRange(argument)
```
As you can see, you do not need to specify the label of the first parameter in Swift 2. However, you have to specify the label of the second (and the rest of the parameters) when calling the function. This syntax is confusing for beginners, so it is designed to standardize the label behavior. In Swift 3 you would call the function like this.
```swift
primeNumbersInRange(n1: 4, n2: 20)
```
But what if you don't want to pass the first parameter label during a function call. Then in Swift 3 while declaring the function you have to be explicit.
```swift
func primeNumbersInRange(_ n1: Int, n2: Int) { ... }
```
By doing this, you can invoke the function using the old way i.e without specifying the first label. This would also initially be helpful in making you code migration process to Swift 3 easier.


