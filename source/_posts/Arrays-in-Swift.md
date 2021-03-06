---
title: Arrays in Swift
date: 2016-05-25 09:00:00
tags:
---
## Powerful Data Structure
Arrays are one of the most powerful data structures in the Swift programming language. An array stores values of the same type in an ordered list. The same value can appear in an array multiple times at different positions. Arrays in Swift are implemented as generic collections. Every value that is stored in an array is called as an element and the position of the element in the array (0 based) is called the index of the element. If you do not want to have repeated elements then you should have a look at the `Set` data structure. Sets are unordered collection of unique values.

<!-- more -->

Arrays are value types. They are not reference types like class instances. However it is important here to note that if the elements of the array are instances of classes, changing the class does affect other copies, because classes have reference semantics. 

If the array Element type is not a class or @objc protocol type then definitely we know for sure that the storage area for the array is a contiguous block of memory, otherwise we just know that it can be a contiguous block of memory but its not for sure. Why should we know all this ? Thats because, in Swift when array storage is full, it allocates a larger region and copies its elements to the new storage. The size of the new storage allocated is a multiple of the old storage size, an exponential growth strategy is followed here that means that appending a element to the end of the array happens in constant time, averaging the performance of many appending operations. Appending operations that trigger reallocation have a performance cost, but their occurrence decreases as the array size becomes larger as larger, because every time the array size is a multiple of the previous size, so its grows exponentially, and thus the chances of needing a reallocation again during appending is negligible.

An array in Swift is declared as follows.
```swift
var data: Array<String> //declare data as an array of strings - Longer form of type annotation
var names: [String] //declare names as an array of strings - Shorter form of type annotation

var array = ["Mac book", "iMac"] //type inference

var strings: [String] = [] //Initialize as an empty array
var anotherArray = [String]() //Initialize as an empty array
```

The statement `var simple = []` will not compile because there is no way for Swift to infer the data type of the simple array. What is the data type of simple array ? Is it an array of `Int`, or array of `String`, or array of `Double` ?

It is important to note that as shown above if the context already provides type information, such as a function argument or an already typed variable or constant you can create an empty array with an empty array literal, which is written as `[]`

## Array Properties

- `count` is a property that gives the number of elements that the array holds currently.
- `description` is a property that gives a textual representation of the array as a string.
- `endIndex` is the successor of last valid subscript argument. If the array has 4 elements then it means that the last index in the array is 3. There `endIndex` is 4 which is one more than the last index. For an empty array `endIndex` is 0. You can think of `endIndex` as the index position from which you will start inserting the next element you append to the end of the array.
- `startIndex` is always zero. Even if the array is empty then `startIndex` property is zero.
- `isEmpty` property returns a boolean indicating whether the array is empty or not. If the array is empty is returns true otherwise false.
- `first` gets the first element from the array, if array is empty then returns nil, therefore the return type is essentially an optional.
- `last` gets the last element from the array, if array is empty then returns nil, therefore the return type is essentially an optional.

```swift
let array = ["iPhone", "iPad", "Mac book"]
print("The number of elements in the array is: \(array.count)")
print("The array contents are \(array.description)");
print("The next position for insert is: \(array.endIndex)")
print("The start index for array is: \(array.startIndex)")
```

## Array Methods
In Swift we cannot use the subscript syntax to append elements to the end of the array. We can only use the subscript syntax to get an element from the array or update an existing element from the array. It is also important to remember that whenever a new element is added in an array or an existing element is removed from an array the elements in the array are automatically reordered, i.e if we remove the first element then 2nd becomes 1st, the 3rd becomes 2nd and so on. Similarly if we remove the 3rd element from the array then the 4th element becomes 3rd, 5th becomes 4th and so on.
```swift
let array = ["iPhone", "iPad", "Mac book"]
print("The first element in the array is: \(array[0])")
print("The second element in the array is: \(array[1])")
array[2] = "Mac book Pro"
print("The third element in the array is: \(array[2])")
``` 

The above statements are perfectly valid because whatever is placed within the square brackets only ranges from 0 to array.count - 1, anything supplied outside this range will result in a run time error. We cannot append an element to the end of the array using the subscript syntax, ie statement `array[array.count] = newvalue` will result in a run time error.

