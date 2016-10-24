---
layout: pattern
title:  "Pagination"
desc: "Pagination"
date:   2016-10-20 05:11:03
updated: 2016-10-24 05:11:03
categories: pattern
comments: true
permalink: /pattern/pagination/
thumb: "assets/images/patterns/pagination/thumb.jpg"
thumbWebp: "assets/images/patterns/pagination/thumb.webp"
outline:
   - title: Things to take in consideration
     link: things-to-take-in-consideration
     subtitles:
      - subtitle: Wrap the pagination links in a nav element
        sublink: wrap-the-pagination-links-in-a-nav-element
      - subtitle: Labeling the navigation links
        sublink: labeling-the-navigation-links
      - subtitle: Indicate which element is currently active
        sublink: indicate-which-element-is-currently-active
   - title: Using JavaScript to dynamically add the aria-label
     link: using-javascript-to-dynamically-add-the-aria-label
   - title: Final Demo
     link: final-demo

summary: "When there is a lot of content to display, using pagination will help us to add navigation links to reveal more content on the page."
stories:
  - I should be able to navigate by keyboard.
  - I should be able to know that there is a pagination navigation when scanning the page with a screen reader.
  - Each navigation item should be read as "Goto Page 1".
  - I need to know which element is currently active.
  - I need to navigation with Next and Previous links.
ingredients:
  - aria-label
  - aria-current
  - role=navigation
  - nav
  - links
---

## Things to take in consideration

### 1- Wrap the pagination links in a `<nav>` element

In order to let AT users recognize that there is a pagination, we should wrap the links in a `<nav>` element.

{% highlight html %}
<nav>
    <ul>
        <!-- pagination links -->
    </ul>
</nav>
{% endhighlight %}

Also, we should add `role=navigation` and `aria-label` to make it clearer to AT users that this navigation [landmark](/article/intro-html5-sectioning-elements/) is intended for the pagination.

{% highlight html %}
<nav role="navigation" aria-label="Pagination Navigation">
    <ul>
        <!-- pagination links -->
    </ul>
</nav>
{% endhighlight %}

### 2- Labeling the navigation links

{% highlight html %}
<nav role="navigation" aria-label="Pagination Navigation">
    <ul>
        <li><a href="/page-1">1</a></li>
        <li><a href="/page-2">2</a></li>
        <li><a href="/page-3">3</a></li>
        <li><a href="/page-4">4</a></li>
        <li><a href="/page-5">5</a></li>
    </ul>
</nav>
{% endhighlight %}

For sighted users, it's clear that the numbers will help him navigating different pages. But for an AT user, it's completely different. We need a better way to make it clear for him.

See the below video for a test with VoiceOver:

{% include youtube.html id="Y858zZzihKI" %}

Imagine that your screen is not working for some reason, you need to navigate between different pages. When you hear `Link, 1` for a link with the number 1, do you think that you will get it? No! It's not clear.

{% highlight html %}
<nav role="navigation" aria-label="Pagination Navigation">
    <ul>
        <li><a href="/page-1" aria-label="Goto Page 1">1</a></li>
        <li><a href="/page-2" aria-label="Goto Page 2">2</a></li>
        <li><a href="/page-3" aria-label="Goto Page 3">3</a></li>
        <li><a href="/page-4" aria-label="Goto Page 4">4</a></li>
        <li><a href="/page-5" aria-label="Goto Page 5">5</a></li>
    </ul>
</nav>
{% endhighlight %}

By using `aria-label`, we can add a label to each link, so instead of hearing the screen reader saying `Link, 1` it will be `Link, Goto Page 1`. See the below video:

{% include youtube.html id="muTF9AaxUXw" %}

To make it more dynamic, we will use JavaScript to loop through all the links and add `aria-label` with the corresponding value of "Goto Page X".

### 3- Indicate which element is currently active

To indicate which element is active, we need to tweak the value of `aria-label` by something like `Page 3, Current page`. Also, we will use `aria-selected=true` for that.

**Update**: Using `aria-selected` is wrong in our case, because it should be used only with a `role` attribute. Instead, we will use `aria-current`. Thanks to David Storey and Stefan Judis for commenting about this. ❤️

{% highlight html %}
<nav role="navigation" aria-label="Pagination Navigation">
    <ul>
        <!-- other pagination links -->
        <li>
          <a href="/page-3" aria-label="Current Page, Page 3" aria-current="true">3</a>
        </li>
        <!-- other pagination links -->
    </ul>
</nav>
{% endhighlight %}

## Using JavaScript to dynamically add the `aria-label`

{% highlight javascript linenos %}
var pagItems = document.querySelectorAll('.pagination__item');

for (var i = 0; i < pagItems.length; i++) {
  var counter = i + 1;
  var string = "Page " + counter;

  if (pagItems[i].getAttribute('aria-current')) {
    string = "Page " + counter + ", Current Page";
  }

  pagItems[i].setAttribute('aria-label', string);
}
{% endhighlight %}

**Line 1**: Select all the pagination links and add them to an array.

**Line 2**: Loop through each item.

**Line 7**: Check if the item has an attribute of `aria-current`, if yes then we need to tweak the `aria-label` value.

**Line 11**: Add the attribute `aria-label` with a custom name for each item.

## Final Demo

<p data-height="300" data-theme-id="23655" data-slug-hash="e8711b7460b4d050a6f4f804080c0b05" data-default-tab="css,result" data-user="shadeed" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/shadeed/pen/e8711b7460b4d050a6f4f804080c0b05/">a11ymatters - Pagination</a> by Ahmad Shadeed (<a href="http://codepen.io/shadeed">@shadeed</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
