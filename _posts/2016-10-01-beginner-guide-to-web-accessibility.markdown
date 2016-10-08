---
layout: post
title:  "Beginners Guide to Web Accessibility"
date:   2016-07-08 09:11:03
categories: article
comments: true
permalink: /article/beginners-guide-to-web-a11y/
---

### Outline

- Add the article of Relative CSS Units on CSS Tricks, introduce the example.


### What is Web Accessibility? 

> refers to the inclusive practice of removing barriers that prevent interaction with, or access to websites, by people with disabilities. **When sites are correctly designed, developed and edited, all users have equal access to information and functionality.** - Wikipedia
 
So basically your website should work for all users and everyone should have access to the content. It's important to keep in mind that accessibility is **not meant** only to people with disabilities, we all can benefit from a website built with accessibility taken into consideration. 

### Issues we might face while browsing the web

- **Browsing the web without a mouse.** You will need to browse a website with your keyboard until you get a new mouse. During that time, if a website is not built well, you won't be able to accomplish your tasks as usual and so this will result in a bad experience.

- **Decrease the laptop brightness.** Using light colors for text will appear quickly when the screen brightness is decreased. Always, be sure that the color contrast meets the 

- Trying to read small text without your glasses.

- Slow Internet connection.

- Browsing the web while on of your hands is broken.

### What are the basics steps for making an accessible website?

- Write semantic HTML markup and use the appropriate elements depending on the content you have.

- Enhance with CSS to establish a look and feel for the website. 

- Use JavaScript as an enhancement for the functionality. 

HTML is the core foundation of the web. When your website HTML is written in a semantic way, the other things should be easier. 

### Assistive Technology Devices

Refers to physical devices and computer applications that increase and improve functional capabilities for people with disabilities. Users can browser your website from many different devices: mobile phones, smart TVs, computers, laptops, tablets.. etc

Most operating systems comes with a built-in screen reader application that help users doing their tasks easily. 

[Learn](https://www.paciellogroup.com/blog/2015/01/basic-screen-reader-commands-for-accessibility-testing/) how to test for various screen readers on different platforms.

{% include assistive-table.html 
   col1="Operating System" 
   col2="Screen Reader" 
   caption="Each operating system and its screen reader"
   fileName="assistive"
%}

### Things to follow

#### 1. HTML Markup

- Adding `lang` attribute to the `<html>` element to let the screen reader announce the document language.

- `<h1>` heading must be added to each page. It could be added to the logo, or a normal title in an article page for example. Then, in your document use headings from `<h2>` to `<h6>`.

- Use the headings for sectioning the page content only. Don't use them to make a text look bold or big in size. You have other elements to do that like `<strong>` tag for example or simply use CSS.

- When using images, you have to decide if it's for decoration purposes only or if it's very important to the context. If the purpose is purely decorative, use CSS `background-image` property to show it and otherwise use the `<img>` element.

- When the `<img>` fails to load, there should be a meaningful alternative text about it, if it's not important then leave the `alt` attribute empty. **Important**: removing the `alt` attribute will make the screen reader read the image file name, as in our next example it will read it like "foo-bar-01.jpg", and this is bad. 

- In case you don't want the screen readers to read the `alt` content, just leave it empty.

{% highlight html %}
<img src="foo-bar-01.jpg" alt="">
{% endhighlight %}

- Implement a good document outline. Use the HTML headings (h1, h2.. h6) to indicate the importance of each section/title in the web page. Usually, the website title/logo should be inside an `<h1>` element and the other elements could take from `<h2>` and below. This is called sectioning content.

- When using a semantic markup, you will save a lot of time and take the accessibility for free. For example, by adding `<select>` element you can navigate between the options by using the up and down arrow keys. In comparison, coding a custom select menu by using `<ul>` or regular `<div>s` won't work with the keyboard. So you will need to invest more time and effort to make this custom designed menu accessible.

- To check if your HTML markup is good or not? Try browsing the page without CSS. If you found that some titles that used to be bold and big with CSS, then you are probably using the wrong HTML for that. We can style a `<div>` element just like `<h1>` but what about no-css case? This `<div>` will appear as a regular paragraph.

- In order to navigate between the different elements in your page, for example navigation links and a search input, in the HTML the navigation markup should be added before the search. Otherwise, when using `tab` key the focus will be on the search element first.

- HTML provides us with an awesome page landmarks to use like: `<header>`, `<footer>`, `<main>`, `<aside>`, `<section>`, `<nav>`. Use them only once in a page except for the `<nav>` element, you can use it in the header and footer navigation but you should provide an additional attribute to help screen readers announce it. 

**Header**

{% highlight html %}
<header>
    <nav aria-label="Main Navigation">
        <!-- nav markup here -->
    </nav>
</header>
{% endhighlight %}

**Footer**

{% highlight html %}
<footer>
    <nav aria-label="Footer Navigation">
        <!-- nav markup here -->
    </nav>
</footer>
{% endhighlight %}

You can read more about ARIA in [this](/article/intro-wai-aria/) article. 

- Always add `role="contentinfo"` to the `<footer>` element. That way, screen readers will announce this area as an additional content and information about the page.

- Users of screen readers always seek out for ways to quickly skip to the main content. To help them achieve that, we can provide a skip link that will only work with keyboard and screen readers. The idea is simply to hide it off screen with CSS and when we hit `tab` from the keyboard, it will be activated.

- When working with `<forms>`, you can use the handy `<fieldset>` element to group a related selectors like checkboxes or radio buttons.

- Assign a `<label>` to each input element. We can apply that by adding an id to the input and then adding this id to `for` attribute of the label.

Now when the user click on the label, it will focus the input element. 

{% highlight html %}
<label for="email">Your Email:</label>
<input type="email" id="email">
{% endhighlight %}


#### 2. Style and Presentation

- Embrace the `outline` property default focus effect. If you don't like it then that's fine but be sure to add your custom style. One of the biggest issues that affect the websites accessibility is resetting the value to 0. When trying to navigate the page with your keyboard, you won't see any the current focused element and so you will get very confused. Be careful, please.

- In links hover and active states, do not depend only on color/background changes. Instead, add more indicators that doesn't depend on the color. For example: underline, bolder text, an outline.

- Use relative CSS units to make it [possible](https://css-tricks.com/building-resizeable-components-relative-css-units/) to [enlarge](https://zellwk.com/blog/media-query-units) the elements and fonts for users who prefer to zoom-in or change their default browser font size.

### Basic testing for accessibility

- Through away your mouse and and start browsing a website you built. Can you use it just like when you use the mouse? Are all the links and buttons focusable? 

- Use a [screen reader](https://www.paciellogroup.com/blog/2015/01/basic-screen-reader-commands-for-accessibility-testing/) and turn off your computer screen. Start browsing with the keyboard and see if it's easy to navigate and get what you want.

- Add `filter: grayscale()` to the root element `<html>` of your page. Try to read the content, did you find that some text is hard to read? Then probably you will need to [fix](http://webaim.org/resources/contrastchecker/) some contrast issues. 


