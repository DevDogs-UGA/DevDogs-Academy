Outline/TOC/TODO
- [ ] Intro/what is HTML?
- [ ] Comments
- [ ] What are tags?
  - [ ] Tags carry semantic meaning
  - [ ] Case insensitive
  - [ ] Whitespace between tags not needed
  - [ ] Self-closing vs not
  - [ ] Attributes
- [ ] Required tags
  - [ ] `<!doctype html>`
  - [ ] `<html>`
    - [ ] lang attr
  - [ ] `<head>`
  - [ ] `<title>`
  - [ ] `<body>`
- [ ] Other important tags
  - [ ] `<p>`
  - [ ] `<b>`
  - [ ] `<em>`
  - [ ] `<i>`
  - [ ] `<br />`
  - [ ] `<h1>`/`<h2>`/.../`<h6>`
  - [ ] `<ol>`/`<ul>`/`<li>`
  - [ ] `<a>`
  - [ ] `<img>`
  - [ ] `<div>`/`<span>`
  - [ ] `<link>`
  - [ ] `<style>`
  - [ ] `<script>`
- [ ] More resources

# HTML From \<head> to Tail
**H**yper**t**ext **M**arkup **L**anguage, or HTML for short, is the single most important element of the web. Both JavaScript and CSS, the other two parts of the HTML/JS/CSS trifecta, orbit around HTML as the source of truth in a webpage's content. Every frontend will have HTML in a pretty central role, and lots of other webthings build on an expected understanding of HTML concepts.

From a high level, the purpose of HTML is to put a webpage's content (the stuff you see) and metadata (other important stuff you don't see) into a meaningful structure so that the web browser can display it in a useful way. You can think of it kind of like a souped up word processor, defining headers, tables, paragraphs, and the like.[^word-proc]

In this article, we'll go over the most important parts of HTML to try and get you up to speed as fast as possible. We couldn't possibly go over every single thing in this article, though, so be sure to check out the resources mentioned at the end and dust off your Google-fu if you're curious about what else there is.

[^word-proc]: In fact, most word processors today (Word, Google Docs, LibreOffice) save their files using an HTML-derived format called XML.

## Required tags
The HTML standard requires you to include some basic tags in every single website in order for that site to be considered valid. If you don't include them, the web browser is allowed to [make assumptions about your page and tweak things to its liking](https://developer.mozilla.org/en-US/docs/Web/HTML/Quirks_Mode_and_Standards_Mode). Undefined behavior, ick! You should always start a new HTML file off with these tags present for basic structure.

### The DOCTYPE
There have been a number of different versions of HTML throughout the years. The modern version, HTML5, is what we're covering in this article. To help the browser identify a page as an HTML5 document, we have to provide a special marker called the DOCTYPE. Long story short, the first line in your HTML file should be a tag that looks like this:
```html
<!doctype html>
```

### The HTML Tag
TODO

## More resources
- https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML
