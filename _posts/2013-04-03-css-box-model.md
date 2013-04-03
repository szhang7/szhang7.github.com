---
layout: post
title: "CSS Box Model"
description: "The CSS box model is essentially a box that wraps around HTML elements, and it consists of: margins, borders, padding, and the actual content."
category: html
tags: [html, CSS, box, model, margin, border, padding, element]
---
{% include JB/setup %}

This article will summary the knowledge of css box model.

## The CSS Box Model

The CSS box model is essentially a box that wraps around HTML elements, and it consists of: margins, borders, padding, and the actual content.

The image below illustrates the box model:

{{ page.staticpath }}

![css boxmodel](/assets/uploads/ct_boxmodel.gif "css boxmodel")


- Margin - Clears an area around the border. The margin does not have a background color, it is completely transparent
- Border - A border that goes around the padding and content. The border is affected by the background color of the box
- Padding - Clears an area around the content. The padding is affected by the background color of the box
- Content - The content of the box, where text and images appear

## CSS Margin

The CSS margin properties define the space around elements.

### Possible Values

- auto:   The browser calculates a margin
- length: Specifies a margin in px,pt,cm,etc. Default values is 0px
- %     : Specifies a margin in percent of the width of the containing element
- inherit:Specifies that the margin should be inherited from the parent element

### Margin - Individual sides

- margin-top:25px
- margin-right:50px
- margin-bottom:75px
- margin-left:100px

### Margin - Shorthand property

To shorten the code, it is possible to specify all the margin properties in one property. This is called a shorthand property.

- margin:25px 50px 75px 100px   # top:25px right:50px bottom:75px left:100px
- margin:25px 50px 75px         # top:25px right,left:50px bottom:75px
- margin:25px 50px              # top,bottom:25px right,left:50px
- margin:25px                   # all four margins are 25px

## CSS Border

The CSS border properties allow you to specify the style and color of an element's border.

### Border Style

border-style values:

- dotted: Defines a dotted border
- dashed: Defines a dashed border
- solid:  Defines a solid border
- double: Defines two borders.
- groove: Defines a 3D grooved border
- ridge:  Defines a 3D ridged border
- inset:  Defines a 3D inset border
- outset: Defines a 3D outset border

### Border Width

The border-width property is uses to set the width of the border.

The width is set in pixels, or by using one the three pre-defined values:thin,medium,or thick.

### Border Color

The color can be set by:

- name: specify a color name, like "red"
- RGB:  specify a RGB value, like "rgb(255,0,0)"
- Hex:  specify a hex value, like "#ff0000"

### Border - Individual sides

    p{
    border-top-style:dotted
    border-right-style:solid
    border-bottom-style:dotted
    border-left-style:solid}

### Border - Shorthand property

The border-style property can have from one to four values.

- border-style:dotted solid double dashed   # top:dotted right:solid bottom:double left:dashed
- border-style:dotted solid double          # top:dotted right,left:solid bottom:double
- border-style:dotted solid                 # top,bottom:dotted right,left:solid
- border-style:dotted                       # all four borders are dotted

## CSS Padding

The CSS padding properties define the space between the element border and the element content.

### Possible Values

- length: Defines a fixed padding(in pixels,pt,em,etc.)
- %     : Defines a padding in % of the containing element

### Padding - Individual sides

- padding-top:25px
- padding-right:50px
- padding-bottom:75px
- padding-left:100px

### Padding - Shorthand property

To shorten the code, it is possible to specify all the padding properties in one property. This is called a shorthand property.

- padding:25px 50px 75px 100px   # top:25px right:50px bottom:75px left:100px
- padding:25px 50px 75px         # top:25px right,left:50px bottom:75px
- padding:25px 50px              # top,bottom:25px right,left:50px
- padding:25px                   # all four paddings are 25px

## CSS Outline

An outline is a line that is drawn around elements(outside the borders) to make the element "stand out"

The outline properties specify the style, color, and width of an outline.

- outline:        Sets all the outline properties in one declaration
- outline-color:  Sets the color of an outline
- outline-style:  Sets the style of an outline
- outline-width:  Sets the width of an outline
## Refrences ##

- [CSS 框模型概述] (http://www.w3school.com.cn/css/css_boxmodel.asp)

