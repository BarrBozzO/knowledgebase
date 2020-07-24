# CORS - Cross-Origin Resource Sharing

The Cross-Origin Resource Sharing standard works by adding new HTTP headers that let servers describe which origins are permitted to read that information from a web browser. Additionally, for HTTP request methods that can cause side-effects on server data (in particular, HTTP methods other than `GET`, or `POST` with certain `MIME` types), the specification mandates that browsers **"preflight"** the request, soliciting supported methods from the server with the HTTP `OPTIONS` request method, and then, upon "approval" from the server, sending the actual request. Servers can also inform clients whether "credentials" (such as Cookies and HTTP Authentication) should be sent with requests.

CORS failures result in errors, but for security reasons, specifics about the error are not available to JavaScript. All the code knows is that an error occurred. The only way to determine what specifically went wrong is to look at the browser's console for details.

**Origin** consists of:

- Port
- Domain
- Protocol (https://, http://)

There are **2 CORS request types**:

- simple
- preflight

## Simple requests (GET, POST, and HEAD)

The browser deems the request to be a **"simple"** request when the request itself meets a certain set of requirements:

- method to be equal to: `GET`, `POST`, or `HEAD`
- [A CORS safe-listed header](https://fetch.spec.whatwg.org/#cors-safelisted-request-header) is used
- When using the `Content-Type` header, only the following values are allowed: `application/x-www-form-urlencoded`, `multipart/form-data`, or `text/plain`
- No event listeners are registered on any XMLHttpRequestUpload object
- No ReadableStream object is used in the request

The request is allowed to continue as normal if it meets these criteria, and the `Access-Control-Allow-Origin` header is checked when the response is returned.

## Preflight request (OPTIONS)

If a request does not meet the criteria for a simple request, the browser will instead make an automatic preflight request using the `OPTIONS` method. If the result of the `OPTIONS` call dictates that the request cannot be made, the actual request to the server will not be executed.

The preflight request sets the mode as `OPTIONS` and sets a couple of headers to describe the actual request that is to follow:

- `Access-Control-Request-Method`: The intended method of the request (e.g., `GET` or `POST`)
- `Access-Control-Request-Headers`: An indication of the custom headers that will be sent with the request
- `Origin`: The usual origin header that contains the script's current origin

An example of such a request might look like this:

```
# Request
curl -i -X OPTIONS localhost:3001/api/ping \
-H 'Access-Control-Request-Method: GET' \
-H 'Access-Control-Request-Headers: Content-Type, Accept' \
-H 'Origin: http://localhost:3000'
```

This request basically says

> "I would like to make a GET request with the Content-Type and Accept headers from http://localhost:3000 - is that possible?".

The server will include some `Access-Control-*` headers within the response to indicate whether the request that follows will be allowed or not. These include:

- `Access-Control-Allow-Origin`: The origin that is allowed to make the request, or `*` if a request can be made from any origin
- `Access-Control-Allow-Methods`: A comma-separated list of HTTP methods that are allowed
- `Access-Control-Allow-Headers`: A comma-separated list of the custom headers that are allowed to be sent
- `Access-Control-Max-Age`: The maximum duration that the response to the preflight request can be cached before another call is made

The response would then be examined by the browser to decide whether to continue with the request or to abandon it.

So a response to the earlier example might look like this:

```
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET,HEAD,PUT,PATCH,POST,DELETE
Vary: Access-Control-Request-Headers
Access-Control-Allow-Headers: Content-Type, Accept
Content-Length: 0
Date: Fri, 05 Apr 2019 11:41:08 GMT
Connection: keep-alive
```

The `Access-Control-Allow-Origin` header, in this case, allows the request to be made from any origin, while the `Access-Control-Allow-Methods` header describes only the accepted HTTP methods. If a given HTTP method is not accepted, it will not appear in this list.

In this example, `Access-Control-Allow-Headers` echos back the headers that were asked for in the OPTIONS request. This indicates that all the requested headers are allowed to be sent. If for example, the server doesn't allow the Accept header, then that header would be omitted from the response and the browser would reject the call.

## Requests with credentials

By default, in cross-site `XMLHttpRequest` or `Fetch` invocations, browsers will **not** send credentials. A **specific flag** has to be set on the `XMLHttpRequest` object or the `Request` constructor when it is invoked.

```
const invocation = new XMLHttpRequest();
const url = 'http://bar.other/resources/credentialed-content/';

function callOtherDomain() {
  if (invocation) {
    invocation.open('GET', url, true);
    invocation.withCredentials = true;
    invocation.onreadystatechange = handler;
    invocation.send();
  }
}
```

Line 7 shows the flag on `XMLHttpRequest` that has to be set in order to make the invocation with Cookies, namely the `withCredentials` boolean value. By default, the invocation is made without Cookies. Since this is a simple `GET` request, it is not preflighted, but the browser will **reject** any response that does not have the `Access-Control-Allow-Credentials: true` header, and not make the response available to the invoking web content.

Flags for CORS credentialed requests:

- [withCredentials](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/withCredentials)
- [credentials](https://developer.mozilla.org/en-US/docs/Web/API/Request/credentials)

### Credentialed requests and wildcards

When responding to a credentialed request, the server must specify an origin in the value of the `Access-Control-Allow-Origin` header, instead of specifying the `*` wildcard.

---

# References

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#Preflighted_requests)
- [simply about CORS](https://auth0.com/blog/cors-tutorial-a-guide-to-cross-origin-resource-sharing/)
- [how to fix CORS errors](https://medium.com/@dtkatz/3-ways-to-fix-the-cors-error-and-how-access-control-allow-origin-works-d97d55946d9)
- [web fonts](https://www.w3.org/TR/css-fonts-3/#font-fetching-requirements)
