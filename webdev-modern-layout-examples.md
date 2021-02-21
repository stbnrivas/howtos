#


http://1linelayouts.glitch.me/




01. super center


```html
<div class="parent" >
  <div class="child" contenteditable>:)</div>
</div>
```


```css
.parent {
  display: grid;
  place-items: center;

}

.child { }

```


02.

not interesting for me





03. sidebar min/max

```html
<div class="parent">
	<div class="section yellow" contenteditable>
	Min: 150px / Max: 25%
	</div>
	<div class="section purple" contenteditable>
	This element takes the second grid position (1fr), meaning
	it takes up the rest of the remaining space.
	</div>
</div>
```

```
.parent {
	display: grid;
	grid-template-columns: minmax(150px, 25%) 1fr;
}
```



04. header, main, footer in single column

```
<div class="parent">
	<header class="blue section" contenteditable>Header</header>
	<main class="coral section" contenteditable>Main</main>
	<footer class="purple section" contenteditable>Footer Content</footer>
</div>
```

```
.parent {
	display: grid;
	grid-template-rows: auto 1fr auto;
}
```



05. header | left-sidebar, main-content, right-sidebar | footer

(the classic holy grail layout)


```
<div class="parent">
	<header class="pink section">Header</header>

	<div class="left-side blue section" contenteditable>Left Sidebar</div>
	<main class="section coral" contenteditable> Main Content</main>
	<div class="right-side yellow section" contenteditable>Right Sidebar</div>

	<footer class="green section">Footer</footer>
</div>
```

```
.parent {
  display: grid;
  grid-template: auto 1fr auto / auto 1fr auto;
}

	header {
		padding: 2rem;
		grid-column: 1 / 4;
	}

	.left-side {
		grid-column: 1 / 2;
	}

	main {
		grid-column: 2 / 3;
	}

	.right-side {
		grid-column: 3 / 4;
	}

	footer {
		grid-column: 1 / 4;
	}
```



06. span grid


```
<div class="parent white">
	<div class="span-12 green section">Span 12</div>
	<div class="span-6 coral section">Span 6</div>
	<div class="span-4 blue section">Span 4</div>
	<div class="span-3 yellow section">Span 3</div>
</div>
```

```
.parent {
	display: grid;
	grid-template-columns: repeat(12, 1fr);
}

.span-12 {
	grid-column: 1 / span 12;
}

.span-6 {
	grid-column: 7 / span 6;
}

.span-4 {
	grid-column: 3 / span 4;
}

.span-3 {
	grid-column: 3 / span 3;
}

/* centering text */
.section {
	display: grid;
	place-items: center;
	text-align: center
}
```


07.

not interesting for me




08. Line Up

horizontal align colums


```
<div class="parent white">

    <div class="card yellow">
      <h3>Title - Card 1</h3>
      <p contenteditable>Medium length description with a few more words here.</p>
      <div class="visual pink"></div>
    </div>

    <div class="card yellow">
      <h3>Title - Card 2</h3>
      <p contenteditable>Long Description. Lorem ipsum dolor sit, amet consectetur adipisicing elit.</p>
      <div class="visual blue"></div>
    </div>

    <div class="card yellow">
      <h3>Title - Card 3</h3>
      <p contenteditable>Short Description.</p>
      <div class="visual green"></div>
    </div>

</div>
```


```
.parent {
	height: auto;
	display: grid;
	grid-gap: 1rem;
	grid-template-columns: repeat(3, 1fr);
}

	.card {
		display: flex;
		flex-direction: column;
		padding: 1rem;
		/* justify-content: space-around; */
		justify-content: space-between;
	}

		.visual {
			height: 100px;
			width: 100%;
		}
```




09. clamping my style (grow until max size)

```
 <div class="parent white">
    <div class="card purple">
      <h1>Title Here</h1>
      <div class="visual yellow"></div>
      <p>Descriptive Text. Lorem ipsum dolor sit, amet consectetur adipisicing elit. Sed est error repellat veritatis.</p>
    </div>
  </div>
```


```
.parent {
    display: grid;
    place-items: center;
}

	.card {
	    width: clamp(23ch, 50%, 46ch);
	    display: flex;
	    flex-direction: column;
	    padding: 1rem;
	}

	.visual {
	      height: 125px;
	      width: 100%;
	}

```



10. respect aspect ratio

```
<div class="parent white">
	<div class="card blue">
	  <h1>Video Title</h1>
	  <div class="visual green"></div>
	  <p>Descriptive Text. This demo works in Chromium 84+.</p>
	</div>
</div>
```


```
.parent {
	display: grid;
	place-items: center;
}

  .card {
    width: 50%;
    display: flex;
    flex-direction: column;
    padding: 1rem;
  }

  	.visual {
    	aspect-ratio: 16 / 9;
  	}
```