# Getting started with the IIS CORS Module

User agents such as browsers usually apply same-origin restrictions to network requests. These restrictions would prevent a malicious page from making a cross origin request initiated from within a script. As an example, this means odinarily a script served from `https://foo.com` cannot make a request to `https://bar.com`. However, there are instances in which you may want to allow sites to make these requests. For example, it's a common practice the split the web frontend (`https://contoso.com`) from the service hosting your API (`https://api.contoso.com`). For such scenarios to work, you will to configure your API to reply with appropriate CORS headers. The IIS CORS module provides a way for web administrators and web site authors to easily support the CORS protocol by delegating all CORS protocol handling to the module. 

## What is CORS?

Cross Origin Resource Sharing (CORS) is a W3C standard that allows an user agent to gain permission to request a resource by a mechanism that uses additional HTTP headers.

The CORS specification makes the distinction between **Simple** and **Preflighted** CORS requests and the IIS CORS can help you with both.

### Simple Requests

Simple requests meet **ALL THREE** of the following criteria:

- The HTTP method is either a HEAD/GET/POST
- Apart from the headers set by the user agent, the only additional headers allowed are those defined in the Fetch spec as [CORS-safelisted-request-header](https://fetch.spec.whatwg.org/#cors-safelisted-request-header).
- The only allowed valued for the `Content-Type` header are `application/x-www-form-urlencoded`, `multipart/form-data`, and `text/plain`.

Here's what an example of a simple request might look like

```
GET http://bar.com/data.json HTTP/1.1
Host: bar.com
Connection: keep-alive
Origin: http://foo.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36
Accept: */*
DNT: 1
Referer: http://foo.com/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9

```
And here's the response from the server
```
HTTP/1.1 200 OK
Content-Type: application/json
Last-Modified: Thu, 01 Feb 2018 21:51:05 GMT
Accept-Ranges: bytes
ETag: "1f116fc2a69bd31:0"
Server: Microsoft-IIS/10.0
Access-Control-Allow-Origin: *
X-Powered-By: ASP.NET
Date: Thu, 01 Feb 2018 22:19:13 GMT
Content-Length: 38

{
    "backgroundColor": "#ff0000"
}
```