# Webdev Notes

Notes for modern web development.

Material is sourced from https://web.dev/ and summarized into what I consider to be the most notable or relevant information to my personal learning and use cases.

Please click the ☆ button on GitHub if this repository is helpful. Thank you!

## Index

### Learn HTML

[Overview of HTML](#overview-of-html)  
[Document Structure](#document-structure)  
[Metadata](#metadata)  
[Semantic HTML](#semantic-html)  
[Headings and Sections](#headings-and-sections)  
[Attributes](#attributes)  
[Text Basics](#text-basics)  
[Links](#links)  
[Lists](#lists)  
[Navigation](#navigation)  
[Tables](#tables)  
[Forms](#forms)  
[Images](#images)

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

## Metadata

Source: https://web.dev/learn/html/metadata

The `<meta>` tag typically uses either the `http-equiv` or `name` attribute to specify the type of metadata, followed by the `content` attribute that fills in the details. If the nature of the metadata matches a field that would normally be found in an HTTP header, then `http-equiv` is used. Otherwise, `name` is used.

Most metadata elements using `http-equiv` are not very useful, however `http-equiv="content-security-policy"` is something to look into for security purposes. Technically, the `<meta charset="utf-8">` element was once a `http-equiv`, but it was so often misspelled that `charset` as an attribute was standardized.

The `name="keywords"` metadata is useless nowadays due partly to past search engine optimization (SEO) abuse. This is similar to how YouTube themselves recommend against adding keywords to YouTube videos when uploading, unless the name of the topic of the video is often misspelled.

The `name="description"` metadata is displayed prominently in several places and is important for SEO. It should be brief, comprehensive, and insightful.

All webpages are indexed by search engines by default, however `<meta name="robots" content="noindex, nofollow">` can be used to opt out. The `noindex` value refers to the current page, while the `nofollow` value refers to all pages that can be reached via hyperlink on the current page.

Some browsers support custom colors for areas like the title bar and tab bar using the following: `<meta name="theme-color" content="#226DAA">`.

Open Graph is a protocol created by Facebook that enables a fancy way of presenting links to external sites. For example, when posting a link to a YouTube video on X, a medium-sized card will appear that contains an image, a title, and a description. The entire card is a link to the video. Many social media sites use the Open Graph protocol to achieve this effect.

When a link is posted, the host site looks for a few special `<meta>` elements on the targetted site to populate the card. If not found, then the information is pulled from elements like the `<title>` and `<meta name="description">`.

Different sites expect slightly different formatting. Here are a few examples of what the protocol is looking for:  
`<meta property="og:title" content="Example Title">`  
`<meta property="og:image" content="http://www.example.com/image.png">`  
`<meta name="twitter:url" content="https://www.example.com/">`

## Semantic HTML

Source: https://web.dev/learn/html/semantic-html

When the browser parses HTML, it builds the Document Object Model (DOM), the CSS Object Model (CSSOM), and the Accessibility Object Model (AOM). The AOM is a node tree similar to the DOM, but is focused on semantics rather than generic element and text structure. Modern semantic elements like `<header>`, `<section>`, and `<nav>` have a major positive affect on the AOM over non-semantic elements like `<div>` and `<span>`.

The Web Hypertext Application Technology Working Group (WHATWG) maintain the living HTML standard, while the Accessible Rich Internet Applications (ARIA) standard provides guidelines on how to increase accessibility of webpages.

The `role` attribute, often called an ARIA role, defines the role or semantics of any element. For example, `<p role="button">` hints to the AOM that this paragraph should be semantically interpretted as a button. Instead of using roles in this way however, the proper HTML element should be used that has the appropriate implicit role. For example, using `<button>` is better than using `role="button"` because it has an implicit role and comes with special button-related functionality, among other advantages.

When building a webpage, always take the time to think about which HTML element most closely matches its intended semantics. This reduces the need for future refactoring, improves CSS selectability, improves accessibility and in come cases SEO optimization, etc.

## Headings and Sections

Source: https://web.dev/learn/html/headings-and-sections

Semantic landmarks are defined as a set a HTML tags and roles that break the webpage into distinct areas, such as the site header, site footer, major articles, etc. These are specifically marked as "landmarks" in the AOM.

The `<header>` element is only a landmark if it is the site header, which takes on the role `banner`. Otherwise, it's a nested header and is treated in the AOM as a simple heading to an article or something similar.

The `<nav>` element is for navigation. If it's nested inside the banner, then it's considered the site navigation. Otherwise, it's internal navigation to some subsection of the webpage.

The `<footer>` element is only a landmark if it is the site footer, which takes on the role `contentinfo`. Otherwise, it's nested as is only relevant to its parent section. It's common to see `<address>` in the site footer, which contains contact information, but not physical addresses.

It's clear the these semantic HTML elements change meaning based on where they're located in the document. This has an affect on not only the AOM, but also search engines, CSS and JavaScript selectability, etc.

There should only be a single `<main>` element per document. It identifies the actual content of the webpage, such as the listing of news articles on a news site, the vertical list of posts on X, etc.

The `<aside>` element is for content that is only tangentially related to whatever is inside the `<main>` element, however it can also be nested inside `<main>` if it's only relevant to a subsection of content. It takes on the role `complementary`.

The `<article>` element is interesting. It's ideally meant to be used as a reusable piece of content. There shouldn't be a refactoring problem if the entire element were to be moved or copied somewhere else on the site, because the article itself is self-contained and includes all of the necessary information to be coherent regardless of where it might appear. For example, a post on Facebook can appear anywhere in the timeline without losing any context.

The `<section>` element is the most generic of all the semantic elements. It outlines a region that is logically consistent, but not necessarily an individual `<article>`. It probably contains its own header, may contain extra navigation, may contain a series of articles, etc. For example, on a news site, the categories of "World News" and "Technology News" might be two different sections.

There exist six headings: `<h1...6>`. The top-level heading should be included inside the site banner as `<h1>`, then each heading down the hierarchy of semantic elements should increment the level. Levels should not be skipped.

It's important use elements based on their meaning, rather than the CSS that the user-agent stylesheet applies by default. Any element can be made to look a certain way with custom CSS. When working with HTML, focus on proper semantics.

## Attributes

Source: https://web.dev/learn/html/attributes

Most attributes are key-value pairs that are placed in an element's opening tag, where the value should be always be quoted.

Boolean attributes should not include a value component. If the boolean attribute is present, then it is considered `true`. If it is missing, then it is considered `false`. Boolean attributes technically can include a value, but that value will simply be ignored and the expression will result in `true`. As a side note, when toggling boolean attributes in JavaScript, the attribute itself should be added or removed from the element entirely instead of changing its value. An example of a boolean attribute is `readonly`.

Enumerated attributes only accept a subset of valid values. If the attribute is missing, its value is missing, or its value is invalid, then some default will be used. The default value in each of these cases may not be the same. Needless to say, always specify a valid enumeration or don't include the attribute at all if it's not important. An example of an enumerated attribute is `type` in an `<input>` tag.

The global `id` attribute is extremely important to scripting, links, selectability, labels, accessibility, etc. Ids must be unique to the document.

An `href` may contain the "fragment" of a path, which points to a specific location on a webpage, rather than just the webpage itself. For example, `href="#about-us"` links to the element on the current page that has `id="about-us"`. The special fragment specifiers `#` and `#top` both link to the top of the current page.

The global `class` attribute is useful as a generic and easy way to target a group of elements for styling with CSS. Separate multiple class names with a space.

The global `style` attribute can be used for inline styling, however it is not recommended.

The global `contenteditable` attribute is powerful. It makes an element editable by the user. This can, for example, be used to make a user interface for editing the current page's styling.

Custom attributes can be used for storing metadata as part of an HTML element. These should start with `data-` so that certain APIs can be used and to avoid name collisions with non-custom attributes, however this prefix isn't technically required.

## Text Basics

Source: https://web.dev/learn/html/text-basics

The line break `<br>` element should be used for oddities like poetry, citations, etc. To space out elements like paragraphs, use CSS instead of inserting extra HTML elements.

Quotations come in two styles: blockquotes and inline quotations. Blockquotes `<blockquote>` are meant to be "lifted out" of the normal flow of a paragraph. Inline quotes `<q>` are meant to flow along with text in a paragraph.

If a quote comes from an external source, then it should be cited. The `<cite>` element should contain the name of a work, rather than someone's name or their contact information. If a quote needs to be cited but you don't want the citation to be visible as its own HTML element, then use the `cite` attribute in the `<blockquote>` or `<q>` element instead.

If a quote is in another language, remember to set the language with the `lang` attribute. Surprisingly, this tells voice software like Siri to use the proper pronunciation, and changes the quotation marks to match the locale.

Escape characters are necessary to display text that conflicts with significant HTML markup, such as `<`, `>`, `&`, and `"`. Unlike many programming languages where characters can be escaped with a simple prefix, HTML uses a prefix surrounded by `&` and `;`. For example: `&lt;`, `&gt;`, `&amp;`, and `&quot;`.

Escape sequences in HTML are also called "entities" because they can be used for more than just displaying reserved characters. A few common entities are `&copy;` for copyright, `&trade;` for trademark, and `&nbsp;` for non-breaking space, which can be used as a space that will not break the text onto a new line.

Any Unicode character can be printed using its codepoint. For example, `<` can be displayed with `&lt;`, `&#60;`, or `&#x3C`. If `<meta charset="utf-8">` is set, then Unicode characters can of course be printed without the assistance of escape sequences.

## Links

Source: https://web.dev/learn/html/links

The anchor element `<a>` with the hyperlink attribute `href` makes up a clickable link. A link may be absolute or relative. If absolute, then a protocol and domain name should be specified, such as `https://example.com`. If relative, then the link is bound to the current website.

The content of `<a>` should briefly describe the destination of the link and nothing else. It is important to give complete context to the user about where a link might take them. In line with this, use the `external` attribute if the link directs the user to an external site.

Links should also be styled differently from surrounding text. Include an `alt` attribute if the link is an image or some resource that has a chance to not load properly.

It is not recommended to include a link insde of some interactable element, or vice versa. Interactions inside interactions can make for a poor user experience. For example, don't place a `<button>` inside a `<a>`.

## Lists

Source: https://web.dev/learn/html/lists

Unordered lists `<ul>` should be used when order isn't significant. Use list items `<li>` as immediate child elements.

Ordered lists `<ol>` should be used when order is significant. Use list items `<li>` as immediate child elements. The `type` attribute can be used to swap the ordinals with something else, such as letters or roman numerals. The `reverse` boolean attribute reverses the ordering. The `start` attribute specifies the starting ordinal of the list.

The `<li>` element can have the `value` attribute, which sets the list item's ordinal to that value. The subsequent list items will then continue from that value.

Although many elements have these stylistic attributes, it is important to consider if, for example, the ordinal should be a decimal number or roman numeral number for semantic reasons or just for stylistic reasons. Remember that HTML elements and attributes are generally supposed to be focused on semantics, while CSS should responsibility for styling.

Description lists `<dl>` contain description terms `<dt>` and description definitions `<dd>`. These terms and definitions should be placed adjacent to each other, rather than nested. The relationship between terms and definitions is many-to-one or one-to-many. Description lists can be used for people, technical terms, or anything else that fits the key-value nature. It is recommended to wrap corresponding groups of definitions in a `<div>` element if they should be styled as a single unit, which means it is valid to sometimes see a `<dl>` where its immediate children are not restricted only to `<dt>` and `<dd>`.

## Navigation

Source: https://web.dev/learn/html/navigation

Local navigation refers to links that go to somewhere on the same site, but are not persistent across every page on the site. For example, an inline link in the middle of a paragraph that jumps to the top of a related page, or a table of contents that links to different parts of the current page.

Global navigation refers to links that are always available to click on, regardless of which page is currently loaded. For example, a list of high-level links in the site banner or footer.

A breadcrumb refers to a series of links that show the hierarchy of the current page in relation to the root of the website, or the pages that the user navigated to in order to reach the current page.

It is very important for usability that site navigation, both global and local, can be reached with as few clicks as possible. It should not be difficult to get to where the user wants to go.

## Tables

Source: https://web.dev/learn/html/tables

The `<table>` element should be used for tabular 2D data being compared, sorted, calculated, or cross-referenced. For use cases such as a grid of images, a CSS grid should be used instead.

The `<caption>` element should be the first nested element inside a table. It serves as the table's title. The `aria-describedby` attribute can be used on surrounding paragraphs that describe the table or state what its purpose is. Another option is to nest the table in a `<figure>` element, along with a `<figcaption>` element.

Tables are made up of three sections after the caption: `<thead>`, `<tbody>`, and `<tfoot>`, or any combination of the three. Each section should contain rows `<tr>` of cells. Each row of cells should contain header cells `<th>` if inside the `<thead>` section, otherwise data cells `<td>` if inside the `<tbody>` or `<tfoot>` sections.

The `rowspan` and `colspan` attributes can be used to merge cells across rows and columns.

Only use `<table>` for data that you could see yourself presenting in a spreadsheet at a business meeting. Otherwise, consider other approaches like CSS grid or description lists. Tables are more complicated to work with and require more work and detail in the AOM. They weren't designed to handle things like image galleries or lists.

## Forms

Source: https://web.dev/learn/html/forms

When data needs to be inputted by the user, validated, and sent to a server for processing, use the `<form>` element. The `action` attribute specifies the URL that processes the submitted data, which is the current URL if omitted. The `method` attribute specifies the HTTP method used.

Form controls are widgets that make up the form. Each control that needs processing should have a `name` attribute. If for some reason a control should be placed outside the `<form>` element, use the `form` attribute to specify the id of the form that the control belongs to.

The `GET` HTTP method appends form data to the `action` URL as name-value pairs. The `POST` HTTP method appends form data to the body of the HTTP request, for lengthy and secure submissions.

Many form controls can override attributes set on the parent `<form>` element. These attributes start with the prefix `form`, such as `formaction`, `formmethod`, etc.

When a form is submitted, all controls that have a `name` and `value` are sent. There are some controls that will consider inner text content as their value, if the `value` attribute is omitted.

Radio buttons within a group should have the same name. There is a "only-one-can-be-selected" rule to form controls with the same name, which creates the effect of only being able to select one radio button. The `checked` attribute will select a button by default. The `required` attribute can be added to any radio button in a group to force the user to make a selection before submitting. It is best practice to always inform the user when input or a selection is required, regardless of the control `type`.

The `<label>` element associates text content with a control. This makes it easier to click on the control and gives accessibility information about what the control might expect as an input. Use the `for` attribute to link the `<label>` with its corresponding control, or alternatively nest the control within the `<label>` element.

For groups of radio buttons or checkboxes, surround the entire group in a `<fieldset>` element, then use the `<legend>` element as its first child, which acts as a description for the entire group.

Try to use the input `type` that best matches your use case. For example, if inputting a telephone number, use `type="tel"`. If inputting an email, use `type="email"`. The keyboard displayed on mobile devices, and perhaps other behaviors, will be different.

Forms can be validated on the client before being sent to the server. One thing to note is that CSS pseudoclasses will update elements as their validity changes in realtime, whereas the form validation itself will not trigger until the user presses the `<button type="submit">` again.

Validation attributes include `required`, `pattern`, `max`, `min`, and `maxLength`. Max length is known to feel frustrating for users, so it may be better to indicate "remaining characters" in a paragraph or an `<output>` element, which is meant to display the result of a calculation from a user input.

Remember to validate form data on both the client and the server. Client code can be edited or malicious. Client-side validation should be used as a gentle guide for clarification.

## Images

Source: https://web.dev/learn/html/images

As usual, if an image is stylistic in nature, then it should be added with CSS. If it is semantic in nature and part of the structure of the page, then it should be added with HTML.

The `<img>` element requires a `src` attribute for the filename. The `alt` attribute should be used as a substitute if the image cannot be loaded, and for accessibility reasons.

Alternative text should be as concise as possible, and only include necessary information based on the context of the image on the page. Don't repeat information in the alt text that is already stated elsewhere. For example, a purely decorative image should have `alt=""`. An image of a graph should have alt text that describes what can be learned from the graph, not what the graph looks like. An image of a standard icon, like a magnifying glass, should have `alt="Search"`. Never include "An image of..." in the alt text because it's already known that an image is supposed to exist there.

The `<picture>` element can be used to specify alternative versions of an image based on resolution and viewport size. Its children should include a list of `<source>` elements, which specify a single option for an image along with a media query, and an `<img>` element, which is the default if none of the other options are good enough. The `srcset` attribute can alternatively be used on the `<img>` element, which achieves a similar result.

The `width` and `height` attributes should be included on the `<img>` element to avoid content-shifting as the image is fetched from the server and painted onto the page.

The `loading` attribute is by default set to `eager`, which loads the image alongside the rest of the page. This may result in longer loading times for the user, and download potentially unnecessary data. Lazy loading `lazy` can be used to only load images that are likely to be displayed, which is determined based on the location of the user's viewport while scrolling down the page.