# Introduction

So you're a beginner struggling with sizing and positioning elements in CSS, or maybe you're a seasoned veteran looking for a quick reminder on the basics. In either case, I've got you covered. This topic can be quite tricky to grasp at first, but at the end of this article, I assure you a good working knowledge of this concept.  

# What is CSS?

Do I really need to explain what CSS is to you again? Oh well. 
**CSS** (Cascading Style Sheets) is used to style and layout web pages — for example, to alter the font, color, size, and spacing of your content, split it into multiple columns, or add animations and other decorative features. To ***cascade*** means to stack or build up something one layer at a time. 
CSS is a stylesheet language used to describe the presentation of a webpage written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) or [XML](https://developer.mozilla.org/en-US/docs/Web/XML/XML_introduction). It describes to the browser how elements should be rendered on screen. 
Think of HTML as the skeleton - structure -  of  a webpage and CSS as the flesh, skin and hair, making the site more appealing.  

## 3 Methods of using CSS 

1. Inline: Here the CSS code is placed within the HTML tags themselves using the "style" keyword.
```html
<div style="property: value;"></div>
```
2. Embedded: This is the use of the "style" tag within a HTML document to contain all the CSS code for a Web page.  

```html
<style>
	element {
		property: value;
	}
</style>
```  

3. External file: The HTML file is linked to an external CSS file containing the styling information using the `link` tag. This is my favorite because it allows you to have multiple, separate, well-structured files rather than one large HTML file.
```html
<link rel="stylesheet" href="styles.css">
```  

# Let's get into it...
---

## Overview of the CSS Box Model
To understand how to arrange elements on a webpage, you first need to understand how these elements are displayed on the screen in the first place, this is where the CSS Box Model comes in.
Every HTML tag or element has what I'll call an invisible box around them. 

### Components of the Box Model:
> `Content`:  the stuff (text, images etc.) within the tag/element  
> `Padding`:  the space within the box, separating the content from the walls of the box  
> `Border`:  the line around the perimeter of the box  
> `Margin`:  the space outside the box, separating that box from the other elements in that   webpage.  
> `Dimensions`:  the width and height of the box  
> `Position`:  the location of the box within the page  

This diagram below illustrates the box model.
<img src="Illustrations/Pasted image 20240227222200.png" width = "500"/>

What we're really interested in at the moment is the position of the box surrounding an element. Like I said earlier, the position of a box is the location of that box within the page. To correctly position and element you need to understand a few keywords:
#### 1. `position` property:

``` css
element {
	position: static|relative|absolute|fixed;
} 
```

- `static`: This is the default position for every HTML element. It keeps an element in its original position in the page flow. The element can not be offset in this state and can only be moved around by adjusting margins.
- ``relative``: Here, the elements are kept in their original position in the page flow as well but the now can be offset with respect to their original (`static`) position.
- ``absolute``:  In simple terms, absolute positioning takes an element out of the regular page flow and offsets its position with respect to the closest "non-static" element which is usually the browser window or any parent element set to a position property other than the default static .
- ``fixed``: Pretty similar to  `absolute` but, as the name implies, when applied, the element retains a fixed position on the screen, regardless of scrolling action. The position of the element is with respect to only the browser window.
#### 2. `top|left|bottom|right` property:
specifies the position of an element based on an offset relative to the corresponding side of the box model and the space - represented by some value and a unit of measurement.

```css
element {
	position: relative|absolute|fixed;
	top|left|bottom|right: value(unit);
}
```

## Units
There are multiple units of measurement in CSS. From the ones you know and love to some abstract units that wouldn't seem to make sense at first. Here are some of them:

| Class    | Units     | Rationale                                                                  |
| -------- | --------- | -------------------------------------------------------------------------- |
| pixel    | px        | individual pixels on the monitor                                           |
| percent  | %         | percentage of the screen width or height                                   |
| metric   | m, cm, mm | standard metric units from geometry                                        |
| imperial | ft, in    | alternative to metric units                                                |
| viewport | vw, vh    | percentage (1/100) of the width or height of the viewport (browser window) |

# Examples

To demonstrate what we've learnt so far let's make use of this example.  Open your text editor and follow along.

The example contains three simple boxes made using ``div`` elements and they are contained within a larger ``div`` - outlined in black. I made use of the ***box*** class to set the dimensions  and the fill of the boxes to keep them consistent and I changed the color of each box using inline CSS.

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<title>LazyCoder's Blog</title>
	<style type="text/css" >
		.box {
			text-align: center;
			line-height: 100px;
			font-size: 25pt;
			width: 100px;
			height: 100px;
			margin: 0px;
		}
	</style>
</head>
<body>
	<div style="border: 1px solid;">
		<div class="box" style="background: red;">1</div>
		<div class="box" style="background: yellow;">2</div>
		<div class="box" style="background: blue;">3</div>
	</div>
</body>
</html>

```

<img src="Illustrations/Pasted image 20240304112432 1.png<img src="Illustrations/"/>
The three boxes are in their original position - ``static`` - within the page flow. No changes have been made yet.

## Relative

Let's see what happens when we make block 2 relative.

```html
<div style="border: 1px solid;">
	<div class="block" style="background: red;">1</div>
	<div class="block" style="background: yellow; position:                    relative; left: 100px;">2</div>
	<div class="block" style="background: blue;">3</div>
</div>
```

![[Pasted image 20240304112532 1.png]] Block 2 now leaves a 100px gap to its left. The relative position enables us to move an element around with respect to its original position.

## Absolute

Now let's set the position of box 3 to absolute. We can pin it to the bottom-right corner by setting both the bottom and the right offset values to 0 pixels.
```html
<div style="border: 1px solid;">
		<div class="box" style="background: red;">1</div>
		<div class="box" style="background: yellow; position:                      relative; left: 100px;">2</div>
		<div class="box" style="background: blue; position: absolute;              bottom: 0px; right: 0px;">3</div>
 	</div>
```


![[Pasted image 20240304113530 1.png]]
Observe the position of box 3. Also notice that the containing div now outlines only boxes 1 and 2

Something else to note is that the absolute position is taken with respect to the closest containing non-static element. So when we set the containing div to relative, the position of the box adjusts to the bottom right corner of the containing div instead.
``` html
	<div style="border: 1px solid; position: relative;">
		<div class="box" style="background: red;">1</div>
		<div class="box" style="background: yellow; position:                      relative; left: 100px;">2</div>
		<div class="box" style="background: blue; position: absolute;              bottom: 0px; right: 0px;">3</div>
	</div>

```

<img src="Illustrations/Pasted image 20240304114843 1.png" />

## Fixed

Finally, to demonstrate the fixed position let's make use of box 1. 

```html
<div style="border: 1px solid; position: relative;">
		<div class="box" style="background: red; position: fixed;">1</div>
		<div class="box" style="background: yellow; position: relative; left: 100px;">2</div>
		<div class="box" style="background: blue; position: absolute; bottom: 0px; right: 0px;">3</div>
</div>
```

<img src="Illustrations/Pasted image 20240304114843 1.png" />

Observe that merely changing the position property keeps the box at its previous position unless you specify otherwise. Also box 1 has been taken out of the container div, the outline now contains only the yellow box 2 which is still set to relative position.

```html
<div style="border: 1px solid; position: relative;">
		<div class="box" style="background: red; position: fixed; left: 0px; top: 0px;">1</div>
		<div class="box" style="background: yellow; position: relative; left: 100px;">2</div>
		<div class="box" style="background: blue;">3</div>
</div>
```

<img src="Illustrations/Pasted image 20240304115319 1.png"/>
This shows that box 1 is positioned relative to the browser window. I have pinned it to the top left corner. This property is applied to headers of webpages.
# Conclusion

With these examples you should have a good understanding of the process of positioning elements in CSS. I implore you to experiment as much as possible, move things around as you see fit or better yet, work on a small project to demonstrate what you've learnt.
