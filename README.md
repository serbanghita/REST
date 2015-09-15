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

|https://developer.yahoo.com/social/rest_api_guide/http-response-codes.html|
