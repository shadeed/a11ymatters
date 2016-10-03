---
layout: pattern
title:  "Skip Navigation Link"
desc: "Skip Link"
date:   2016-09-14 09:11:03
updated: 2016-09-14 09:11:03
categories: pattern
comments: true
permalink: /pattern/skip-link/
thumb: "assets/images/patterns/skip/thumb.jpg"
thumbWebp: "assets/images/patterns/skip/thumb.webp"
outline:
   - title: What is a skip link?
     link: what-is-a-skip-link
   - title: Implementing a Skip Navigation Link
     link: implementing-a-skip-navigation-link
   - title: Final demo
     link: final-demo
summary: "Imagine that your mouse is not working and you want to use the keyboard to browse the web. With the skip link, you will be able to jump quickly to the content without tabbing through every single link in the website header."
stories:
  - I should be able to skip to content quickly.
  - I should know get that this is a button for skipping navigation.
ingredients:
  - link
  - positioning 
---

## What is a skip link?

When browsing a website with a keyboard, we need a quick way to skip a group of navigation items. Without that skip link, we will need to tab through the whole links to get out of the navigation area. 

In small websites, it might be ok to tab through 5 links. Lets explore the below example of [New York Times](www.nytimes.com) design.

{% include figure.html
		img="../../assets/images/patterns/skip/nytimes.jpg"
		title = ""
%}

How many tabs you need in order to reach the content area? In this design, we have almost 30 links to tab through. 

New York times did a great job in order to make it easy for users to:

- Skip to navigation

- Skip to content

{% include figure.html
		img="../../assets/images/patterns/skip/nytimes-tabbing.gif"
		title = ""
%}

## Implementing a Skip Navigation Link

The idea is to place a link before all all focusable elements in the source order. That way, we can style the skip link and hide it off screen with CSS.

Then, inside `href` attribute we should add a `#` followed by the ID value of the content block.

{% highlight html linenos %}
<body>
    <div class="wrapper">
        <a class="skip-link" href="#content">Skip to content</a>
        <header>
            <nav>
                <!-- Nav links -->
            </nav>
        </header>
        <div id="content">
            <!-- Content goes here -->
        </div>
    </div>
</body>
{% endhighlight %}

{% highlight css linenos %}
.skip-link {
    position: fixed;
    top: -200px;
}
{% endhighlight %}

{% include figure.html
		img="../../assets/images/patterns/skip/explain-hiding-link.jpg"
		title = ""
%}

Notice the dotted line that represents the browser window. Anything goes outside it is hidden off-screen. 

When pressing on `tab` key, the first element that will receive focus is the skip link element. Why? because it's the first one in the source order. 

In CSS, we will tell the browser in case the link is focused, show it at the top of the screen.

{% highlight css linenos %}
.skip-link:focus {
    top: 0; /* Now the link will appear */
}
{% endhighlight %}

{% include figure.html
		img="../../assets/images/patterns/skip/explain-hiding-link-focused.jpg"
		title = ""
%}

## Use `em` for the positioning

When setting the value of `top` property, be sure to test how it will look while changing the browser default font size. I didn't take care of this point while working on a11ymatters design, notice the top edge of the browser. The skip link is not completely hidden off screen.

{% include figure.html
		img="../../assets/images/patterns/skip/skip-browser-zoom.jpg"
		title = ""
%}

{% highlight css linenos %}
.c-skip {
    position: absolute;
    left: 50%;
    top: -2.5em; /* it's better to set this value in relative units, like em */
    padding: 0.75em;
}
{% endhighlight %}

For more info about that, read my [article](https://css-tricks.com/building-resizeable-components-relative-css-units/) on CSS Tricks about building resizeable components with relative CSS units.

## Final Demo

Click on the white area in the demo below and then start tabbing. Did you notice our skip link? 

<p data-height="600" data-theme-id="23655" data-slug-hash="64636e8ac6f3554f47455895d23a2b81" data-default-tab="result" data-user="shadeed" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/shadeed/pen/64636e8ac6f3554f47455895d23a2b81/">a11ymatters - Skip Navigation Link</a> by Ahmad Shadeed (<a href="http://codepen.io/shadeed">@shadeed</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>