To append elements to the end of the array we use the `append(_:)` method.
```swift
var array = ["iPhone", "iPad", "Mac book Pro"] //array is declared as a variable for mutability
array.append("iMac")
array.append("Mac book Air")
print(array.count) //Prints 5
```

But the `append` method can only insert elements at the end of the array. To insert an element in between we have to use the `insert(_:atIndex:)` method.
```swift
var array = ["iPhone", "iPad", "Mac book Pro"]
array.insert("iMac", atIndex: 0)
array.insert("Mac book Air", atIndex: array.count)
```

The `atIndex` parameter of the insert method can be supplied with an integer argument ranging from 0 to array.count. Anything exceeding this range will result in an run time error. Thus we can use this function to also insert an element to the end of the array by doing `array.insert(value, atIndex: array.count)`. If the array is empty then we can pass only 0 to the`atIndex` parameter of the method.

To remove an element from an array at a specific index we can use the `removeFromIndex(_:)` method.
The argument supplied to this method is an integer that can range from 0 to array.count - 1.
If index outside of this range is supplied it gives a runtime error. The method removes the element from the array at the given index and returns the removed element. If the array is empty then any argument supplied to the method will result in a run time error.
```swift
var array = ["iPhone", "iPad", "Mac book Pro"]
let name = array.removeAtIndex(0)
print("The removed element is: \(name)") // The removed element is: iPhone
print(array.count) //Prints 2
```

To remove the last element from the array we can do `array.removeAtIndex(array.count - 1)` but we have another useful method for this. It is the `removeLast(_:)` method. It removes the last element in array and returns it, if the array is empty then a call to this method results in a run time error.
```swift
var array = ["iPhone", "iPad", "Mac book Pro"]
let last = array.removeLast(_:)
print("The last element that was removed is: \(last)")
```

To check whether an element is present in an array or not we use the `contains(_:)` method. It returns a boolean response, if the element is present in the array it returns `true` otherwise `false`.
```swift
var array = ["iPhone", "iPad", "Mac book Pro"]
let last = array.contains("Mac book Pro") //Prints true
```

To get the index of a particular element from the array we use the `indexOf(_:)` method.
It gets the index of the given element in the array, if the element is not found or if the array is empty then it returns nil, therefore return type is essentially `Int?` (Optional Int).
```swift
var array = ["iPhone", "iPad", "Mac book Pro"]
let index = array.indexOf("Mac book Pro")
print("The index of the element Mac book Pro is: \(index)")
```

We can also get the minimum and the maximum element in the array according to the < operator.
The `maxElement` method returns the maximum element in the array, if the array is empty it returns nil. The `minElement` method returns the minimum element in the array, if the array is empty it returns nil.
```swift
var array = ["iPhone", "iPad", "Mac book Pro"]
let min = array.minElement(_:)
let max = array.maxElement(_:)
print("The minimum element in the array is: \(min)")
print("The maximum element in the array is: \(max)")
```

We can also remove the first n elements or the last n elements from the array. The `removeFirst(_:)` method removes the first n elements from the array. Similarly the `removeLast(_:)` method removes the last n elements from the array. In both the methods n cannot exceed array.count. If n is larger than the number of elements in the array then we get a runtime error.  
```swift
var array = ["iPhone", "iPad", "Mac book Pro"]
array.removeFirst(1)
array.removeLast(2)
print(array.count) //Prints 0
```

We can also sort the elements of the array according to the < operator. The `sort(_:)` method returns a new array with the elements in the sorted order.
```swift
var array = [2, 1, 7, 3, 6]
for number in array.sort(_:) {
	print(number)
}
```

Instead of returning a new array with the elements in sorted order, if we would like to sort the elements of the array in place then we can use the `sortInPlace(_:)` method.
```swift
var array = [2, 1, 7, 3, 6]
array.sortInPlace(_:)
for number in array {
	print(number)
}
```

We can also remove all the elements in the array with a single method call. We use the `removeAll` method for this purpose. It removes all the elements and has no effect on an empty array.
```swift
var array = [2, 1, 7, 3, 6]
array.removeAll(_:)
print(array.count) //Prints 0
```
