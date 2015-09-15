### POST response

*200 OK*
Standard response for successful HTTP requests. The actual response will depend on the request method used. 
In a GET request, the response will contain an entity corresponding to the requested resource. 
In a POST request, the response will contain an entity describing or containing the result of the action.

*CREATED 201*
Following a POST command, this indicates success, but the textual part of the response line indicates the 
URI by which the newly created document should be known.

*Specs:* http://tools.ietf.org/html/rfc2616#section-10.2.2

*Example:* http://docs.stormpath.com/rest/product-guide/#creating-resources

*303 See Other* (since HTTP/1.1)
The response to the request can be found under another URI using a GET method. When received in response to a 
POST (or PUT/DELETE), it should be assumed that the server has received the data and the redirect should be 
issued with a separate GET message.

### Response codes

|Source|Link|
|-------------|-------------|
|Yahoo|https://developer.yahoo.com/social/rest_api_guide/http-response-codes.html|


|Range|Category|
|-------------|-------------|
|100-199|Informational|
|200-299|Successful|
|300-399|Redirection|
|400-499|Client error|
|500-599|Server error|

From [What Every Developer should know about HTTP]


### `?envelope=true`

1. For cross domain requests via JSONP.
2. For clients that cannot read headers.

Example from [Best practices for a pragmatic restful API]:

```javascript
callback_function({
  status_code: 200,
  next_page: "https://..",
  response: {
    // ... actual JSON response body ... 
  }
})
```

[What Every Developer should know about HTTP]:https://www.amazon.com/gp/product/B0076Z6VMI/ref=oh_aui_d_detailpage_o00_?ie=UTF8&psc=1
[Best practices for a pragmatic restful API]:http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api
