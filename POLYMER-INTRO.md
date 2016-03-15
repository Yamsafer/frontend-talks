##Polymer Introduction

[TOC]

### Abundance of choice
It feels like every 6 months to a year there is some new framework we have to learn.

![Alt text](./js-frameworks-trends.png)

- Lots of frameworks,
- Notion of **components**,
- **they don’t work together**.

There i still hope for humanity
> A few years ago, engineers who work on the browsers got together to figure out, what are the best features of the frameworks and can we make them part of the browser. That way you don’t have to rewrite your code every 6 months.

![Alt text](./logo.jpg)

> In the past, a new tag would be invented, and then we had to wait for it to ship in every browser.

**Web Components are low-level primitives that let you define your own HTML Elements.**

### Web Components
#### Template
##### WHY
as the landscape of web architecture is changing, and as the MVC model is not anymore bound by server frameworks only, and with the rise of client-side javascript framworks that compiles and render views on the user-agent, and as it's a shame if we move forward doing client side templating using such syntax

```
<script type="text/template">
  <div>
    <h1>Web Components</h1>
    <img src="http://webcomponents.org/img/logo.svg">
  </div>
</script>
```
##### What
Web components brings us the template html tag
```
<template id="template">
  <style>
	.thumb{
		border : 1px solid red;
		padding : 5px;
	}
  </style>
  <div>
    <h1>Frontend Talks</h1>
    <img class="thumb" src="./logo.png">
  </div>
</template>
```
##### Usage
```
<script>
  var template = document.querySelector('#template');
  // deep clone
  var clone = document.importNode(template.content, true);
  var host = document.querySelector('#host');
  host.appendChild(clone);
</script>
```
##### Browser Support
![Alt text](./template-browser-support.png)

but  don't worry, polyfills are there for the save.

#### SHADOW DOM
##### What
##### What
##### USAGE
##### Browser Support

#### HTML IMPORTS
##### What
	HTML Imports are a way to include and reuse HTML documents in other HTML documents

##### WHY 
> Imports provide convention for **bundling HTML/CSS/JS** (even other HTML Imports) into a single deliverable. It's an intrinsic feature, but a powerful one. If you're creating a theme, library, or just want to **segment your app** into logical chunks, giving users a single URL is compelling. Heck, you could even **deliver** an entire app via an import. Think about that for a second.


##### USAGE
```
<head>
  <link rel="import" href="/path/to/imports/stuff.html">
</head>
```
##### Browser Support

#### CUSTOM ELEMENTS
##### What
A custom element is an element whose constructor and prototype are defined by a developer, instead of by the user agent. The developer-supplied constructor function is called the custom element constructor.

##### WHY
1. Provide a way for Web developers to build their own, fully-featured DOM elements.
Although it was long supported to create any element you want on the html page, this feature was not very functional, inform the4 parser on how to properly construct an element and to react to life cycle changes of an element.

2. Rationalize the platform.
HTML elements explain the functionality of existing Web platform features.
Rationalize all HTML, SVG and MathML, elements into one coherent system.
##### USAGE

Extending an existing element class (ex. native elements)
```
	 document.defineElement("x-foo", class XFoo extends HTMLElement {
        constructor() {
            super();
            this._initialData = "foo";
        }
    });

```
then use it in javascript

`var foo = document.createElement("x-foo");`

or in html

`<x-foo></x-foo>`

##### Browser Support
![Alt text](./custom-elements-browser-support.png)

### Polymer


