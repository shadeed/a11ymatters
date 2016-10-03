---
layout: pattern
title:  "Search"
desc: "Different patterns on implementing an accessible search component"
date:   2016-09-8 09:11:03
updated: 2016-09-8 09:11:03
categories: pattern
comments: true
permalink: /pattern/accessible-search/
thumb: "assets/images/patterns/search/thumb.jpg"
thumbWebp: "assets/images/patterns/search/thumb.webp"

outline:
   - title: Things to take in consideration
     link: things-to-take-in-consideration
     subtitles:
      - subtitle: Including a label element
        sublink: including-a-label-element
      - subtitle: Include a meaningful description in the label
        sublink: include-a-meaningful-description-in-the-label
      - subtitle: Handling form errors
        sublink: handling-form-errors
      - subtitle: Always include a clear focus style
        sublink: always-include-a-clear-focus-style
      - subtitle: If the input is required, indicate that
        sublink: if-the-input-is-required-indicate-that
   - title: Building the search component
     link: building-the-search-component
   - title: Issues we have
     link: issues-we-have
     subtitles:
      - subtitle: Reading the error message twice
        sublink: reading-the-error-message-twice
   - title: Final demo
     link: final-demo
summary: "When building a search component, it's important to take accessibility in mind from the beginning. We will explore some bad things to avoid and then show the final pattern with testing results and videos."
stories:
  - I should be able search by using the keyboard.
  - I should be informed that the field is required.
  - I want to know when the field status is invalid.
  - I should be able to search by clicking Enter key on the input.
  - I need to know what is the purpose of this input.
ingredients:
  - form
  - label
  - input
  - aria-required
  - aria-invalid
  - alert
---

## Article Todo

- [ ] role="search"

- [x] Things to avoid

- [x] Building the component

- [ ] Explain about how the error is added

- [x] Add videos for how it should work

- [ ] Find a way to show the testing results with a better design

- [x] Embed the real demo

- [x] Summary


## Things to take in consideration

### 1- Including a `<label>` element.

{% highlight html linenos %}
<form>
  <input id="search" type="text" placeholder="Search about recipes">
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

When we don't have a `<label>` element, AT (Assistive Technology) users won't get the meaning of this input, even if there is a `placeholder` attribute.

Testing results from different screen readers:

- **VoiceOver on Safari**: edit text

- **JAWS 17 on IE11**: edit

- **NVDA 2016 on Firefox Win**: edit has auto complete, blank

- **iOS VoiceOver**: text field, double tab to edit

What's the purpose of this input? The user will have no clue that this is a search input. This is very bad and confusing. As a result, your user will be frustrated and not happy with that. 

**Solution**

{% highlight html linenos %}
<form>
  <label class="search-label" for="search">Search about recipes:</label>
  <input id="search" type="text" placeholder="Search about recipes">
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

### 2- Include a meaningful description in the `label`

{% include figure.html
		img="../../assets/images/patterns/search/search-no-label.jpg"
		title = ""
%}

How could that happen? When you add a search icon as an `<img>`, `<svg>` or `background-image`, it's important to add a text saying _Search_ for example, and hide it with CSS.

In the below example, we have a search icon as a replacement for the text _Search_ inside a `<label>`. 

{% highlight html linenos %}
<form>
  <label class="search-label" for="search">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 40 40" >
        <!-- path data -->
      </svg>
  </label>
  <input id="search" type="text" placeholder="Search about recipes">
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

Let's see what screen readers will announce.

- **VoiceOver on Safari**: edit text

- **JAWS 17 on IE11**: edit

- **NVDA 2016 on Firefox Win**: edit has auto complete, blank

- **iOS VoiceOver**: text field, double tab to edit

It's the same as not including a `<label>` element. To solve this, we can try the following:

#### 1- Add a title for the SVG element that will be associated with `aria-labelledby` attribute.

{% highlight html linenos %}
<form>
  <label class="search-label" for="search" aria-labelledby="searchTitle">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 451 451" >
        <title id="searchTitle">Search</title>
        <!-- path data -->
      </svg>
  </label>
  <input id="search" type="text" placeholder="Search about recipes">
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

#### 2- Add text _Search_ inside the `<label>` and hide it with CSS `text-indent`.

{% highlight html linenos %}
<form>
  <label class="search-label" for="search">
      Search
  </label>
  <input id="search" type="text" placeholder="Search about recipes">
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

{% highlight css linenos %}
.search-label {
  width: 40px;
  height: 40px;
  background-image: url('search.png');
  text-indent: -9999px;
}
{% endhighlight %}

#### 3- Hide the text off screen

{% highlight html linenos %}
<form>
  <label class="search-label" for="search">
      <span>Search</span>
  </label>
  <input id="search" type="text" placeholder="Search about recipes">
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

{% highlight css linenos %}
.search-label {
  width: 40px;
  height: 40px;
  background-image: url('search.png');
}

.search-label span {
  position: absolute;
  clip: rect(1px, 1px, 1px, 1px);
  padding: 0;
  border: 0;
  height: 1px;
  width: 1px;
  overflow: hidden;
}
{% endhighlight %}

### 3- Handling form errors

It's important to validate your forms for accessibility. In case the user didn't enter anything in the field and pressed on button, it should inform AT that this input is not valid and required.

Adding a `<p>` element with text like "Your input is not valid" in a red color, is not enough for AT users because it won't be accessible to them.

