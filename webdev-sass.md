# sass cli 

```bash
# simple compilation
sass  input.scss:output.css
```

```bash
# watch for changes and recompile if neeeded
sass --watch inputFolder:outputFolder
```

```bash
# can be compact, compressed, expanded
sass --style compressed input.scss:output.css
```


# sass with scss sintax


## importation another file

```sass
/* _vars.scss*/
$mainColor: #000;
/* main.scss*/
@import "_vars.scss"
body{
	color:$mainColor;
}
```

```css
body{
	color:#000;
}
```


## variables declaration


```sass
$defaultColor:#000000;

a{color:$defaultColor;}
```

```css
a{color:#000000;}
```


## nesting


```sass
	ul {
		list-style-type:none
		li {
			margin:0px;
		}
	}
	```

	```css
	ul {
		list-style-type:none
	}
	ul li {
		list-style-type:none
		margin:0px;
	}
```


## operations and functions

```sass
$defaultWindowsSize:960px;
#nav.side{
	width:$defaultWindowsSize/3;
}

```

```css
#nav.side{
	width:320px;
}

```



## mixins

mixins allow reuse of styles without to copy paste them into a non-semantic class

```sass
@mixin default-box{
	$bordercolor: #666;
	border: 1px solid $bordercolor;
	display:inline-block;
}

.box-comment{@include default-box;}
.box-response{@include default-box;}
```

```css
.box-comment{
	border: 1px solid #666;
	display:inline-block;
}
.box-response{
	border: 1px solid #666;
	display:inline-block;
}
```

you can pass power of mixins passing them arguments


```sass
	@mixin default-box($color,$background,$display,$padding){
	display:$display;
	color: $color;
	background:$background;
	padding:$padding $padding $padding $padding;
}
.box-comment{@include default-box(#666,#333,block,10px);}

```

```css
.box-comment{
	display:block;
	color:#666;
	background:#333;
	padding:10px 10px 10px 10px;
}
```


## inheritance with @extend

```sass
%error{
	background: #FDD;
	color:#FFF;
}
.fatalError{
	@extend %error;
	border:solid 1px #F36;
}

```

```css
.error{
	background:#FDD;
	color:#FFF;
}
.fatalError{
	background:#FDD;
	color:#FFF;
	border:solid 1px #F36;
}
```


