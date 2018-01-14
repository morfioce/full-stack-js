## Walking the DOM

DOM allows to do anything with elements and their contents, but first we need to reach the corresponding DOM object, get it into a variable, and then we are able to modify it.

All operations on DOM start with the document object. From it we can access any node.

Here’s a picture of links that allow to travel between DOM nodes:

<p align="center">
  <img src="../resources/images/dom-links.png">
</p>

## On top: documentElement and body

The topmost tree nodes are available directly as document properties:

`<html>` = document.documentElement
The topmost document node is document.documentElement. That’s DOM node of `<html>` tag.

`<body>` = document.body
Another widely used DOM node is the `<body>` element – document.body.

`<head>` = document.head
The `<head>` tag is available as document.head.

## Children: childNodes, firstChild, lastChild

There are two terms that we’ll use from now on:

* `Child nodes` (or children) – elements that are direct children. In other words, they are nested exactly in the given one. For instance, `<head>` and `<body>` are children of `<html>` element.

* `Descendants` – all elements that are nested in the given one, including children, their children and so on.

For instance, here `<body>` has children `<div>` and `<ul>` (and few blank text nodes):

```html
<html>
<body>
  <div>Begin</div>

  <ul>
    <li>
      <b>Information</b>
    </li>
  </ul>
</body>
</html>
```
…And if we ask for all descendants of `<body>`, then we get direct children `<div>`, `<ul>` and also more nested elements like `<li>` (being a child of `<ul>`) and `<b>` (being a child of `<li>`) – the entire subtree.

The `childNodes` collection provides access to all child nodes, including text nodes.

The example below shows children of `document.body`:

```html
<html>
<body>
  <div>Begin</div>

  <ul>
    <li>Information</li>
  </ul>

  <div>End</div>

  <script>
    for (let i = 0; i < document.body.childNodes.length; i++) {
      alert( document.body.childNodes[i] ); // Text, DIV, Text, UL, ..., SCRIPT
    }
  </script>
  ...more stuff...
</body>
</html>
```

Please note an interesting detail here. If we run the example above, the last element shown is `<script>`. In fact, the document has more stuff below, but at the moment of the script execution the browser did not read it yet, so the script doesn’t see it.

Properties `firstChild` and `lastChild` give fast access to the first and last children.

They are just shorthands. If there exist child nodes, then the following is always true:

```JavaScript
elem.childNodes[0] === elem.firstChild
elem.childNodes[elem.childNodes.length - 1] === elem.lastChild
```

There’s also a special function `elem.hasChildNodes()` to check whether there are any child nodes
