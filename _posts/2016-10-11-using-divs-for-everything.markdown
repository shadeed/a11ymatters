---
layout: post
title:  "Don't Use DIVs for Everything"
date:   2016-10-11 08:11:03
categories: article
comments: true
permalink: /article/dont-use-divs-for-everything/
---

## Introduction

At the early months of my Front-End career, I was intrigued to the idea of using `<div>`s for almost everything. For example, instead of picking an `<h2>` for a post title, I would choose a `<div>` and make it look like a heading.

If I want to build an article component, I won't think about anything semantic. I just use `<div>`s because you know, it's way faster than picking semantic elements. The reason for that is  because I get used to [Emmet](http://emmet.io/) plugin, where I just type `.post-date` and then press `tab` to get a new `<div>`.

{% include figure.html
		img="../../assets/images/articles/divs-for-everything/emmet.gif"
		title = "An animated image shows how typing with Emmet plugin might make us lazy to write semantic HTMl."
%}

## How I did it in the past

{% highlight html %}
<div class="post">
    <div class="post-date">October 11, 2016</div>
    <div class="post-title">Here is the post title</div>
    <div class="post-author">By Ahmad Shadeed</div>
</div>
{% endhighlight %}

For a person that is not aware about web [accessibility](/article/beginners-guide-to-web-a11y/), this might look fine. The old me see that this markup is totally fine as well. If I look at this markup now, I will be like: OMG!! RIP HTML.

## The right way to build things

HTML provides with many elements to describe content in the best semantic way. Here is the best way to describe the above example:

{% highlight html %}
<article class="post">
    <time class="post-date">October 11, 2016</time>
    <h2 class="post-title">Here is the post title</h2>
    <p class="post-author">By Ahmad Shadeed</p>
</article>
{% endhighlight %}

## CSS is an enhancement

When I approached that bad way of writing HTML, I supposed that CSS is always there, while in reality it's an enhancement. When we compare both examples with `<div>`s **VS** semantic elements, we will notice something as in the following comparison image:

{% include figure.html
		img="../../assets/images/articles/divs-for-everything/compare.jpg"
		title = "A Comparison between using semantic elements and divs when CSS is off."
%}

Without CSS, the semantic HTML is looking clearer than the `<div>`s one in terms of font size, font weight and spacing. This is the default look that we get for free! Each browser has default styles applied for some HTML elements (User Agent Stylesheet).