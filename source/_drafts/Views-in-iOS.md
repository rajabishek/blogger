---
title: Views in iOS
tags:
---

## Superview & Subview
You can never tell the view hierarchy by just looking at the views in an iOS application. Apple has revised the view architecture from OS X 10.5 and ever since then when dealing with views one must remember the following 2 points.
- Some or all of a subview can appear outside its superview.
- A view can overlap another view and can be drawn partially or totally in front of it without being its subview.

The first point means that just because a view lets say v1 is a subview of v2 it doesn't mean that the visibility of v1 is bounded by v2. Even though v1 is a subview of v2 it can appear outside the rectangular area defined for v2. The second point means that a view doesn't own its rectangular area, meaning lets say we have a view v3 with a rectangular area defined for it. Now another view v4 can still appear in the rectangular area of v3 even though v4 is not a subview of v3.

![Screenshot 1](/img/ios-views/view-hierarchy.png)

By seeing the above image you can never tell which view is the parent of what. You can never get any idea about the view hierarchy by just seeing the visualization. Actually the black view and the red view are siblings, they have the main view of the view controller as the parent and the blue view is actually the sub view of black view. As I told you earlier even though the blue view is the child of black view still it can be visible outside the regions of the black view and even though the red view is not the child of black view it can still overlap or cover the area occupied by the black view.

So if view hierarchy doesn't dictate the way views are drawn then what is the use of having it, what is the use of declaring one view as the parent of another ? What is the significance of view hierarchy then ?. The view hierarchy dictates the order in which the views are drawn on the screen. A superview is drawn before a subview. The subviews of a superview are drawn in the same order as they are in the view hierarchy. 

In the above diagram we know that the black view and red views are siblings and they are children of the main view of the view controller. Since black view is the first child it is drawn first. Then the red view is drawn. When drawing a view you draw all the super views along with it. But we need to remember here that parent views is drawn before the child views are drawn. Therefore the order of drawing here is first the black view is drawn then the blue view and then the red view.

You can think of drawing like painting on a canvas. The later one drawn will cover the previous ones drawn if the areas overlap. And as I mentioned just now, the red view cannot appear in between the black and blue view, because the black and blue views are subview and superview and are therefore they are always drawn together.

The view hierarchy is also important for the following reasons:
- If a view is removed from or moved within its superview, its subviews go along with it.
- A view’s degree of transparency is inherited by its subviews.
- A view can optionally limit the drawing of its subviews so that any parts of them outside the view are not shown. This is called clipping. To enable clipping we set the `clipsToBounds` property to true.
- If a view’s size is changed then its subviews can be resized automatically.

