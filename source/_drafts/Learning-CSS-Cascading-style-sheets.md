---
title: Learning CSS - Cascading style sheets
tags:
---
## Introduction
CSS is a stylesheet language. It controls the presentation of the markup language documents. HTML controls the structure of the document and CSS controls the presentation. CSS essentially consists of formatting rules that describe how the content should be presented visually on the page. Styles are applied in order they are found cascading down from external to local styles.

<!-- more -->

An important thing to keep in mind before anyone begins writing CSS is that browsers have default stylesheets. Whenever you don't write any stylesheets for the pages it is usually called as an unstyled document. It is wrong to call them this way because the pages have some default styles already defined, it is just that they are poorly styled. Browsers have default stylesheets to style the markup documents. The default stylesheets differ slightly from one browser to another. Whenever to define any styles using CSS rules you are essentially overriding these default browser styles. 

Sometimes you may be confused when you may see styles which you haven't defined but are present in your document, these are coming from the default stylesheet. This confusion has even resulted in its own technique called as CSS reset which a collection of styles which are first written that zero out the browser default styles giving you a consistent point to begin writing styles. You can visit [CSS reset](http://cssreset.com) which is website having links to the popular CSS resets that are currently available.

## Syntax
![Screenshot 1](/img/learning-css/css-syntax.png)

The above is a valid CSS syntax. There are two main sections, the yellow area is the selector and the blue area is called as declaration. The selector is used to target the element to be styled. The declaration portion consists of a set of formatting rules to style the target element. The red area is called as a formatting rule. Every formatting rule has a property and a value.

We also have something called as inline rules which are typically used to group style definitions together, for example `@font-face`, `@media`, `@import`, `@page` etc. And there is only one type of a comment in CSS as shown below.
```css
/* This is a comment */
```
