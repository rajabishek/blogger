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

## Units of measurement
There are two broad categories one is **absolute** and the other one is **relative**. Absolute values are well suited for devices with a known output size(like printer). Some examples of absolute values are as follows:
- in - inches
- cm - centimeters
- mm - millimeters
- pt - points
- pc - picas

Relative values are well suited for devices like screens, where the device size and resolution is not known or could change.
- em - ems
- ex - exes
- px - pixels
- gd - grids
- rem - rootems
- vw - viewport width
- vh - viewport height
- vm - viewport minimum
- ch - character
The units gd, vw, vh, vm are brand new in CSS3. gd is widely used in east asian typography. vw, vh, vm allows us to size elements based on the browser size. Now lets discuss a bit about the ems unit of measurement. The way how measurement works depends on where the value is used. When used with the font-size property lets say its is set a x ems, then the font size is x times the font size of the parent element. Look at the following HTML markup.
```html
<body>
	<h1>This is main heading</h1>
	<h2>This is the sub heading</h2>
	<h3>This is another sub heading</h3>
	<p>This is a paragraph</p>
</body>
```
Now consider the following CSS rules for the above markup.
```css
body { font-size: 100%; } //Font size is default font size of the device
h1 { font-size: 1.6em; } //Font size is 1.6 times font size of body
h2 { font-size: 1.4em; } //Font size is 1.4 times font size of body
h3 { font-size: 1.2em; } //Font size is 1.2 times font size of body
p { font-size: 1em; } //Font size is 1 times font size of body
```
If ems are used anywhere else other than the `font-size` property then its value is equal to the computed size of the text of that element. For example look at the following CSS declaration.
```css
h1 {
	font-size: 2em; //Font size of 2 times the font size of the parent element let the value be y
	margin-bottom: 3em; // The bottom margin value is 3 times y
}
```
So as you can see above the font size of h1 is 2 times the font size of the parent. Lets say the parent element is body and no font-size property is set on the body tag, then the font size of body is the default font size of the device. The ex unit os measurement is similar to ems, they are based on the x-height of a font. Root ems are also like ems, only that they are relative to the root element like body or html rather than the element's immediate parent. 

Lets also look at percentages, another unit of measurement thats not exactly considered as length. Percentage values are calculated relative to their parent element. A div with a width of 80% would use 80% of its parent element's width. While a paragraph with its font-size set to 80% would size the text at 80% of the size of its parents text.