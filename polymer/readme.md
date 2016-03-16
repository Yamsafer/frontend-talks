<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Polymer](#polymer)
  - [What](#what)
  - [Why](#why)
  - [Who](#who)
  - [Usage](#usage)
  - [In depth](#in-depth)
    - [Registration & Lifecycle](#registration-&-lifecycle)
    - [Declared properties](#declared-properties)
    - [Local dom](#local-dom)
    - [Events](#events)
    - [Data binding](#data-binding)
    - [Behaviors](#behaviors)
    - [Styling](#styling)
  - [Community Elements](#community-elements)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Polymer

### What
* Polymer is a library to help you build Web Components.
* Polymer is not a framework and it’s not trying to replace any existing frameworks.
* The very premise of web components is that they are not a framework

![Alt text](./_images/polymer-position.png)

### Why
> The goal is to make it easier for you to build web components that you can use anywhere. Use them in an angular app, or a react app, or build your entire app out of components. That’s the dream!

### Who
Google.

### Usage

`bower install --save Polymer/polymer`

Anytime you create a new Polymer element, you’ll want to create an html file to hold its definition. 

Use HTML Imports, to load dependency elements inside the newly created element, and later we will use HTML Imports to import our element into the document where it will register itself as a new element inside the browser and be used.

```
<!-- date-format.html -->
<link rel=“import” href=“bower_components/polymer/polymer.html”>
<link rel=“import” href=“vendor/momentjs.html”>
<dom-module id=“date-format">
  <template>
        <style>
        /* CSS rules for your element */
        :host {
            display: block;
            font-weight : bold;
      color: grey;
        }
        </style>
        <!-- shadow/local DOM for your element -->
        <span> {{ dateFromatted }} </span> <!-- data bindings in local DOM -->
    </template>
  <script>
    // element registration
    Polymer({
      is: ‘date-format',
            // add properties and methods on the element's prototype
      properties: {
          // declare properties for the element's public API
        date: String,
        format: String,
          dateFormatted: String
      },
      ready : function(){
        var date = this.date;
        var format = this.format;
        this.dateFormatted = this._format(date, format);
      },
      _format : function(date, format){
    return moment(date).format(format);
    }
    });
  </script>
</dom-module>
```
use it
```
  <head>
    <script src="bower_components/webcomponentsjs/webcomponents.min.js"></script>

    <link rel=“import” href=“elements/date-format.html”>
  </head>
  <body>
    <date-format date="14-1-1989" format="MMM, DD"></date-format>
  </body>

```
result will be ishi zay hek
> **Jan, 14**

-------------------------------------------

### In depth

##### Registration

```javascript
// register an element
MyElement = Polymer({
  is: 'my-element',
  created: function() {
    this.textContent = 'My element!';
  }
});
```

> By specification, the custom element’s name **must contain a dash (-)**.

use in document

`<my-element></my-element>`

or in javascript with the constructor

`var myEl = new MyElement();`

* The `Polymer` function registers the element with the browser and returns a constructor that can be used to create new instances of your element via code.
* The `Polymer` function sets up the prototype chain for your custom element, chaining it to the Polymer`Base` prototype.
* use [behaviors](#behaviors) to share code between elements.



We can as well extend native elements (later will be able to extend custom-elements as well)

```
MyInput = Polymer({
  is: 'my-input',
  extends: 'input',
  created: function() {
    this.style.border = '1px solid red';
  }
});
```

```
<input is="my-input">
```

##### Lifecycle

```
MyElement = Polymer({
  is: 'my-element',
  created: function() {
	// Use instead of createdCallback.
	// Called when the element has been created
    // Before property values are set and shadow/local DOM is initialized.
  },
  ready: function() {
	// Called after property values are set and local DOM is initialized.
  },
  attached: function() {
  	// Use instead of attachedCallback.
	// Called after the element is attached to the document. 
    // ex. Access computed dom styles, add document-level event listeners
  },
  detached: function() {
    // Use instead of detachedCallback.
    // Called after the element is detached from the document.
  },
  attributeChanged: function(name, type) {
	// Called when one of the element's attributes is changed.
  }

});
```

In a document dom-tree, elemens are usually initialized in order

consider the following example

```
<avatar-list>
  <my-photo class="photo" src="one.jpg">First photo</my-photo>
  <my-photo class="photo" src="two.jpg">Second photo</my-photo>
</avatar-list>
```

>  `<avatar-list> ` is *likely* to have its `ready` method called before `<my-photo> ` `ready` method.

What about siblings like `<my-photo>` ?

> There are no guarantees with regard to initialization timing between sibling elements.



####Local dom

Naturally a custom-element tempalte will be treated as a shadow-dom, 



#### Declared properties



#### Events



#### Data binding



#### Behaviors



#### Styling

------------------------

### Community Elements
* Elements Catalog
* Customelemtns.io