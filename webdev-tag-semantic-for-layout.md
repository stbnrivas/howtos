# html global attributtes

https://www.w3.org/wiki/HTML/Attributes/_Global


name          values  description
accesskey   list of key labels  A key label or list of key labels with which to associate the element; each key label represents a keyboard shortcut which UAs can use to activate the element or give focus to the element.
An ordered set of unique space-separated tokens, each of which must be exactly one Unicode code point in length.
class   set of space-separated tokens   A name of a classification, or list of names of classifications, to which the element belongs.
contenteditable   "true" or "false" or "" (empty string) or empty   Specifies whether the contents of the element are editable.
contextmenu   ID reference  The value of the id attribute on the menu with which to associate the element as a context menu.
dir   "ltr" or "rtl"  Specifies the element’s text directionality.
draggable   "true" or "false"   Specifies whether the element is draggable.
hidden  "hidden" or "" (empty string) or empty  Specifies that the element represents an element that is not yet, or is no longer, relevant.
id  ID  A unique identifier for the element.
There must not be multiple elements in a document that have the same id value.
Any string, with the following restrictions: 1. must be at least one character long 2. must not contain any space characters
lang  language tag  Specifies the primary language for the contents of the element and for any of the element’s attributes that contain text.
A valid language tag, as defined in [BCP47].
spellcheck  "true" or "false" or "" (empty string) or empty   Specifies whether the element represents an element whose contents are subject to spell checking and grammar checking.
style   string  Specifies zero or more CSS declarations that apply to the element [CSS].
tabindex  integer   Specifies whether the element represents an element that is is focusable (that is, an element which is part of the sequence of focusable elements in the document), and the relative order of the element in the sequence of focusable elements in the document.
title   normal character data   Advisory information associated with the element. 












Semantic Element  Description   Example
--------------------------

<header>  Introduction for the whole page or individual sections, article, nav, aside elements. Typically contains site name, logo, navigation. Does not have to be at the beginning of page.   

<header>
<h1>The Importance of Being Earnest</h1>
<h3>A Quest for Truth and Beauty</h3>
<p>The play was written in 1895 by playwright Oscar Wilde</p>
</header>



<footer>  Includes typical footer information like authoring, copyrights, contact information and a footer menu.  

<footer>
<p>Written by: Oscar Wilde</p>
<p>Contact information: <a href="mailto:oscar@wilde.com">
oscar@wilde.com</a>.</p>
</footer>



<nav>   Navigation links for the document. A page can have more than one 

<nav> element like table of contents, horizontal navigation in header and footer navigation.   <nav><ol>
<li><a href="/act1/">Act 1</a></li>  
<li><a href="/act2/">Act 2</a></li>
<li><a href="/act3/">Act 3</a></li>
</ol></nav>



<section>   Defines sections in the document such as chapters, headers, etc. Typically used on content that cannot make sense on its own.   

<section>
<h1>Act 1 - Scene 1</h1>
<p>Set in the morning room of Algy's flat in Half Moon Street</p>
</section>



<article>   Defines independent content that should make sense on its own outside of the document such as newspaper articles, blog posts, etc.  

<article>
<h1>A blogger's analysis of this brilliant satire</h1>
<p>This witty, sometimes conscious play is Wilde's playground to raise his progressive sentiments...</p>
</article>


<aside>   Side content other than main content, like a sidebar. These are not considered as part of the main page outline.  <p>Algernon's flat is luxuriously and artistically furnished</p>

<aside>
<h3>Algernon Moncrieff</h3>
<p>A wealthy bachelor who lives in a fashionable part of London. He has a good sense of humor and utter lack of respect for society.</p>
</aside>


<details> *see example below  A way to provide additional information that the user can show or hide. Content that is shown to user by default. Other content is hidden and can be expanded to view.  

<details>
<summary>Cast Members</summary>
<p>George Washington as Algernon Moncrieff</p>
<p>Ronald Reagan as John Worthing</p>
</details>


<figcaption> *see example below
  Provides a caption (explanation) of an image. To be used within <figure>.   

<figure>
  <img src="img_cast.jpg" alt="The Importance of Being Earnest Cast">
  <figcaption>Fig1. - The cast hard at work at dress rehearsal before opening night</figcaption>
</figure>


<figure>  Contains an image and can be used to group with an image's caption  Refer to <figcaption>



<mark>  *see example below
  Defines a part of a text you want to highlight. The highlight styling is specified in CSS.  

<h4>Lane: </h4><p>Yes sir. [<mark>Handing his master the sandwiches on a salver</mark>]</p>


<summary>   Used within the <details> tag. Specifies the visible content. The rest of the content in details is shown/hidden by user.   

<details>
<summary>Cast Members</summary>
<p>George Washington as Algernon Moncrieff</p>
<p>Ronald Reagan as John Worthing</p>
</details>





<code>  Used to represent short computer code in a sentence. It displays code in default monospace font.    <p>For larger code snippets, you should use the <code>pre tag</code>.</p>

<abbr>  Used to indicate the occurrence of an abbreviation.   
  <abbr title="Hypertext Markup Language">HTML</abbr>

<br>  Used to introduce a line break in your HTML document.   
<br>

<address>   Used to supply contact information for its nearest <article> or <body> ancestor.  <address>
<a href="www.example.com">John Doe</a><br>
#123, Doe Villa<br>
Los Angeles, USA
</address>

<hr>  Used to introduce a horizontal line in your HTML document.  <p>Hello</p><hr><p>World!</p>



Can you have more than one <header>, <footer> and <nav>?

There is a common misconception that a Web page can only have one header at the start, one footer at the end and one main navigation section to maneuver the site. Header and footer elements are for the parent element (section, article, division or body) that they are used in. If you have multiple sections or articles, then you can have one header and footer for each.

Global header & footer

Header and footer elements can also be used site-wide at the top and bottom of the body of the Web page.




<article> and <section> elements



An article element as we know is stand-alone content. If you pick an article out of a Web page, it should make sense all by itself. In Brad's Blog example in the previous unit, if you extract only the first article, you can see that it will make sense all by itself without any context. It can be reused anywhere else. One article element can be nested inside another. For example, if you have a blog post and you want to include a forum post or newspaper article in it, you can nest it in another <article> tag. 

The section element is used to section a page. For example, chapters in a book, sections in a thesis or splitting an 'about me' page into introduction, interests and skills. Sections can be used in a page or within an article. In fact, all content within the body element is considered to be within one section. Sections can be nested (one section in another). Sections can also be part of an article, aside or nav elements. While the code above makes no sense by itself, if you add it to our CES 2015 <article> example, it will fit right in:

<article>
  <header>
  </header>
  <section>
  </section>
</article>

One article element can be nested inside another, i.e. a blog post can contain a newspaper article like in the example above.




Introduction to images


<img src="" alt="" title="" height="" width="">

alt is extremely important: is it decorative, functional or informational image?

Actually, you don't need to define both width and height. You can just specify either height or width 



anchor hyperlink
<a href="" target="_self"></a>
<a href="" target="_blank"></a>
<a href="" target="_parent"></a>
<a href="" target="_top"></a>


<a href="https://en.wikipedia.org/wiki/Media_queries?output=print" media="print and (resolution:250dpi)">Print wiki page about media queries</a>


<a href="/assets/hello.txt" download>
<a href="/assets/hello.txt" download="new-name-for-text-file"