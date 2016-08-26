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
