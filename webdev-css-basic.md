# css basic


## sizing elements

```
    |-------------------------------------------------------------------------------|
    | margin                                                                        |
    |        |----------------------------------------------------------|           |
    |        | border                                                   |           |
    |        |         |---------------------------------------|        |           |
    |        |         | padding                               |        |           |
    |        |         |          |-----------------|          |        |           |
    |        |         |          |      w x h      |          |        |           |
    |        |         |          |-----------------|          |        |           |
    |        |         |                                       |        |           |
    |        |         |---------------------------------------|        |           |
    |        |                                                          |           |
    |        |----------------------------------------------------------|           |
    |                                                                               |
    |-------------------------------------------------------------------------------|

```

```css
*, *::before, *::after {
	box-sizing:border-box;
}
```


```
.element { box-sizing: content-box; /*by default*/ }

If you set an element's width to 100 pixels, then the element's content box will be 100 pixels wide, and the width of any border or padding will be added to the final rendered width, making the element wider than 100px.

width  = margin-left + border-left + w + border-right  + margin-right
height = margin-top  + border-top  + h + border-botton + margin-botton
```





```
.element { box-sizing: border-box }

If you set an element's width to 100 pixels, that 100 pixels will include any border or padding you added, and the content box will shrink to absorb that extra width. This typically makes it much easier to size elements.


```

It is often useful to set box-sizing to border-box to layout elements. This makes dealing with the sizes of elements much easier, and generally eliminates a number of pitfalls you can stumble on while laying out your content.  On the other hand, when using position: relative or position: absolute, use of box-sizing: content-box allows the positioning values to be relative to the content, and independent of changes to border and padding sizes, which is sometimes desirable.




## display property

```
.element{ display:absolute; }
.element{ display:relative; }

.element{ display:block; }
.element{ display:inline; }
.element{ display:inline-block; }

.element{ display:flex; }
.element{ display:grid; }
```


## measurement units

1. Absolute

- px
- pt
- in
- cm
- mm


2. Relative

- `%`
```css
.element{
	width: 50%;  /* means 50% from the width of the parent    */
	height: 50%: /* means 50% from the height of the parent   */
	             /* block element have 100% width to default  */
	             /* block element have 0 height to default    */
	             /* inline element have a fixed to content    */
	             /* cascading relative width between parent and children do a "auto sizing" */
}
```

- `vw` (viewport width)
- `vh` (viewport height)

- `em`

```
.element{
	width: 10em; /* 10 x font size */
}
```

- `rem`

```
.element{
	width: 10rem; /* 10 x font size of the root element */
}
```


## position

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="index.css">
  <title>Document</title>
</head>
<body>
  <div class="boxes">
    <div class="box"></div>
    <div class="box box-one">a</div>
    <div class="box"></div>
    <div class="box box-two position-relative-left">b</div>
    <div class="box box-three position-relative-right">c</div>
    <div class="box box-four position-relative-top">d</div>
    <div class="box box-five position-relative-bottom">e</div>
    <div class="box box-six position-relative-top">f</div>
    <div class="box"></div>
  </div>
  <div class="boxes-relative-absolute">
    <div class="box box-seven position-absolute">g</div>
    <div class="box box-eight">h</div>
    <div class="box box-nine">i</div>
  </div>
  <div class="boxes-fixed">
    <div class="box position-fixed">j</div>
  </div>
</body>
</html>
```

```css
body {
  background-color: #3F3F3F;
  color:#AE6600;
}

.box {
  width:5rem;
  height: 5rem;
  border: 1px solid #FFF;
}

.box-one{ background-color: #111; }
.box-two{ background-color: #222; }
.box-three{ background-color: #333; }
.box-four{ background-color: #444; }
.box-five{ background-color: #555; }
.box-six{ background-color: #666; }
.box-seven{ background-color: #777; }
.box-eigth{ background-color: #880; }
.box-nine{ background-color: #999; }

/*    */
.boxes {
  margin-left: 5rem;
}
  .position-static { position:static; }

  .position-relative-left { position:relative; left:5rem;}
  .position-relative-right { position:relative; right:5rem;}
  .position-relative-top { position:relative; top:5rem;}
  .position-relative-bottom { position:relative; bottom:5rem;}

/*    */
.boxes-relative-absolute { position:relative;}

    .position-absolute {
      position:absolute;
      right: 0;
      bottom: 0;
    }

/*    */
.boxes-fixed { position:relative;}

  .position-fixed { position:fixed; top:0; right:0;}


.position-sticky { position:sticky;}
```



1. `position:static`

Default. the element is positioned according to the normal flow of the document. The top, right, bottom, left, and z-index properties have no effect. This is the default value.

2. `position:relative`

*relative to itself^*

The element is positioned according to the normal flow of the document, and then offset relative to itself based on the values of top, right, bottom, and left.
The offset does not affect the position of any other elements; thus, the space given for the element in the page layout is the same as if position were static.

3. `position:absolute`

*the parent should has `position:relative`*
*itself element has `position:absolute`*

The element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial containing block. Its final position is determined by the values of top, right, bottom, and left.
This value creates a new stacking context when the value of z-index is not auto. The margins of absolutely positioned boxes do not collapse with other margins.

4. `position:fixed`

The element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to the initial containing block established by the viewport, except when one of its ancestors has a transform, perspective, or filter property set to something other than none (see the CSS Transforms Spec), in which case that ancestor behaves as the containing block. (Note that there are browser inconsistencies with perspective and filter contributing to containing block formation.) Its final position is determined by the values of top, right, bottom, and left.

6. `position:sticky`

The element is positioned according to the normal flow of the document, and then offset relative to its nearest scrolling ancestor and containing block (nearest block-level ancestor), including table-related elements, based on the values of top, right, bottom, and left. The offset does not affect the position of any other elements.

This value always creates a new stacking context. Note that a sticky element "sticks" to its nearest ancestor that has a "scrolling mechanism" (created when overflow is hidden, scroll, auto, or overlay), even if that ancestor isn't the nearest actually scrolling ancestor.



## visibility

```css
.element {
	display: none; /* the space for element is NOT reserved */
}

.element {
	visibility: hidden; /* the space for element is reserved */
}
```













## medias queries


```
@media screen and (min-width: 600px) and (max-width: 900px){
	/* */
}
```
