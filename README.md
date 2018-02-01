# Getting started with the IIS CORS Module

User agents such as browsers usually apply same-origin restrictions to network requests. These restrictions would prevent a malicious page from making a cross origin request initiated from within a script. As an example, this means odinarily a script served from `https://foo.com` cannot make a request to `https://bar.com`. However, there are instances in which you may want to allow sites to make these requests. For example, it's a common practice the split the web frontend (`https://contoso.com`) from the service hosting your API (`https://api.contoso.com`). For such scenarios to work, you will to configure your API to reply with appropriate CORS headers. The IIS CORS module provides a way for web administrators and web site authors to easily support the CORS protocol by delegating all CORS protocol handling to the module. 

## What is CORS?

Cross Origin Resource Sharing (CORS) is a W3C standard that allows an user agent to gain permission to request a resource by a mechanism that uses additional HTTP headers.

The CORS specification makes the distinction between **Simple** and **Preflighted** CORS requests and the IIS CORS can help you with both.

### Simple Requests

