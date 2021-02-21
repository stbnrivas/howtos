# semantic html 5

1. google paragraph description

```
<meta name="twitter:description" content="Wolfram|Alpha brings expert-level knowledge and capabilities to the broadest possible range of people—spanning all professions and education levels.">

<meta name="description" content="Compute answers using Wolfram's breakthrough technology &amp; knowledgebase, relied on by millions of students &amp; professionals. For math, science, nutrition, history, geography, engineering, mathematics, linguistics, sports, finance, music…">
```

2. use header in a hierachical way. Only h1, multiples h2...


3. `<b></b>`  and `<i></i>` do not semantic don't use. Use `strong` and `emp`


4. don't use anchor with relative url at html this is a messy, use anchor with absolute

5. use download attribute for anchor

```
<a href="https:///pdf/2021.pdf" download>year 2021</a>

<a href="https://ahrefs.com" rel="nofollow">blue text</a>
```

6. `div` and `span` are general purpose but `article` `figure` `mark` `time`are more explicit

- `article` an independent , self-contained content useful for: forum post, comments, reviews, product cards

- figure

```
<figure>
	<img src="" alt="">
</figure>
```



7. `header`, `main`, `aside`, `footer`

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<header>
		<nav>
			<ul>
				<li></li>
				<li></li>
				<li></li>
			</ul>
		</nav>
	</header>
	<main>
		<section></section>
		<section></section>
		<section></section>
	</main>
	<aside></aside>
	<footer>
		<nav>
			<ul>
				<li></li>
				<li></li>
				<li></li>
			</ul>
		</nav>
	</footer>
</body>
</html>
```

8. nesting is right


```html
<section>
	<h2></h2>
	<article>
		<section>
			<header></header>
			<main></main>
			<footer></footer>
		</section>
		<section></section>
		<section></section>
	</article>
	<article></article>
	<article></article>
</section>
```






# layout