**[See the demo](http://padolsey.github.com/findAndReplaceDOMText/demo.html)**

`findAndReplaceDOMText` searches for regular expression matches in a DOM node and wraps all matches (and portions of matches separated by node bounderies) with a specified element.

For example:

```html
<p id="t">
	123 456 999
</p>
```

```js
findAndReplaceDOMText(/9+/, document.getElementById('t'), 'em');
```

This would result in:

```html
<p id="t">
	123 456 <em>999</em>
</p>
```

And it also works when matches are spread **across multiple nodes**! E.g.

```html
<p id="t">
	123 456 99<span>9 foo</span>
</p>
```

```js
findAndReplaceDOMText(/9+/, document.getElementById('t'), 'em');
```

This would result in:

```html
<p id="t">
	123 456 <em>99</em><span><em>9</em> foo</span>
</p>
```

The `EM` element has been added twice, to cover both portions of the match.

### The third argument

The third argument to `findAndReplaceDOMText` can be one of:

 * A nodeName (e.g. `"em"` or `"span"`)
 * A "stencil" node that will be cloned.
 * A function which will return an element whenever called with a match portion (text)

E.g. if I wanted to replace every instance of `foo` in an element with `<span class="found">` I would simply do:

```js
var span = document.createElement('span');
span.className = 'found';
findAndReplaceDOMText(/foo/g, myElement, span);
```

### Changelog

 * 0.1: Initial commit + Fix for IE's broken HTML5 cloneNode ([pull request](https://github.com/padolsey/findAndReplaceDOMText/pull/3))
 * 0.11: Minor fix: Make sure replacement node function is called in order of matches (see [issue #4](https://github.com/padolsey/findAndReplaceDOMText/issues/4))