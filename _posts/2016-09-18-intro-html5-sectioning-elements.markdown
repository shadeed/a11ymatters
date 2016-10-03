---
layout: post
title:  "Introduction to HTML5 Elements"
date:   2016-09-18 09:11:03
categories: article
comments: true
permalink: /article/intro-html5-sectioning-elements/
---

## Todo

- explain about aria-label

- using lynx browser

- add resources for each one

- provide demos specially for the region

## Introduction

HTML5 provide us with a lot of elements that could be used to lay out pages structure. 5 years ago, the support was not perfect and so they used [HTML5shiv](https://github.com/aFarkas/html5shiv) in order to fallback for non supporting browsers. 

In 2016, the [support](http://caniuse.com/#feat=html5semantic) is pretty good for these elements, which give us a set of handy tools to build better layouts.

## HTML5 Sectioning Elements

### The `<main>` element

From its name, `<main>` is an important element in a web page which contain the main and important content. It should used only one time per page and couldn't be nested. With that element in place, screen reader users can scan the page and navigate to the important content easily. 

In the below example, we have a web page with a `<main>` element:

{% highlight html linenos %}
<header>
    <!-- page head -->
</header>
<main>
   <p>
     <!-- unique content -->
   </p>
</main>
<footer>
   <!-- page foot -->
</footer>
{% endhighlight %}

#### Takeaways

- `<main>` element should only be used one time per page. By the way, the HTML standard spec says that they removed the restriction about using multiple `<main>` elements.

- The content inside `<main>` should be unique.

- We should add `role=main` so we can guarantee better support for screen readers. 

- There should not be repeated content inside the `<main>`, logo, navigation, page title, social links.. etc

- `<main>` must not be a descendant of an `<article>`, `<aside>`, `<footer>`, `<header>`, or `<nav>` element.

### The `<nav>` element

A section of a page that contains navigation elements which link to the parts within the page or other pages of the website. In most cases, we should only use the `<nav>` element for major links that lead to important pages in the website. 

{% highlight html linenos %}
<header>
  <h1>a11ymatters</h1>
  <nav>
    <ul>
      <li><a href="/articles">Articles</a></li>
      <li><a href="/projects">Projects</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
  </nav>
</header>
<main>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. 
  Quaerat perferendis doloremque cupiditate...</p>
</main>
<footer>
  <ul>
    <li><a href="/articles">Articles</a></li>
    <li><a href="/projects">Projects</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</footer>
{% endhighlight %}

In the above example, we are using `<nav>` to wrap the most important links on the page. But in the footer, we have the same links but without the `<nav>` element; it's recommended to not repeat the same `<nav>` element with the same links inside. 

Another example:

{% highlight html linenos %}
<nav>
  <h2>Navigation</h2>
  <p>Go to <a href="/articles">Articles</a></p>
  <p>And also, you can check out my <a href="/works">portfolio</a></p>
</nav>
{% endhighlight %}

In the above example, it shows that we can add links to a `<nav>` element without listing them with `<ul>` list. 

Below is an example on using multiple `<nav>`s for primary and secondary navigation:

{% highlight html linenos %}
<header>
  <h1>a11ymatters</h1>
  <!-- primary navigation -->
  <nav role="navigation">
    <ul>
      <li><a href="/articles">Articles</a></li>
      <li><a href="/projects">Projects</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
  </nav>
</header>
<main>
  <!-- secondary navigation -->
  <nav role="navigation">
    <ul>
      <li><a href="projects/web/">Web</a></li>
      <li><a href="projects/graphic/">Graphic</a></li>
      <li><a href="projects/dev/">Development</a></li>
    </ul>
  </nav>
</main>
<footer>
  <!-- footer links -->
</footer>
{% endhighlight %}

#### Takeaways

- `<nav>` is used to wrap major links in the page.

- In case you have a list of links, then use `<ul>` with `<nav>`.

- It's unnecessary to use `<nav>` in `<footer>`, add the links in a `<ul>` and that's enough.

- We can use multiple `<nav>` elements in a page, for example: primary and secondary navigation.

- Add `role=navigation` to ensure a better support.

### The `<header>` element

Represents a group of introductory content for its nearest ancestor sectioning content (`<article>`, `<nav>`, `<aside>`, `<section>`) or sectioning root element. If a header element is used for the whole page, then it should include the page title as an `<h1>` for example. 

In case the sectioning content or sectioning root is the `<body>` element, then the header applies to the whole page. See the below example:

{% highlight html linenos %}
<body>
  <header role="banner">
    <h1>a11ymatters</h1>
    <nav>
      <!-- nav elements -->
    </nav>
  </header>
  <main>
    <!-- main content -->
  </main>
  <footer>
    <!-- nav elements -->
  </footer>
</body>
{% endhighlight %}

Also, you can use `<header>` for defining the header of an `<article>` element. See the below example:

{% highlight html linenos %}
<main>
  <article>
    <header>
      <h2>Article title</h2>
      <time>Tue Sep 20</time>
    </header>
    <div>
      <!-- article content -->
    </div>
  </article>
</main>
{% endhighlight %}

#### Takeaways

- We can include multiple `<header>`s in the page.

- It's better to add `role=banner` to ensure better support for screen readers.

- In case the `<header>` represents the whole page, then it should include a title. 

- It could be used as a child of `<article>`, `<nav>`, `<aside>` and `<section>` elements.

### The `<footer>` element

Represents a footer for its nearest ancestor sectioning content (`<article>`, `<nav>`, `<aside>`, `<section>`) or sectioning root element. It typically contains information about the author of a section, legal info, copyright and links to related pages or documents.

Also, for screen reader users we should add `role=contentinfo` for better support. 

An example with a footer at the end of the document:

{% highlight html linenos %}
<body>
  <header role="banner">
    <!-- header content -->
  </header>
  <main>
    <!-- main content -->
  </main>
  <footer>
    <ul>
        <li><a href="/content">Contact</a></li>
        <li><a href="/works">Works</a></li>
        <li><a href="/faq">FAQ</a></li>
    </ul>
    <p>Copyright 2016</p>
  </footer>
</body>
{% endhighlight %}

Another example on using the `<footer>` is for the end of an `<article>` element.

{% highlight html linenos %}
<main>
  <article>
    <header>
      <h2>Article title</h2>
      <time>Tue Sep 20</time>
    </header>
    <div>
      <!-- article content -->
    </div>
    <footer>
        Published by John Smith
    </footer>
  </article>

  <article>
    <header>
      <h2>Article title</h2>
      <time>Wed Sep 17</time>
    </header>
    <div>
      <!-- article content -->
    </div>
    <footer>
        Published by Steve Smith
    </footer>
  </article>
</main>
{% endhighlight %}


#### Takeaways

- We can include multiple `<footer>`s in the page.

- Add `role=contentinfo` to ensure better support for screen readers.

- It could be used as a child of `<article>`, `<nav>`, `<aside>` and `<section>` elements.

### The `<aside>` element

This element represents complementary content that is not important to the user but related or connected to it. For example: author bio, related articles, advertisements. In some cases, the `<aside>` could be added as a sidebar. 

Here is a basic example on the use of `<aside>`

{% highlight html linenos %}
<article>
  <p>This is the main paragraph of this article.. etc</p>
  
  <aside>
    <p>Do you know that this paragraph is written by John Smith?</p>
  </aside>
</article>
{% endhighlight %}

Notice that the content is not that important so we placed it in the `<aside>`. In the design, we can position this on the side with a smaller font or something that indicates this is a secondary content.

An example of using `<aside>` for the whole page:

{% highlight html linenos %}
<main>
  <article>
    <!-- Article content -->
</article>
</main>
<aside>
  <!-- Author bio -->
  <!-- Related articles -->
  <!-- Advertisements -->
</aside>
{% endhighlight %}

In that case, it represents the sidebar which contains advertisements, related articles and author bio.

#### Takeaways

- Add `role=complementary` to ensure better support for screen readers. 

- `aside` element is used to wrap secondary content that is connected or related to the main one. 


### The `<section>` element

Represents a generic section of a page or document which typically contains a heading (h1-h6) and a content like paragraphs or images. It's not recommended to use `<section>` as a container, you can use a `<div>` for that purpose instead of it. 

{% highlight html linenos %}
<section>
  <h2>Section title</h2>
  <p>Your content goes there..</p>
  
  <ul>
    <li>bla</li>
    <li>bla</li>
  </ul>
</section>
{% endhighlight %}

For screen readers users, if you want to let them know about an important section title, then you should do the following:

- Add `role=region` to the `<section>` element.

- Define an ID for the `<section>`'s heading.

- Add `aria-labelledby` attribute to the `<section>` with the value of its heading ID.

See the below example:

{% highlight html linenos %}
<section role="region" aria-labelledby="title">
  <h2 id="title">Latest Articles</h2>
  <p>Your content goes there..</p>
</section>
{% endhighlight %}

That way, screen reader users will be able to scan the page and know about that section titled "Latest Articles".

#### Takeaways 

- Don't use the `<section>` element as a container.

- If you want to let screen reader users know about a specific important section, you can use `role=region` associated with a title inside that `<section>`.

## ARIA Landmarks Roles

By using ARIA landmarks, we will define all regions of a page. By doing that, we will help screen reader users to know about all page landmarks when scanning it. 

{% highlight html linenos %}
<body>
  <header role="banner">header content</header>
  <main role="main">
    main content
  </main>
  
  <aside role="complementary">
    aside content
  </aside>
  <footer role="contentinfo">footer info</footer>
</body>
{% endhighlight %}

To test this on macOS VoiceOver:

1. CMD + F5

2. ALT + CTRL + U

3. Move with left/right arrows until you reach the landmarks list

Here is the testing result we get: 

**Landmarks:**

- banner

- main

- complementary

- contentinfo

## HTML5 elements with their ARIA roles

{% include table.html 
   col1="HTML5 Element" 
   col2="ARIA Role" 
   caption="HTML5 elements with their ARIA roles"
   fileName="ariaTable"
%}