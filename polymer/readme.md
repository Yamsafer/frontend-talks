### Polymer

#### What
* Polymer is a library to help you build Web Components.
* Polymer is not a framework and it’s not trying to replace any existing frameworks.
* The very premise of web components is that they are not a framework

![Alt text](./_images/polymer-position.png)

#### Why
> The goal is to make it easier for you to build web components that you can use anywhere. Use them in an angular app, or a react app, or build your entire app out of components. That’s the dream!

#### Who
Google.

#### Usage

```
<!-- Webcomponents polyfill library -->
<script src="bower_components/webcomponentsjs/webcomponents.min.js"></script>
```

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
        :host {
            display: block;
            font-weight : bold;
      color: grey;
        }
        </style>
        <span> {{ dateFromatted }} </span>
    </template>
  <script>
    Polymer({
      is: ‘date-format',
      properties: {
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

