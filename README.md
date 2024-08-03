# Webdev Notes

Notes for modern web development.

Please click the ☆ button on GitHub if this repository is helpful. Thank you!

## Overview of HTML

Source: https://web.dev/learn/html/overview

A HyperText Markup Language (HTML) document consists of a tree of nodes. Nodes are classified as either elements or text, and make up the structure or semantics of a webpage. This complete tree structure is called the Document Object Model (DOM), where Document refers to the webpage, Object refers to the JavaScript objects which represent each node, and Model refers to the parsing method as a whole. The HTML DOM API provides dynamic access to every node in the DOM.

A tag is everything between `<` and `>` characters. If a tag can contain content, then it must be split between an opening and closing tag. Content is everything between corresponding opening and closing tags. An element is a tag plus its content.

A non-replaced element does not replace its content with anything special. For example, `<p>Example</p>` is a non-replaced element because it displays its content exactly as written. All non-replaced elements have an opening and closing tag.

A replaced element replaces its content with something special. For example, `<video>...</video>` is a replaced element because it replaces the entire element with a video player. All replaced elements have an opening and closing tag.

A void element cannot have content, and therefore does not have a closing tag. An optional `/` may be be appended to a void element for readability. Some void elements are replaced, such as `<img>`, which displays an image. Some void elements are non-replaced, such as `<meta>`, which provides metadata about the webpage.

Attributes provide information about an element. These are key-value pairs in the opening tag of an element, however sometimes a value is optional or omitted. Some attributes are global, some only apply to a subset of elements, and some are specific to just one element. Values must be quoted if they contain a space or special character.

The default appearence of elements is set by user-agent stylesheets, which are provided by the browser. Therefore, without custom styling, different browsers may display certain elements differently.

## Document Structure

Source: https://web.dev/learn/html/document-structure

Always start the document with `<!DOCTYPE html>`, which tells the browser to conform to the latest HTML standards.

The root element is `<html>`, which contains all other HTML elements. The `lang` attribute should be set here, however this attribute can be used again in nested elements to mark text in other languages.

The `<head>` element contains webpage metadata, whereas the `<body>` element contains everything that might be rendered.

Always start the `<head>` element by setting the character encoding to UTF-8: `<meta charset="utf-8">`.

The `<title>` text is used in several important places, such as in the browser tab, search history, etc.

Set the initial viewport width to match the user's device: `<meta name="viewport" content="width=device-width">`. This tells the browser to use responsive design, rather than simply shrink a large viewport, which would make everything look very small and zoomed out.

The `<link>` element links the HTML document against external resources. There are a myriad of different types of resources that might be linked, including stylesheets, icons, language-dependent versions of the site, etc. Custom stylesheets should be loaded here to avoid using the user-agent stylesheet and repainting the site: `<link rel="stylesheet" href="styles.css">`.

Instead of writing CSS in external stylesheets, it can be nested into the `<head>` element with the `<style>` element.

A favicon is a small icon that appears in similar places to the webpage's title. It is particularly important to load a custom favicon because, if there are many tabs open, then the favicon will be the only indication of what webpage is loaded in each tab. Use `rel="icon"` link against favicons.

JavaScript scripts can be nested at the end of the `<body>` element with the `<script>` element. Use `type="module"` if it's a JavaScript module. Scripts are render-blocking, meaning the page will not continue painting to the screen until whenever the `<script>` element is finished. Scripts also block background downloading of other resource types. We also can't reference HTML elements in JavaScript until they've been declared. For all of these reasons, it's recommended to place `<script>` elements at the very end of the `<body>` element.

There are two attributes to change the default blocking behavior of scripts. The first is `defer`, which disables blocking and defers JavaScript execution until after the page has been fully rendered. The second is `async`, which disables blocking until the script is downloaded and ready to execute. Then, the script executes and blocks other processes. These two attributes are only valid on external scripts. Example: `<script src="js/switch.js" defer></script>`.

The `target="_blank"` attribute is mainly useful for opening links in a new tab.

HTML supports comments using the following syntax: `<!-- This is a comment -->`.