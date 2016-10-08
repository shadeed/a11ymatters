---
layout: pattern
title:  "Page Title"
desc: "Page Title"
date:   2016-09-02 09:11:03
updated: 2016-09-02 09:11:03
categories: pattern
comments: true
permalink: /pattern/page-title/
thumb: "assets/images/patterns/page-title/thumb.jpg"
thumbWebp: "assets/images/patterns/page-title/thumb.webp"
outline:
   - title: Things to take in consideration
     link: things-to-take-in-consideration
     subtitles:
      - subtitle: Always use an h1 for the page title
        sublink: always-use-an-h1-for-the-page-title
      - subtitle: Be sure to add an alt text for the img
        sublink: be-sure-to-add-an-alt-text-for-the-img
      - subtitle: Include a text
        sublink: include-a-text
      - subtitle: Add logo description when needed
        sublink: add-logo-description-when-needed
   - title: Final demo
     link: final-demo
summary: "A page title is the most important thing in a web page. Imagine a document without a title? We will explore different ways to use page titles under different circumstances"
stories:
  - I should be read the page title when CSS is not available.
  - I want to know the text content even if the title is an image
ingredients:
  - h1
  - link
  - aria-label
  - img 
---

## Things to take in consideration

### 1- Always use an `h1` for the page title

Image a word document without a title? 😱

It's not good to just through an anchor link `<a>` and then to depend on it as the page title. Screen readers won't get that easily. 

{% highlight html linenos %}
<header>
    <a class="logo" href="/">Knowledge Space</a>
</header>
{% endhighlight %}

### 2- Be sure to add an `alt` text for the `img`

In case you have the logo as an img (Most of the websites do that), then you must add meaning of the logo inside the `alt` attribute.

{% highlight html linenos %}
<header>
    <h1>
      <a class="logo" href="/">
        <img src="logo.svg" alt="Knowledge Space"/>
      </a>
    </h1>
</header>
{% endhighlight %}

Screen readers will get the text content in `alt` attribute. This is important and when it's not included, users won't get the meaning of this link.

Another option will be to leave the `alt` empty and then to add the logo meaning as a text inside the link.

{% highlight html linenos %}
<header>
    <h1>
      <a class="logo" href="/">
        <img src="logo.svg" alt=""/>
      </a>
      Knowledge Space
    </h1>
</header>
{% endhighlight %}

In case you want to hide the text, then you should hide it visually with CSS.

{% highlight css linenos %}
.logo {
  position: absolute;
  clip: rect(1px, 1px, 1px, 1px);
  padding: 0;
  border: 0;
  height: 1px;
  width: 1px;
  overflow: hidden;
}
{% endhighlight %}

### 3- Include a text

When the logo is added as a `background-image` in CSS, be sure to add it as a text.

{% highlight html linenos %}
<header>
    <h1>
      <a class="logo" href="/"></a>
    </h1>
</header>
{% endhighlight %}

{% highlight css linenos %}
.logo {
  background: url('logo.svg');
}
{% endhighlight %}

Implementing a page title in that way is not accessible. We should add the text and hide it with CSS `text-indent`.

{% highlight html linenos %}
<header>
    <h1>
      <a class="logo" href="/">Knowledge Space</a>
    </h1>
</header>
{% endhighlight %}

{% highlight css linenos %}
.logo {
  background: url('logo.svg');
  text-indent: -100%;
}
{% endhighlight %}

### 4- Add logo description when needed

In the below example, when a screen reader read "a11ymatters", it will be hard to understand the meaning of that. 

{% highlight html linenos %}
<header>
    <h1>
      <a class="c-page-title__link" href="/">
        a11ymatters
      </a>
    </h1>
</header>
{% endhighlight %}

A solution for this is be to add `aria-label` attribute with the correct meaning.

{% highlight html linenos %}
<header>
    <h1 aria-label="Accessibility Matters">
      <a class="c-page-title__link" href="/">
        a11ymatters
      </a>
    </h1>
</header>
{% endhighlight %}

Notice how Chrome canceled the content "a11ymatters" and replaced it with the title inside `aria-label`.

{% include figure.html
		img="../../assets/images/patterns/page-title/chrome-a11y.jpg"
		title = ""
%}

In the meantime, the accessibility inspection is not available by default in Chrome. Follow these [instructions](https://gist.github.com/marcysutton/0a42f815878c159517a55e6652e3b23a) to learn about that.