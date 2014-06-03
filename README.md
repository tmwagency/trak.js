# Trak - Universal event tracking API

## Usage:
Include fastclick.js in your JavaScript bundle or add it to your HTML page like this:
```js
<script type='application/javascript' src='/path/to/trak.js'></script>
```
Don't forget to add a [shim](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget.addEventListener#Compatibility) for `addEventListener` if you want to support IE8 and below.

There are two main ways to use **trak.js**, in you js code or as data attributes in your markup.

### JS implementation:
```js
Trak.event('category', 'action');
Trak.event('category', 'action', 'label');
Trak.event('category', 'action', 'label', value); // value is an integer
Trak.event('category', 'action', 'label', value, nonInteraction); // nonInteraction is an integer
```
##### Example:
`Trak.event('engagement', 'signpost', 'href');`

### Data attr implementation:
```js
<a href="#" data-trak='{"category":"Rating","action":"Comparison notepad","label":"Up"}'>link</a>
```

#### Data-attr wildcards:
Wildcards can be used to specify certain options like the page title or url. 
##### page.href: Uses `window.location.href`
`<a href="#" data-trak='{"category":"Rating","action":"page.href","label":"Up"}'>link</a>` 
##### page.title: Uses `document.title`
`<a href="#" data-trak='{"category":"Rating","action":"page.title","label":"Up"}'>link</a>`
##### link.href: Uses `this.href`
`<a href="#" data-trak='{"category":"Rating","action":"link.href","label":"Up"}'>link</a>` 
##### link.title: Uses `this.title`
`<a href="#" data-trak='{"category":"Rating","action":"link.title","label":"Up"}'>link</a>`

--- 

## Options
Various default **trak.js** options can be overridden:

### Trak.options.delimeter
**trak.js** includes a cleaning method to normalise the arguments that are passed to it.
```js
clean : function(str) {
  return str.toString().replace(/\s|'|"/g, this.options.delimeter).toLowerCase();
}
```
**Default**: `'_'`

**Alternatives**: Anything you like, preferably a hyphen

### Trak.options.trackType
Use this to change your default tracking provider.

**Default**: `'ga'`

**Alternatives**: `'gaq'`

## Which tracking API's are used?
The default implementation uses latest version of Google Analytics (`ga.js`) but **trak.js** also supports the older `_gaq` type. For more information about either, please visit https://developers.google.com/analytics/devguides/collection/analyticsjs/
