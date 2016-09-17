---
title: Gradle For Android
tags:
---
## Introduction
Gradle is used to build android applications. There is a plugin for gradle that allows us to configure android applications. There are various build types available, we could build a release build or a debug build. We could setup an automatic signing configuration, so that we can digitally sign the output apks in preparation for uploading them to the google play store. We can also define additional build types if we want. We will also look at the concept of flavors.

<!-- more -->

A flavor allows you to essentially build the same app in multiple different ways with slight changes to the look and feel or even changes to the application itself. A combination of a flavour and a build type is known as a variant. We will also look at using our own android library projects as part of a larger android application, so that we can split functionality into reusable components that can be part of other applications as well.

When android applications were first created was first created there was no real separate build toll available. At that time build for android was an IDE build, i.e we would build an application in an IDE rather than having some separate execution process for building the application itself. Previously there was a plugin for eclipse called ADT(Android developer tools). Back then once you download the ADT plugin and add it to the eclipse IDE, that would take care about building the project. But this was something that the Java community had moved away from for the last 10-15 years, because doing this way would be difficult to reproduce outside an IDE and for example trying to build something on a CI server becomes something that is very difficult. One of the issues was that we could not build different types of the same application at the same time.

So in 2013 Android decided to switch to a real build tool called as gradle and they replaced the IDE to Android Studio which a free version of IntellijIDEA that understands gradle better. In the background Android studio is running the gradle tasks. You can even think the android studio as a UI wrapper around the gradle build tool. The android plugin for gradle runs independent of Android studio, so you could build your app from the command line also or on machines where android studio is not installed (such as CI servers). With gradle we can handle build variants, dependencies, manage manifest entries, deal with signing configurations, run the proguard tool and perform testing.

## Groovy - Classes & Objects
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

In Java if you don't get a constructor you just get one default constructor, but in groovy you get 2 default costrcutor one is like how you have in Java and another one is a default memberwise initialization constructor(Like the default constructor for structures in Swift programming language). But the beauty here is that unlike the swift memberwise constructor you need not provide values for all the fields also. You can just provide the values for those fields that you want and for others groovy will assign default values null for references, 0 for numerics and false for booleans just like Java. Therefore for the person class defined above you could create an instance using `Person person = new Person(first: 'Raj', last: 'Abishek')`. And as I said previously we can also just provide the values for the fields that we want and for others groovy will give a default value `Person person = new Person(first: 'Raj')` will create a person object with first as 'Raj' and the last field will be given a default value of null.But it is important to note here that when you are using this member wise constructor the values for the property are assigned using the setter methods for the properties. Therefore we would get the inside set last string output. Therefore the member wise initialization constructor uses the setter methods to assign values for the properties.

You could also have a toString method on the class that will be automatically called when you pass an instance to the println function.
```groovy
String toString() { "${first} ${last}" }
```
In groovy if you observer you don't even need the return statement because it will automatically return the last evaluated expression in the block and not only that it will look at the return type of the method and try to convert the last evaluated expression to the return type if the types are not matching.

