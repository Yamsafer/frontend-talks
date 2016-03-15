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

#### HTML IMPORTS

#### CUSTOM ELEMENTS

### Polymer


