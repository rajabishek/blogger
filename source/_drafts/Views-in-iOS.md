---
title: UIView Fundamentals
tags:
---

## Superview & Subview
You can never tell the view hierarchy by just looking at the views in an iOS application. Apple has revised the view architecture from OS X 10.5 and ever since then when dealing with views one must remember the following 2 points.

<!-- more -->

- Some or all of a subview can appear outside its superview.
- A view can overlap another view and can be drawn partially or totally in front of it without being its subview.

The first point means that just because a view lets say v1 is a subview of v2 it doesn't mean that the visibility of v1 is bounded by v2. Even though v1 is a subview of v2 it can appear outside the rectangular area defined for v2. The second point means that a view doesn't own its rectangular area, meaning lets say we have a view v3 with a rectangular area defined for it. Now another view v4 can still appear in the rectangular area of v3 even though v4 is not a subview of v3.

![Screenshot 1](/img/ios-views/view-hierarchy.png)

By seeing the above image you can never tell which view is the parent of what. You can never get any idea about the view hierarchy by just seeing the visualization. Actually the black view and the red view are siblings, they have the main view of the view controller as the parent and the blue view is actually the sub view of black view. As I told you earlier even though the blue view is the child of black view still it can be visible outside the regions of the black view and even though the red view is not the child of black view it can still overlap or cover the area occupied by the black view.


## Importance of view hierarchy
So if view hierarchy doesn't dictate the way views are drawn then what is the use of having it, what is the use of declaring one view as the parent of another ? What is the significance of view hierarchy then ?. The view hierarchy dictates the order in which the views are drawn on the screen. A superview is drawn before a subview. The subviews of a superview are drawn in the same order as they are in the view hierarchy. 

In the above diagram we know that the black view and red views are siblings and they are children of the main view of the view controller. Since black view is the first child it is drawn first. Then the red view is drawn. When drawing a view you draw all the super views along with it. But we need to remember here that parent views is drawn before the child views are drawn. Therefore the order of drawing here is first the black view is drawn then the blue view and then the red view.

You can think of drawing like painting on a canvas. The later one drawn will cover the previous ones drawn if the areas overlap. And as I mentioned just now, the red view cannot appear in between the black and blue view, because the black and blue views are subview and superview and are therefore they are always drawn together.

The view hierarchy is also important for the following reasons:
- If a view is removed from or moved within its superview, its subviews go along with it.
- A view’s degree of transparency is inherited by its subviews.
- A view can optionally limit the drawing of its subviews so that any parts of them outside the view are not shown. This is called clipping. To enable clipping we set the `clipsToBounds` property to true.
- If a view’s size is changed then its subviews can be resized automatically.

## Properties and helper methods
Every view has a `superview` property of type `UIView` that is a reference to the instance of super view. And every view has a property called `subviews` of type `[UIView]` that is an immutable array of the subviews in the back to front order. We also have the `isDescendantOfView:` to check whether a view is a child of a subview, i.e is it a subview at any depth. Every view also has a property called `tag` which is a simple numeric value. Every view has a `backgroundColor` property that sets the background color for the view and if set to nil(default value) then in has a transparent background.

If you need any reference to a view higher up in the hierarchy from a particular view you can use the `viewWithTag:` method. It propagates up the view hierarchy chain and checks the tag to find the correct view. The method `addSubview:` makes one view a subview of another and `removeFromSuperview:` takes a subview out of its superview’s view hierarchy. When `addSubview:` method is called, the view is placed as the last subview, thus it is drawn last, meaning that it appears frontmost. The subviews of a superview are indexed from 0. The first subview i.e the one drawn first has the index 0. Since we have an index for every subview this gives us the flexibility to perform some neat operations. 
- We can insert a sub view at a specific index using the `insertSubview:atIndex:` method. 
- We can insert a subview below particular subview using the `insertSubview:belowSubview:` method.
- We can insert a subview above particular subview using the `insertSubview:aboveSubview:` method.
- We can swap the order of two sibling views using `exchangeSubviewAtIndex:withSubviewAtIndex:` method.
- Bring a subview all the way to the front using the `bringSubviewToFront:` method.
- Send a subview all the way to the back using the `sendSubviewToBack:` method.

Removing a subview from its superview releases it. If we intend to reuse that subview later on, then we will have to retain it first by assigning it to a property. There is no single function in iOS that allows us to remove all the sunviews. But we can cycle through the `subviews` property and remove each subview one by one.
```swift
superview.subviews.forEach { (subview: UIView) in subview.removeFromSuperview() }
```

## Visibility and Opacity
A view can be made invisible by setting its `hidden` property to true, and visible again by setting it to false.

When you hide a view, the view and all its sub views are made invisible but they are not removed from the view hierarchy. It is just that they are nor visible on the screen and they will not receive any touch events. For making a view partially transparent we can manipulate the `alpha` property on the view. The alpha value can range from 0.0 to 1.0. 0.0 is perfectly transparent and 1.0 is opaque. The alpha value is inherited by all the subviews. When setting the alpha value to 0.5 for a view the view and all its subview become 50% transparent.

Lets say we have a view b as a subview of view a. Not lets say the alpha value for view a is 0.5 then when you give alpha value of b as 0.5, the view b is actually 25% transparent. Since view b is already inheriting the alpha value of a, any alpha value you assign to be will be relative to the value assigned for its super view. A view’s alpha property value affects both the apparent transparency of its background color and the apparent transparency of its contents.

## Frame & Bounds
Both the `frame` and `bounds` property of a view are of type `CGRect`. A `CGRect` essentially represents 4 elements the x and y coordinates i.e the position of the view and the width and height i.e the size of the view. Now the difference between frame and bounds is that the `frame` property give a `CGRect` in which the position of the view is with respect to the superview’s coordinate system and the `bounds` property gives a `CGRect` in which the position of the view is with respect to its own coordinate system. By default the superview’s coordinate system will have the origin at its top left and with the x axis in the rightwards direction and the y axis downwards.

Since CGRect represents the position and size of a view, resetting a views frame will result in resizing and repositioning a view within its parent. When you create a view programatically in iOS you initialize it with a frame using the `init(frame:)` initializer. If you don't provide a frame the default CGRect is CGRectZero which has zero height and width. A view with a zero-size frame is effectively invisible.

## Window coordinates
The device screen has no frame, but it has bounds, because there is nothing up the device screen. The main window has no superview, but its frame is set with respect to the screen’s bounds.
```swift
let window = UIWindow(frame: UIScreen.mainScreen().bounds)
```
In iOS 9 you can omit the frame parameter it is automatically set the screen bounds. The window's coordinates is thus essentially the screen coordinates.