Now lets take a look at AST transformation i.e Abstract syntax tree transformation. To look at this concept first we need to look at import statements. Its important to understand here is that by default groovy imports a couple of packages, like `java.lang.*`, `java.util.*`, `java.io.*`, `java.net.*`, `groovy.lang.*`, `groovy.util.*` and other important packages. Now AST transformation allows groovy developers to typehint annotations at the top of a class and groovy will automatically provide that functionality.
```groovy
import groovy.transform.*

@ToString
class Person {
	String first
	String last

	String toString() { "${first} ${last}" }
}
```
The @ToString annotation will automatically provide a toString method for a class. In our cause since we have manually provided a method groovy will not overwrite it. Groovy will only provide a method if its already not there. But if remove this toString method from the class then groovy will provide a toString method.
```groovy
import groovy.transform.*

@ToString
class Person {
	String first
	String last
}
Person person = new Person(first: 'Raj', last: 'Abishek')
println person
```
Now we would get the output as `Person(Raj, Abishek)`, because this is the way how groovy provides the toString method internally. We can actually typehint multiple annotations to provide multiple functionalities. @EqualsAndHashCode method will generate an equals method and a hashCode method on the Person class according to the normal condition layed out in the Effective Java book. When you actually compare two instances in groovy using the == operator it is operator overloading in action internally groovy calls the equals method on the first instance and passes the 2nd instance as a parameter. Therefore by typehinting the `@EqualsAndHashCode` annotation above the Person class we can actually use the == operator for comparing two instances of the person class to check whether the values are equal.(Unlike java that compares the references).
```groovy
import groovy.transform.*

@ToString
@EqualsAndHashCode
class Person {
	String first
	String last
}
Person person1 = new Person(first: 'Raj', last: 'Abishek')
Person person2 = new Person(first: 'Raj', last: 'Abishek')
println person1 == person2
```
The output of the above code is true because the values are being compared. The == operator is actually calling the equals method on the `Person` class. There is another transformation called as @TupleConstructor that generates a new constructor that allows us to specify the values for the fields in the same order without providing the parameters names while calling the constructor.
```groovy
import groovy.transform.*

@TupleConstructor
class Person {
	String first
	String last
}
Person person1 = new Person('Raj','Abishek')
```
As you can see in the above code, type hinting `@TupleConstructor` generates a new constructor for providing the values for the fields in the same order in which they were defined without the need for naming the parameters. The combination of the @ToString, @EqualsAndHashCode and @TupleConstructor is so popular that there is another transformation called as @Canonical that is functionally equivalents to writing these 3 transformations together.
```groovy
import groovy.transform.*

@ToString
@EqualsAndHashCode
@TupleConstructor
class Person {
	String first
	String last
}
```
The above code is the same as the below code.
```groovy
import groovy.transform.*

@Canonical
class Person {
	String first
	String last
}
```

## Groovy - Closures & Collections
Lets make a collection of person references.
```groovy
import groovy.transform.*

@Canonical
class Person {
	String first
	String last
}

def people = [
	new Person('Raj','Abishek'),
	new Person('Sailesh','Dev'),
	new Person('Dev','Prakash'),
	new Person('Kani','Amuthu')
]

println people.class.name
```
As you know by now when accessing properties, internally the methods are called. There it is functionally equivalent to calling people.getClass().getName() which will print `java.util.ArrayList`. So the people above is a collection, its an array list of person objects. But what if we wanted a linkedlist instead, you could use `LinkedList` instead of the def keyword above or you can do.
```groovy
def people = [
	new Person('Raj','Abishek'),
	new Person('Sailesh','Dev'),
	new Person('Dev','Prakash'),
	new Person('Kani','Amuthu')
] as LinkedList
```
The people variable above is a instance of `java.util.LinkedList` now. If used as `Set` then we would get an instance of `LinkedHashSet`, which will make sure that we don't have any duplicates, thank to the @Canonical transformation for providing the equals and hashCode method using which the set collection is able to maintain a list of unique elements alone. We could also do `as TreeSet` which will give us a sorted set but we haven't implemented the comparable interface that allows the tree set to decide on how its going to sort. In groovy we needn't manually implement the comparable interface as there is an AST transformation for that too called as @Sortable.
```groovy
import groovy.transform.*

@Canonical
@Sortable
class Person {
	String first
	String last
}

def people = [
	new Person('Raj','Abishek'), //#1
	new Person('Raj','Abishek'), //#2
	new Person('Raj','Dev'),
	new Person('Sailesh','Dev'),
	new Person('Dev','Prakash'),
	new Person('Kani','Amuthu')
] as TreeSet

println people
```
First of all since its a set we won't have any duplicates so only one of #1 or #2 will be there. Secondly its will make sure that the list is sorted. It will sort the instances based on the first name and then the last name alphabetically.
```groovy
def nums = [3, 1, 4, 1, 5, 9]
println nums
for(int i=0;i<nums.size();++i) { println nums[i] }
```
As you can see above the normal for loop with the subscript sytax works fine even though the collection is an array list because internally when you use the subscript nums[i] groovy calls the `get` method on the array list collection. Another option to loop through the list is we can use java's foreach operator.
```groovy
def nums = [3, 1, 4, 1, 5, 9]
for(int num : nums) { println num }
```
We also have something called as a for in loop in groovy where we can do the following. This is similar to the foreach lopp in java but we need not typehint the datatype of the array element in the index.
```groovy
def nums = [3, 1, 4, 1, 5, 9]
for(num in nums) { println num }
```
The another interesting way in which we would do this in groovy would be with the help of clousures. The curly brace is like the curly brace inside a method or a function. It takes one argument by default and it is called as it.
```groovy
def nums = [3, 1, 4, 1, 5, 9]
nums.each { println it }
nums.each { n -> println n }
```
As you can see above if we want to give a different name for the parameter then we can give a different name followed by right arrow. As you can see above doing this, only `n` is available and `it` is not available. The each method also returns the collection itself. One of the trends that has become very popular in computer science is the idea of moving towards functional programming. The benefits of functional programming are many but it especially works with small easily composable functions that can be combines with immutable classes inorder to make something that is easy to parallelize and optimize. Its is a very nice system that can minimize a lot of side effects. Groovy is an object oriented language with the concept of closures it can actually do certain functional things. We also have a collect method on the collection that returns a new collection based on the closure that we provide. It applies the closure to each element and returns a new collection based on that. This is similar to the map method present in other programming languages.
```groovy 
def nums = [3, 1, 4, 1, 5, 9]
nums.collect { it * 2 }
```
There is another method called findAll that finds all elements in the collection that satisfies the closure. This is similar to the filter method that is present in other programming languages. The sum method will calculate the sum of all the elements in the collection.
```groovy
def nums = [3, 1, 4, 1, 5, 9]
nums.collect { it * 2 }
	.findAll { it%3 == 0 }
	.sum()
```
The output of the above code is 24. First we find the twice of every number and then filter the elements that is divisible by 3 and they find the sum of those elements. We have seen about linear collections so far, now lets take a look at maps or dictionaries.
```groovy
def map = [k1:1, k2:2, k3:3]
println map.getClass().name
```
The output we get is `java.util.LinkedHashMap`. As you see above we had to use the getClass() method and not the class property because, in a map the . operator is overloaded for putting and getting values from the map. Therefore if we would have used the class property then the map would have looked for a key called class which does not exist and would have returned null, it woudn't have actually called the getClass method internally. We can put values into the map using the . operator or using the subscript syntax as shown below.
```groovy
def map = [k1:1, k2:2, k3:3]
map.k4 = 1
map['k5'] = 2
println map
```
To iterate over the map we can use the each function.
```groovy
def map = [k1:1, k2:2, k3:3]
map.each { e -> println "${e.key} maps to ${e.value}" }
```
The e.key internally calls the e.getKey() and the e.value calls the e.getValue() method, normal property access calls the methods internally. The each methods also supports a two argument closure that will pass the key and the value to the closure.
```groovy
def map = [k1:1, k2:2, k3:3]
map.each { k,v -> println "$k maps to $v" }
```
As you can see above during string interpolation we need not use the {} after the $ if we are just outputting the value and not accessing a property or method. If we use the collect method on the map it transforms it into a list by applying the closure to each element.
```groovy
def map = [k1:1, k2:2, k3:3]
map.collect { k,v -> "$k=$v" }
```
The output is [k1=1, k2=2, k3=2]. The list also has a method called join that joins the elements of the list using the separator given.
```groovy
def map = [k1:1, k2:2, k3:3]
map.collect { k,v -> "$k=$v" }.join('&')
```
The output is k1=1&k2=2&k3=2. The collect methods transforms the map to a list and the join method on the list combines the elements using the & separator.

