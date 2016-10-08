---
layout: post
title:  "What is WAI-ARIA?"
date:   2016-09-21 09:11:03
categories: article
comments: true
permalink: /article/intro-wai-aria/
---

## Introduction

WAI-ARIA is a shorthand for (Web Accessibility Initiative – Accessible Rich Internet Applications). 

> **WAI-ARIA** is technical specification published by the W3C that specifies how to increase the accessibility of web pages, in particular, dynamic content and user interface components developed with HTML, JavaScript, Ajax and related technologies. - [Wikipedia](https://en.wikipedia.org/wiki/WAI-ARIA)

ARIA will help us to define a way to make our websites and web applications more accessible. By using HTML attributes that will define the **role**, **states** and **properties** of specific HTML elements. It will bridge areas where accessibility can't be perfect with semantic HTML.

## Accessibility Tree

Each web page has an accessibility tree that got parsed by the browser or screen readers. That tree contains different elements from the pages with their nested elements.  

> the accessibility tree is a subset of the DOM tree. It includes the user interface objects of the user agent and the objects of the document. Accessible objects are created in the accessibility tree for every DOM element that should be exposed to an assistive technology, either because it may fire an accessibility event or because it has a property, relationship or feature which needs to be exposed. - [The Paciello Group](https://www.paciellogroup.com/blog/2015/01/the-browser-accessibility-tree/)

{% include picture.html
		svgPath="../../assets/images/articles/aria-intro/aria.svg"
        pngPath="../../assets/images/articles/aria-intro/aria.png"
		title = "Comparing the accessibility before and after using ARIA"
%}

The above figure shows us how ARIA can help us in bridging the gaps in our pages. By using ARIA attributes, we will be able to do that.

## ARIA Roles

We can use roles for:

- Widgets: menu, accordion, modal.

- Elements: header, main, aside, footer.

{% highlight html linenos %}
<ul role="menu">
  <!--  -->
</ul>
{% endhighlight %}

{% highlight html linenos %}
<ul role="tablist">
  <!--  -->
</ul>
{% endhighlight %}

[Checkout the spec for more roles](https://www.w3.org/TR/wai-aria/roles#widget_roles)

### ARIA States

Suppose you have a button that toggle a mobile menu, to make it clearer for screen readers, you should use the ARIA state `aria-expanded` which is a boolean attribute.

{% highlight html linenos %}
<button aria-expanded="false">
  Open menu
</button>
{% endhighlight %}

### ARIA Properties

With properties, we can provide more info about a specific element or a relationship between element and the other. 

{% highlight html linenos %}
<nav role="navigation" aria-label="Main menu">
  <!-- content -->
</nav>
{% endhighlight %}

In the above example, screen readers will read the additional text we added "Main menu", this will make it easier for the user. 

Another example is on using `aria-describedby` attribute. Lets suppose that we want to make a custom region in our page.

{% highlight html linenos %}
<section role="region" aria-labelledby="title">
  <h2 id="title">Latest Articles</h2>
  <p>Your content goes there..</p>
</section>
{% endhighlight %}

We are saying: this section is labeled by the element that has an ID of **"title"**. With that in place, we created a relationship between the `<section>` and `<h2>` elements. Now, screen readers will read that section as a landmark.

[Read this article for more info on regions](/article/intro-html5-sectioning-elements/)