{% highlight html linenos %}
<form>
  <p class="form-error">The input is not valid. It must not be empty!</p>
  <label class="search-label" for="search">Search</label>
  <input id="search" type="text" placeholder="Search about recipes">
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

{% highlight css %}
.form-error {
  color: red;
}
{% endhighlight %}

**Normal person**

{% include figure.html
		img="../../assets/images/patterns/search/search-error-normal.jpg"
		title = ""
%}

**Blind person**

{% include figure.html
		img="../../assets/images/patterns/search/search-error-blind.jpg"
		title = ""
%}

Screen readers? Simply the user will get nothing. The error message won't be seen from the first place because its added as a regular `<p>` without taking in consideration ARIA and Role attributes.

### 4- Always include a clear focus style

When the user focuses on the input, we should indicate that in a very clear way. That could be done by:

- Adding a thick border with a dark color.

- Adding a glow or a blurred shadow.

- Changing the background color a bit to be darker.

In general, we shouldn't depend only on the color to indicate that an input is focused. There are people with color blindness (partial or full) who won't be able to recognize the color on focus. 

Give them other indicators that doesn't depend on colors, like a thick border or a shadow. Whatever works for your case.

In the below example, we will see how a red border will be seen from the view of a color blindness user. 

**A Person with normal color vision:**

{% include figure.html
		img="../../assets/images/patterns/search/form-normal.jpg"
		title = "How the border will look for normal people"
%}

**A Person with [Deuteranopia](http://www.color-blindness.com/deuteranopia-red-green-color-blindness/) color blindness:**

{% include figure.html
		img="../../assets/images/patterns/search/form-color-blind.jpg"
		title = "How the border will look for color blindness people"
%}

Noticed how the border color is almost dark green? This won't give an idea that this input is not valid. You should add other indicators like a message or an "X" icon for example.

### 5- If the input is required, indicate that

It's not enough to add `required` attribute to the input, AT users won't get that the input is required. 

{% highlight html linenos %}
<form>
  <label class="search-label" for="search"></label>
  <input id="search" type="text" placeholder="Search about recipes" required>
  <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

Let's explore how the right way to build out component.

## Building the search component

Now we will go through the steps on building an accessible search form. Below is the end result we want to achieve: 

**HTML**

{% highlight html linenos %}
<form>
    <label class="search-label" for="search">Search about a recipe
      <p id="error" role="alert"></p>
    </label>
    <input id="search" class="search-input" type="text" aria-describedby="error">
    <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

1. We have a `<label>` with a proper and easy to understand description. Then, inside the `<label>` we have a `<p>` element with `role=alert` attribute. This will help screen readers to get the error text in case the input was not valid.

2. Our input, with `aria-describedby="error"`. That's mean when the user focuses on the input and it's not valid, the validation error will be announced based on the element with `id=error`.

3. Search button.

[Learn more about how to use ARIA and Role](#)

{% include figure.html
		img="../../assets/images/patterns/search/final-result.jpg"
		title = "Search pattern final result"
%}

**Focus style**

{% include figure.html
		img="../../assets/images/patterns/search/search-focus.jpg"
		title = "Search pattern focus style"
%}

**Form error**

{% include figure.html
		img="../../assets/images/patterns/search/search-error.jpg"
		title = "Search pattern form error"
%}

Enough visual, let's see how screen readers will understand our simple search form!

### Input Focus

- **VoiceOver on Safari**: search about a recipe, edit text

- **JAWS 17 on IE11**: search about a recipe, edit

- **NVDA 2016 on Firefox Win**: search about a recipe, edit

- **iOS VoiceOver**: 


### Form Error (Search when the input is empty)

- **VoiceOver on Safari**: You need to enter a search term before pressing submit, You need to enter a search term before pressing submit

- **JAWS 17 on IE11**: Search about a recipe, You need to enter a search term before pressing submit, edit invalid entry, You need to enter a search term before pressing submit

- **NVDA 2016 on Firefox Win**: alert, You need to enter a search term before pressing submit

- **iOS VoiceOver**:

## Issue(s) we have

### Reading the error message twice

JAWS and Safari read the error message twice, which is not what we want. Mainly the issue was because we are using `aria-describedby` to let screen readers get the error, in addition to adding the error inside the `<label>` element. This will result in reading the error message twice!

### Testing with VoiceOver on Safari

{% include youtube.html id="rE5a_YRKmi8" %}

**HTML** after removing `aria-describedby`:

{% highlight html linenos %}
<form>
    <label class="search-label" for="search">Search about a recipe
      <p id="error" role="alert"></p>
    </label>
    <input id="search" class="search-input" type="text">
    <input class="button" type="button" value="Search">
</form>
{% endhighlight %}

### Testing with VoiceOver on Safari after removing `aria-describedby`

{% include youtube.html id="M4CF1-4zTrc" %}

So we no longer need `aria-describedby`, we have an `alert` that will do the job. 

## Final Demo

<iframe height='364' scrolling='no' src='//codepen.io/shadeed/embed/e265a0f975047a06d1a45471813c653f/?height=364&theme-id=23655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='http://codepen.io/shadeed/pen/e265a0f975047a06d1a45471813c653f/'>a11ymatters - Search</a> by Ahmad Shadeed (<a href='http://codepen.io/shadeed'>@shadeed</a>) on <a href='http://codepen.io'>CodePen</a>.
</iframe>