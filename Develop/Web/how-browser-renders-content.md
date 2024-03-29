# How Browser Renders Content

TL;DR;

1. DOM tree
2. CSSOM tree
3. Render tree
4. Layout
5. Paint

So far, we've looked over [What Happens Behind Browser](./what-happens-behind-browser.md)

## The steps of how browser renders content

According to [How browsers work](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work) and [Critical Rendering Path](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path)

1. Building the DOM(Document Object Model) tree

- The HTML response turns into tokens which turns into nodes which turn into the DOM Tree.
- DOM construction is incremental. Incremental DOM construction means that the browser builds the DOM tree gradually, as it parses the HTML document. It doesn't wait for the entire document to be parsed before starting to construct the DOM.

2. Building the CSSOM(CSS Object Model) tree

- While the DOM construction is incremental, CSSOM is not. CSS is render blocking: the browser blocks page rendering until it receives and processes all the CSS.
- CSS is render blocking because rules can be overwritten, so the content can't be rendered until the CSSOM is complete.

3. Render tree

- The render tree captures both the content and the styles: the DOM and CSSOM trees are combined into the render tree.

4. Layout

- The layout step determines where and how the elements are positioned on the page, determining the width and height of each element, and where they are in relation to each other.

5. Paint

- The last step is painting the pixels to the screen

> 💡 What happens while the browser builds the DOM tree:<br />
> While the browser builds the DOM tree using the main thread, the preload scanner in the background will parse through the content available and request high-priority resources like CSS, JavaScript, and web fonts. Thanks to the [preload scanner](https://web.dev/articles/preload-scanner), we don't have to wait until the parser finds a reference to an external resource to request it.

> 💡 JavaScript can block HTML parsing:<br />
> When the HTML parser finds a `<script>` tag, it pauses the parsing of the HTML document and has to load, parse, and execute the JavaScript code. Why? because JavaScript can change the shape of the document using things like `document.write()` which changes the entire DOM structure

## Furthermore

- [What makes React exceptional](../Reactjs/what-makes-react-exceptional.md)

---

If you have any questions or ideas, please leave a comment on this issue :)
