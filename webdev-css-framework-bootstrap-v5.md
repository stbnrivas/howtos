# bootstrap v5


## responsive helper bootstrap

```
<nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item">
      <a class="page-link bg-info text-white         d-xs-none" href="#">XS</a>
      <a class="page-link                    d-none d-xs-block" href="#">XS</a>
    </li>
    <li class="page-item">
      <a class="page-link bg-info text-white         d-sm-none" href="#">SM</a>
      <a class="page-link                    d-none d-sm-block" href="#">SM</a>
    </li>
    <li class="page-item">
      <a class="page-link bg-info text-white         d-md-none" href="#">MD</a>
      <a class="page-link                    d-none d-md-block" href="#">MD</a>
    </li>
    <li class="page-item">
      <a class="page-link bg-info text-white         d-lg-none" href="#">LG</a>
      <a class="page-link                    d-none d-lg-block" href="#">LG</a>
    </li>
    <li class="page-item">
      <a class="page-link bg-info text-white        d-xl-none" href="#">XL</a>
      <a class="page-link                    d-none d-xl-block" href="#">XL</a>
    </li>
    <li class="page-item">
      <a class="page-link bg-info text-white        d-xxl-none" href="#">XXL</a>
      <a class="page-link                    d-none d-xxl-block" href="#">XXL</a>
    </li>
  </ul>
</nav>
```


## layout

container, row, grid, columns gutters

1. container

```
.container

.container-sm
.container-md
.container-lg
.container-xl
.container-xxl

.container-fluid


<div class="container">

</div>
```

2. row
```
.row

.row-cols-1
.row-cols-2
.row-cols-3
.row-cols-4
.row-cols-5
.row-cols-6
.row-cols-7
.row-cols-8
.row-cols-9
.row-cols-10
.row-cols-11
.row-cols-12

<div class="container">
	<div class="row">
	</div>
</div>
```


3. col
```
.col

.col-2
.col-3
.col-4
.col-5
.col-6
.col-7
.col-8
.col-9
.col-10
.col-11
.col-12

.col-sm
.col-md
.col-ls
.col-xl
.col-xxl

.col-{sm,md,ls,xl,xxl}-{2-12}

.col-auto

<div class="container">
	<div class="row">
		<div class="col"></div>
	</div>
</div>
```



4. gutters

gutters are gaps between column content, created by horizontal padding

```
g   gap  into x, y axis => horizontally and vertically
gx  gaps into x axis => horizontally
gy  gaps into y axis => vertically

g{,x,y}-{0-5}


g{,x,y}-{sm-md-ls-xl-xxl}-{0-5}

```