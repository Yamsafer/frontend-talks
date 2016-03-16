<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [Web Components](#web-components)
    - [Abundance of choice](#abundance-of-choice)
    - [Web Components Specs](#web-components-specs)
      - [Template](#template)
        - [What](#what)
- [Frontend Talks](#frontend-talks)
        - [WHY](#why)
        - [Usage](#usage)
        - [Browser Support](#browser-support)
      - [HTML IMPORTS](#html-imports)
        - [What](#what-1)
        - [WHY](#why-1)
        - [USAGE](#usage)
        - [Browser Support](#browser-support-1)
      - [Custom Elements](#custom-elements)
        - [What](#what-2)
        - [WHY](#why-2)
        - [Browser Support](#browser-support-2)
      - [SHADOW DOM](#shadow-dom)
        - [What](#what-3)
        - [Why](#why)
          - [Dom Pollution](#dom-pollution)
        - [USAGE](#usage-1)
        - [Browser Support](#browser-support-3)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Web Components

### Abundance of choice
It feels like every 6 months to a year there is some new framework we have to learn.

![Alt text](./_images/js-frameworks-trends.png)

- Lots of frameworks,
- Notion of **components**,
- **they don’t work together**.

There i still hope for humanity

 A few years ago, engineers who work on the browsers got together to figure out, what are the best features of the frameworks and can we make them part of the browser. That way you don’t have to rewrite your code every 6 months.

The result was:

### Web Components Specs

Web Components are low-level primistives that let you define your own HTML Elements.

In the past, a new tag would be invented, and then we had to wait for it to ship in every browser, now we can invent these tags, and share them.

![Alt text](./_images/logo.jpg)

There are four specs that make up web components

1. [Template](#template)
2. [Shadow Dom](#shadow-dom)
3. [HTML Imports](#html-imports)
4. [Custom elements](#custom-elements)

We will discuss each component in details later, 

But what about browser support for these new specifications now? 
> A lot of progress has been made since the introduction of the Web Components back in 2011. All major browsers have started implementation of the technologies needed to run web components natively. While browser vendors are still working on native implementations, libraries have been able to use a polyfill to make web components available to developers already.

 The webcomponent.js polyfills enable Web Components in (evergreen) browsers that lack native support.

`<script src="bower_components/webcomponentsjs/webcomponents.min.js" </script>`


#### Template
##### What
Templates allow you to declare fragments of markup which are parsed as HTML, go unused at page load, but can be instantiated later on at runtime.
```
<template id="template">
  <div>
    <h1>Frontend Talks</h1>
    <img class="thumb" src="./logo.png">
  </div>
</template>
```
##### WHY
As the landscape of web architecture is changing, and as the MVC model is not anymore bound by server frameworks only, and with the rise of client-side javascript framworks that compiles and render views on the user-agent, and as it's a shame if we move forward doing client side templating using such syntax

```
<script type="text/template">
  <div>
    <h1>Web Components</h1>
    <img src="http://webcomponents.org/img/logo.svg">
  </div>
</script>
```
##### Usage
```
<template id="template">
  <div>
    <h1>Frontend Talks</h1>
    <img class="thumb" src="./logo.png">
  </div>
</template>
<script>
  var template = document.querySelector('#template');
  // deep clone
  var clone = document.importNode(template.content, true);
  var host = document.querySelector('#host');
  host.appendChild(clone);
</script>
```
##### Browser Support
![Alt text](./_images/template-browser-support.png)

#### HTML IMPORTS
##### What
HTML Imports are a way to include and reuse HTML documents in other HTML documents

##### WHY 
 Imports provide convention for **bundling HTML/CSS/JS** (even other HTML Imports) into a single deliverable. It's an intrinsic feature, but a powerful one. If you're creating a theme, library, or just want to **segment your app** into logical chunks, giving users a single URL is compelling. Heck, you could even **deliver** an entire app via an import. Think about that for a second.


##### USAGE
```
<head>
  <link rel="import" href="/path/to/imports/stuff.html">
</head>
```

##### Browser Support
> add content

#### Custom Elements
##### What
A custom element is an element whose constructor and prototype are defined by a developer, instead of by the user agent. 


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
![Alt text](./_images/custom-elements-browser-support.png)


#### SHADOW DOM
##### What
##### Why
> Web components aim to provide the user a **simple element interface** that is rendered with **complexity hidden under the hood.**



###### Dom Pollution

Using code/libraries to build new web elements that do specific jobs, likfe for example take twitter typeahead, it i want to transform an input field to be an autocomplete field, it does a great job at that, although you have to write lots of code, but also if you inspect your DOM-TREE you will find that your simple 

`<input type="text" class="typeahead" />`

is now looking something like this

```
<input type="text" class="typeahead">
<span class="twitter-typeahead" style="position: relative; display: inline-block;"><input id="destination" value="" autocomplete="off" name="destination" type="text" placeholder="Search for a hotel, city or a landmark" blur-placeholder="Search for a hotel, city or a landmark" focus-placeholder="Start Typing ..." class="ys-input-group__input bold typeahead tt-input" spellcheck="false" dir="auto" style="position: relative; vertical-align: top; color: inherit; font-weight: bold;"><pre aria-hidden="true" style="position: absolute; visibility: hidden; white-space: pre; font-family: 'Source Sans Pro', ubuntu, 'Helvetica Neue', Helvetica, Arial, sans-serif; font-size: 15px; font-style: normal; font-variant: normal; font-weight: bold; word-spacing: 0px; letter-spacing: 0px; text-indent: 0px; text-rendering: auto; text-transform: none;"></pre><div id="dest-wrap" class="destination-wrapper hide"><div class="dropdown-wrapper">Destinations</div><div class="tt-menu desktop" style="position: absolute; top: 100%; left: 0px; z-index: 100; display: none;"><div class="tt-dataset tt-dataset-Recent"><div class="tt-heading text-danger"> Recent Searches </div><div class="fade in tt-suggestion tt-selectable">     <small class="pull-right"> 471 Properties </small>     <span> United Arab Emirates, <small class="text-muted"> Dubai </small> </span></div></div><div class="tt-dataset tt-dataset-Trends"><div class="tt-heading text-danger">Trending </div><div class="fade in tt-suggestion tt-selectable">     <small class="pull-right"> 471 Properties </small>     <span> Dubai, <small class="text-muted"> United Arab Emirates </small> </span></div><div class="fade in tt-suggestion tt-selectable">     <small class="pull-right"> 201 Properties </small>     <span> Jeddah, <small class="text-muted"> Saudi Arabia </small> </span></div><div class="fade in tt-suggestion tt-selectable">     <small class="pull-right"> 167 Properties </small>     <span> Makkah, <small class="text-muted"> Saudi Arabia </small> </span></div><div class="fade in tt-suggestion tt-selectable">     <small class="pull-right"> 19 Properties </small>     <span> Ramallah, <small class="text-muted"> Palestine </small> </span></div><div class="fade in tt-suggestion tt-selectable">     <small class="pull-right"> 64 Properties </small>     <span> Madinah, <small class="text-muted"> Saudi Arabia </small> </span></div></div><div class="tt-dataset tt-dataset-City"></div><div class="tt-dataset tt-dataset-Region"></div><div class="tt-dataset tt-dataset-Property"></div><div class="tt-dataset tt-dataset-Attraction"></div></div></div></span>

```



Which is ok! but it's also now inside your document, and this is indeed pollution, it's like cars smoke, with web components, we build custom-elements that leverage shadow-doms to hide away the implementation details, so to have a twitter typeahead input, you would do something like

and we can see here that :

- Details of the implementation are leaking.
- Queries over the document now include the all the new inserted dom.
- The new nodes may be affected by stylesheets, because the document author wasn’t expecting them.
- Some libraries might even change the position of a DOM in a document, thus the user might lose track, user here means developer (user of the library)



And this is where shadow-dom comes in, shadow-dom puts the element dom-tree (implementation) in a different scope of the current document, it is as if we are hiding the new dom in the shadows! and so.


- Details of the implementation are hidden.
- Queries over the document will not see the new dom, which is consistent with what you see while developing to what you see at render time.
- The new nodes are not affected by stylesheets, because they are not in the document scope.
- The dom position in the document tree will not change, thus no unexpected behaviours like messy styles or failing dom queries.


##### USAGE
##### Browser Support