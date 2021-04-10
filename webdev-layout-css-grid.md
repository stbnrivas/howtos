# css-grid layout

The css grid layout, was designed as a two-dimensional layout model which controls columns and rows together.


concepts:
- grid container:
- grid item:
- grid track:
- grid lines
- grid area: space surrounded by 4 grids lines
- implicit grid
- explicit grid





## grid skeleton

```html
<div class="container">
    <!-- grid work even without div -->
</div>

<div class="container">
    <div class="cell"></div>
    <div class="cell"></div>
    <div class="cell"></div>
    <div class="cell"></div>
    <div class="cell"></div>
    <div class="cell"></div>
</div>
```

```css
.container{
    display:grid;

    grid-template-rows: 100px 100px 100px;
    grid-template-columns: 100px 100px;
}


.container{
    display:grid;

    grid-template-rows: repeat(3, 100px);
    grid-template-columns: repeat(2, 100px);
}


.container{
    display:grid;

    grid-template: repeat(3, 100px) / repeat(2, 100px);
}
```



## grid container

```css
.container {
    display:grid|inline-grid;
    grid-auto-flow: row|column|row dense|column dense;
    grid-template-columns: 100px 20em 5vw 20% 1fr repeat(2,1fr) ;
    grid-template-rows: repeat(4,fit-antent)
    grid-column-gap:1vw;
    grid-column-gap:1vw;

    justify-items: center|start|end|stretch;
    align-items:

    justify-content:
    align-content:center|start|end

}
```
## grid items

```css
    grid-template-columns
    grid-template-rows
    grid-template-areas
    grid-template
    grid-auto-columns
    grid-auto-rows
    grid-auto-flow
    grid
    grid-row-start
    grid-column-start
    grid-row-end
    grid-column-end
    grid-row
    grid-column
    grid-area
    grid-row-gap
    grid-column-gap
    grid-gap

/* css functions */

    repeat()
    minmax()
    fit-content()
```


```css
    .wrapper{
        display:<grid|inline-grid>;

        grid-template-columns:<length> <percentage> <flex> <max-content> <min-content> <minmax(min, max)>
        grid-template-rows:<length> <percentage> <flex> <max-content> <min-content> <minmax(min, max)>


        grid-template-columns: 20px repeat(6, 1fr) 20px | repeat(4,fit-antent);

        grid-template-rows:

        grid-column-gap:1vw;
        grid-column-gap:1vw;

        grid-auto-rows: minmax(100px, auto)
        grid-gap:


        grid-auto-flow: row|column|row dense|column dense;


        justify-items: center|start|end|stretch;
        align-items:

        justify-content:
        align-content:center|start|end
    }

        .grid-item{
            grid-column:
            grid-row:

            grid-column-start:
            grid-column-end:
            grid-row-start:
            grid-row-end:
        }
```






## example 1 columns

```html
<section class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</section>
```

```css
.container{
    display:grid;
    /* grid-template-columns: 200px 200px 200px; */
    grid-template-columns: 25% 200px 25%;
}


```


## example 1 rows


```html
<section class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</section>
```

```css
.container{
    display:grid;
    grid-template-columns: 200px 200px 200px;
    grid-template-rows: 25% 200px 25%;
}


```



## grid areas


```
<section class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</section>
```

```
.container {
    display:grid;
    grid-template-areas:
        "header  header"
        "sidebar main"
        ".       footer"
}

.box-one   { grid-area: "header"; }
.box-two   { grid-area: "sidebar"; }
.box-three { grid-area: "main"; }
.box-four  { grid-area: "footer"; }

```






## grid [column|row] start end

```css
.container {
    display:grid;
    grid-template-columns: repeat(5, 20%);
    grid-template-rows: repeat(5, 20%);
}


    .row-one {
        grid-column-start:1;
        grid-column-end:6;
    }

    .row-two {
        grid-column-start:1;
        grid-column-end: span 2;
    }

    .row-two {
        grid-column:1 / 3;
    }
```


```css
.container {
    display:grid;
    grid-template-columns: repeat(5, 20%);
    grid-template-rows: repeat(5, 20%);
}


    .row-one {
        grid-row-start:1;
        grid-row-end:6;
    }

    .row-two {
        grid-row-start:1;
        grid-row-end: span 2;
    }

    .row-two {
        grid-row:1 / 3;
    }
```


```css
.container {
    display:grid;
    grid-template-columns: repeat(5, 20%);
    grid-template-rows: repeat(5, 20%);
}

    .row-one {
        grid-area: <grid-row-start> / <grid-column-start> / <grid-row-end> / <grid-column-end>
    }

```