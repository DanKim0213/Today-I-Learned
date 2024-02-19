# What Happens Behind Browser

TL;DR;

1. IP address for the domain
2. TCP Connection
3. HTTP request to the server
4. Response from the server
5. Browser rendering.

## What happens when you type a URL into your browser?

According to [What happens when you type a URL into your browser?](https://aws.amazon.com/blogs/mobile/what-happens-when-you-type-a-url-into-your-browser/):

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

## Furthermore

- [How Broswer Renders Content](./how-browser-renders-content.md)

---

If you have any questions or ideas, please leave a comment on this issue :)
