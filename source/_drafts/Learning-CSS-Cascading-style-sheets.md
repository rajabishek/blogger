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

Styles can be defined at three different levels in css, these are inline, embedded and external styles. Inline styles override embedded styles which in turn override external styles. The inline styles are written in the html markup itself using the style attribute on the html element as shown below.
```html
<p style="color:black; font-size: 14px;">This is a paragraph</p>
```
Embedded styles are written in the head of the document inside the `<style>` tags as shown below.
```html
<head>
	<style>
		p {
			font-size: 14px;
			font-weight: 200;
			color: black;
		}

		body {
			background: yellow;
		}
	</style>
</head>
```
With external styles the CSS is written in a separate css file and is linked to the markup document using the link tag as shown below.
<head>
	<link rel="stylesheet" type="text/css" href="css/style.css">
</head>
There is also another way to link external styles instead of the link tag as shown below. This is not however recommended and not so widely used.
```html
<head>
	<style type="text/css">
		@import url("css/style.css");
	</style>
</head>
```
The following [CSS Reference](http://reference.sitepoint.com/css) is very useful for referring to CSS formatting rules. You can also look at [Can I use](http://caniuse.com) which talks about the compatibility of CSS rules across multiple browsers. Also you may find it interesting to look at [Position is everything](http://positioniseverything.net) website which talks about the browser quirks and bugs.

Browser specific code designed to combat an error is called as a hack. Fixing a bug in one browser can occasionally lead to an error in another. At minimum hacks add weight to your code and make them harder to maintain. Hacks often break in future browser versions. We should avoid hacks whenever possible and also try to avoid conditions that trigger the browser error.

Place all IE specific code fixes in a separate style sheet and these style sheets can be served through conditional comments. Your sites will not look the same in all browser accept it. Always try your best to design according to the existing web standards to support large number of possible browsers.

Use meaningful tags to write the html. Focus on using clear, semantic code. Express the content in a semantic way. Structure your code consistently throughout your site. Simplify your code whenever possible and avoid non semantic markup. Lets look at some of the selectors that are available in CSS.
```css
p {
	...
	...
}
``
As you can see above we are targeting every single paragraph element. This is called as an element selector. We also have something called as class selectors as shown below. This targets all elements with a class of `class-name`. 
```css
.class-name {
	...
	...
}
```
We can also target elements based on the value of the id attribute. The following CSS declaration targets an element with is value as id-value.
```css
#id-value {
	...
	...	
}
```
When a class and id selector conflict with each other, the id selector styling will be used in favor of the class because it is more specific. id and classes are not just for adding styles they also add meaning to the markup. We can also mention the element before the class or the id selector in this way only the specified element with the class or id will be targeted, other elements will not be taken into account.
```css
h1#id-name {
	...
	...
}

h2.class-name {
	...
	...
}
```
Even of other elements had this id or class name then these formatting rules won't apply. These are called as element specific selectors. We can also style every single element on the page by using the universal selector. It is as though you apply the formatting rules individually to every single element on the page. The syntax of a universal selector is shown below.
```css
* {
	...
	...
}
```
```css
p {
	color:black;
	marging-bottom:10px;
}

h1 {
	color:black;
	marging-bottom:10px;
}
```
If we notice ourselves writing the same CSS formatting rules for multiple elements was shown above then we can combine the declaration by grouping the selectors as shown below.
```css
p, h1 {
	color:black;
	marging-bottom:10px;
}
```
Next lets take a look at descendant selectors. This targets an element that is a descendant of another html element.
```css
div p {
	...
	...
}

.outer div p {
	...
	...
}
```
As you can see above the first declaration targets any paragraph element that is nested inside of a div element. The second targets any paragraph element which is nested inside a div and that div being nested inside of an element with a class as outer. One thing to remember here is that the descendant need not be the immediate child. But there is a css selector that can used to target elements based being an immediate child of its parent. This is called as a child selector. The following CSS rules targets a h2 element which is a immediate child of an article tag.
```css
article > h2 {
	...
	...
}

aside ol > li {
	...
	...
}
```
We can also combine descendant selectors and child selectors. The second declaration shown above targets all li elements that are direct children of a ol element which are descendants of some article tag. We can also target elements based on an element following an another using an adjacent selector. The following CSS rule targets all paragraph elements that immediately follows a h2 element and both have the same parent.
```css
h2 + p {
	...
	...
}

h1 + h2 + p {
	...
	...
}
```
Target p that immediately comes after h2, which immediately comes after h1. h1, h2 and p have the same parent. Similarly we can also target elements based on an attribute. The following css declaration targets any element that has a title attribute.
```css
a[title] {
	...
	...
}

a[title="visit google"] {
	...
	...
}
```
The second declaration targets an anchor element that has a title attribute with a value of `visit google`. When targeting elements based on the attribute value we can also use pattern matching.
```css
p[class~="red"] {
	...
	...
}
```
The above CSS declaration targets elements in which red occurs as the class value in a whitespace word separated list. For example elements having the following class values would succeed - "red white blue", "yellow red green" etc. We can also traget elements with a beginning attribute value as shown below.
```css
a[href^="http://"] {
	...
	...
}
```
We can also target elements ending in a attribute value. The following declaration targets a anchor tag where the href attribute value ends in .com.
```css
a[href$=".com"] {
	...
	...
}
```
We can also target elements with an attribute containing a specific value as shown below.
```css
a[href*="google"] {
	...
	...
}
```
The above CSS declaration targets anchor elements with href attribute containing the value google in them.