## Accessing a RESTFUL web service
```groovy
import groovy.json.*

String url = 'http://api.icndb.com/jokes/random?'
def params = [limitTo:'[nerdy]', firstName: 'Raj', lastName: 'Abishek']
String queryString = params.collect { k,v -> "$k=$v" }.join('&')
String jsonTxt = "$url$queryString".toURL().text
def json = new JsonSlupper().parseText(jsonTxt)
println json.value.joke
```
As you can see in the above example first we store the parameters for the request in the map. Then we convert in unto a query string and append it to the end of the url. Then groovy have a `toURL` method on string object to convert a string to a `java.net.URL` instance and then we access the text property to call the `getText` method on the url instance. This gives us the JSON result as a string which needs to be parsed. To parse the JSON string we create an instance of `JsonSlupper` class from the `groovy.json` package and then call the `parseText` method to convert the JSON string to a map.

## Gradle basics
Gradle is an open source project available at http://gradle.org that is supported by a company called Gradle.Inc. Now for our android applications we needn't install Gradle. Gradle will come with Android Studio. Nevertheless you can also install it separately on your hard drive and use it separately. If you are not using Android Studio for android app development, then this is what you will need to do, you will have to install Gradle separately. Installing Gradle is really simple, you must have Java installed on your machine preferably the latest JDK. You need not install Groovy on you machine Gradle installed comes with groovy bundled inside. Gradle ships with its own Groovy library, therefore Groovy doesn't need to be installed separately.