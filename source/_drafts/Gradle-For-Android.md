---
title: Gradle For Android
tags:
---
## Introduction
Gradle is used to build android applications. There is a plugin for gradle that allows us to configure android applications. There are various build types available, we could build a release build or a debug build. We could setup an automatic signing configuration, so that we can digitally sign the output apks in preparation for uploading them to the google play store. e can also define additional build types if we want. We will also look at the concept of flavors.

A flavor allows you to essentially build the same app in multiple different ways with slight changes to the look and feel or even changes to the application itself. A combination of a flavour and a build type is known as a variant. We will also look at using our own android library projects as part of a larger android application, so that we can split functionality into reusable components that can be part of other applications as well.

<!-- more -->

When android applications were first created was first created there was no real separate build toll available. At that time build for android was an IDE build, i.e we would build an application in an IDE rather than having some separate execution process for building the application itself. Previously there was a plugin for eclipse called ADT(Android developer tools). Back then once you download the ADT plugin and add it to the eclipse IDE, that would take care about building the project. But this was something that the Java community had moved away from for the last 10-15 years, because doing this way would be difficult to reproduce outside an IDE and for example trying to build something on a CI server becomes something that is very difficult. One of the issues was that we could not build different types of the same application at the same time.

So in 2013 Android decided to switch to a real build tool called as gradle and they replaced the IDE to Android Studio which a free version of IntellijIDEA that understands gradle better. In the background Android studio is running the gradle tasks. You can even think the android studio as a UI wrapper around the gradle build tool. The android plugin for gradle runs independent of Android studio, so you could build your app from the command line also or on machines where android studio is not installed (such as CI servers). With gradle we can handle build variants, dependencies, manage manifest entries, deal with signing configurations, run the proguard tool and perform testing.

## Groovy fundamentals
```groovy
class Person {
	String first
	String last
}

Person person = new Person()
person.setFirst('Raj')
person.last = 'Abishek'
println "${person.getFirst()} ${p.last}"
```
This is a sample groovy code show above. In groovy fields are private by default(in Java they are package-private by default). Also in groovy methods are public by default and class itself is public by default. Now if you want a public field or a private method you have to use those access modifiers while defining them. In groovy if you don't provide an access modifier for the fields then it automatically generates getters and setters for them. Ok Raj, you told me that the fields are private by default then how are you able to access the last field shown above. The thing is that groovy automatically converts to the corresponding getter or setter method whenever you are trying to access the fields directly. So actually the line person.last = 'Abishek' is internally interpreted as person.setLast('Abishek') and similarly the p.last is interpreted as p.getLast(). Infact if you had defined a setLast method on the class manually like this
```groovy
void setLast(String last) {
	println 'inside set last'
	this.last = last
}
```
then while executing the statement person.last = 'Abishek', the string inside set last will be printed. So when it looks like you are doing property access you are indirectly using the getters and setters. Infact even if you don't have a property called test in the class and you try to access it via an instance the groovy will internally call the instance.getTest method. So it is important to note here that you could get away with just having the the getters and setters and not the property itself and accessing the property will invoke the getters and setters.

In Java if you don't get a constructor you just get one default constructor, but in groovy you get 2 default costrcutor one is like how you have in Java and another one is a default memberwise initialization constructor(Like the default constructor for structures in Swift programming language). Therefore for the person class defined above you could create an instance using `Person person = new Person(first: 'Raj', last: 'Abishek')`. But it is important to note here that when you are using this member wise constructor the values for the property are assigned using the setter methods for the properties. Therefore we would get the inside set last string output. Therefore the member wise initialization constructor uses the setter methods to assign values for the properties.

You could also have a toString method on the class that will be automatically called when you pass an instance to the println function.
```groovy
String toString() { "${first} ${last}" }
```
In groovy if you observer you don't even need the return statement because it will automatically return the last evaluated expression in the block and not only that it will look at the return type of the method and try to convert the last evaluated expression to the return type if the types are not matching.
