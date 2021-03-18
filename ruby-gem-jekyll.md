# jekyll static site builder

THE GOOD: jekyll has the themes gemifyed, to change theme you have to install gem theme and persist it into jekyll folder by copying from gem
THE BAD:  jekyll never reload  the `_config.yml` file
THE UGLY


## jekyll CLI

1. launch server

```bash
cd blog
bundle exec jekyll serve

bundle exec jekyll serve --livereload

bundle exec jekyll serve --draft
```

2. update

```bash
$ bundle update jekyll
```


3. how to reload full including `_config.yaml` NOT WORKING

```
npm i -g watchy

nodenv rehash

watchy -w _config.yml -- "bundle exec jekyll serve --watch"
```



## front-matter


```
---
layout: post
title: "post title"
date: 2020-06-20 00:59:59 -0700
categories: jekyll categories

# own created
author: "me"
---
```


## pages

- pages live into root folder like index.markdown
- pages has a layout into front-matter

## posts

- posts is the minimal page that jekyll must to have
- also use a layout
- published post live into `_posts` folder
- drafts live into `_drafts` folder

## layouts


check your front-matter into your files

 - about.markdown   `page`
 - index.markdown   `home`

```
tree _layouts

_layouts
├── default.html
├── home.html
├── page.html
└── post.html

```

but the logical insertion is like


```


_layouts
├── default.html
│   ├── _includes/head.html
│   ├── _includes/header.html
│   ├── content {home,page,post}
│   └── _includes/footer.html
│
├── home.html   // are pages and inside declare using `layout: default`
├── page.html   // are pages and inside declare using `layout: default`
└── post.html   // are pages and inside declare using `layout: default`

```


now we will see the file into root folder





ergo there are two layouts which are embedded into default

```
│
├── index.markdown  [layout: home] / [layout: default]
├── about.markdown  [layout: page] / [layout: default]
│
└── 404.html

	default
```


## data

the folder named `_data` can be used to store data in yml, json ... an example person.data


```
{{ site.data.people }}
```


```
<ul>
{% for person in site.data.people %}
	<li>{{person.name}}, {{person.surname}}</li>
{% endfor %}
</ul>
```


## static files

should be into `assets` folder

```
{% for file in site.static_files %}
	{{ file.name }} {{ file.url}}
{% endfor %}
```


## github pages with jekyll

- create new repo without README.md

- add `baseurl: ...` to `_config` file


