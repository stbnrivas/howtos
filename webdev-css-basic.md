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

```