# How Broswer Works

Prerequisite: [What happens when you type a URL into your browser?](https://aws.amazon.com/blogs/mobile/what-happens-when-you-type-a-url-into-your-browser/)

1. Browser looks up IP address for the domain

- If the browser cannot find the IP address at any of those cache layers, the DNS server on your corporate network or at your ISP(Internet service provider) does a recursive DNS(Domain Name System) lookup.

2. Browser initiates TCP connection with the server

- Once the browser finds the server on the Internet, it establishes a TCP(Transmission Control Protocol) connection with the server and if HTTPS is being used, a TLS(Transport Layer Security) handshake takes place to secure the communication.

3. Browser sends the HTTP request to the server

- `GET /hello-world HTTP/1.1`: you want to `GET` resource at `/hello-world` and to communicate with `HTTP/1.1`.

4. Server processes request and sends back a response

- The requested resource at that path is either content like HTML, CSS, Javascript, or image files, or data

5. Browser renders the content

- Browser inspects the response headers for information on how to render the resource. For example, `Content-Type: text/html; charset=utf-8` on header tells the browser it received an HTML resource in the response body.

## How browser renders content

Let's take step further. As we are frontend developers, we must know how browser renders content.

According to [How browsers work](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work) and [Critical Rendering Path](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path)

1. Building the DOM(Document Object Model) tree

- The HTML response turns into tokens which turns into nodes which turn into the DOM Tree.
- DOM construction is incremental. Incremental DOM construction means that the browser builds the DOM tree gradually, as it parses the HTML document. It doesn't wait for the entire document to be parsed before starting to construct the DOM.

2. Building the CSSOM(CSS Object Model) tree

- While the DOM construction is incremental, CSSOM is not. CSS is render blocking: the browser blocks page rendering until it receives and processes all the CSS.
- CSS is render blocking because rules can be overwritten, so the content can't be rendered until the CSSOM is complete.

3. Rendering tree

- The render tree captures both the content and the styles: the DOM and CSSOM trees are combined into the render tree.

4. Layout

- The layout step determines where and how the elements are positioned on the page, determining the width and height of each element, and where they are in relation to each other.

5. Paint

- The last step is painting the pixels to the screen

> 💡 What happens while the browser builds the DOM tree:<br />
> While the browser builds the DOM tree using the main thread, the preload scanner in the background will parse through the content available and request high-priority resources like CSS, JavaScript, and web fonts. Thanks to the [preload scanner](https://web.dev/articles/preload-scanner), we don't have to wait until the parser finds a reference to an external resource to request it.

> 💡 JavaScript can block HTML parsing:<br />
> When the HTML parser finds a `<script>` tag, it pauses the parsing of the HTML document and has to load, parse, and execute the JavaScript code. Why? because JavaScript can change the shape of the document using things like `document.write()` which changes the entire DOM structure

## Next topic

- [How react renders content](/)
