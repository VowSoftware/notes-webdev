# Webdev Notes

Notes for modern web development.

Please click the ☆ button on GitHub if this repository is helpful. Thank you!

## Overview of HTML

Source: https://web.dev/learn/html/overview

A **HyperText Markup Language (HTML)** document consists of a tree of nodes. **Nodes** are classified as either elements or text, and make up the structure or semantics of a webpage. This complete tree structure is called the **Document Object Model (DOM)**, where Document refers to the webpage, Object refers to the JavaScript objects which represent each node, and Model refers to the parsing method as a whole. The **HTML DOM API** provides dynamic access to every node in the DOM.

A **tag** is everything between `<` and `>` characters. If a tag can contain content, then it must be split between an opening and closing tag. **Content** is everything between corresponding opening and closing tags. An **element** is a tag plus its content.

A **non-replaced element** does not replace its content with anything special. For example, `<p>Example</p>` is a non-replaced element because it displays its content exactly as written. All non-replaced elements have an opening and closing tag.

A **replaced element** replaces its content with something special. For example, `<video>...</video>` is a replaced element because it replaces the entire element with a video player. All replaced elements have an opening and closing tag.

A **void element** cannot have content, and therefore does not have a closing tag. An optional `/` maybe be appended to a void element for readability. Some void elements are replaced, such as `<img>`, which displays an image. Some void elements are non-replaced, such as `<meta>`, which provides metadata about the webpage.

**Attributes** provide information about an element. These are key-value pairs, however sometimes a value is optional or omitted. Some attributes are global, some only apply to a subset of elements, and some are specific to just one element. Values must be quoted if they contain a space or special character.

The default appearence of elements is set by **user-agent stylesheets**, which are provided by the browser. Therefore, without custom styling, different browsers may display certain elements differently.