### URI Template

A compact sequence of characters for describing a range of Uniform Resource Identifiers 
through variable expansion, see [RFC 6570]. URI Templates provide a mechanism for abstracting a space of resource identifiers such that the variable parts can be easily identified and described.


|Examples of URI Template in action|
|-------------|
|https://api.github.com|
|https://api.github.com/search/repositories?q=mobile&per_page=10|


### Verbs

|Verb|Description|
|-------------|-------------|
|HEAD|Can be issued against any resource to get just the HTTP header info.|
|GET|Used for retrieving resources.|
|POST|Used for creating resources.|
|PATCH|Used for updating resources with partial JSON data. For instance, an Issue resource has title and body attributes. A PATCH request may accept one or more of the attributes to update the resource. PATCH is a relatively new and uncommon HTTP verb, so resource endpoints also accept POST requests.|
|PUT|Used for replacing resources or collections. For PUT requests with no body attribute, be sure to set the Content-Length header to zero.|
|DELETE|Used for deleting resources.|

From [GitHub Enterprise API]

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

# Attributes

#### `?expand=space,body.view,version,container`

1. When GET-ing a complex resource.
2. When POST-ing a new resource and you want the response to be expanded.

From: [Atlassian REST API]

#### `?envelope=true` or `?callback`

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

Example from [GitHub Enterprise API]
```
$ curl https://api.github.com?callback=foo
```
```javascript
/**/foo({
  "meta": {
    "status": 200,
    "X-RateLimit-Limit": "5000",
    "X-RateLimit-Remaining": "4966",
    "X-RateLimit-Reset": "1372700873",
    "Link": [ // pagination headers and other links
      ["https://api.github.com?page=2", {"rel": "next"}]
    ]
  },
  "data": {
    // the data
  }
})
```

#### `?fields=AccountNumber,BillingPostalCode`

Example response from [SalesForce SObject API]:

```json
{
    "AccountNumber" : "CD656092",
    "BillingPostalCode" : "27215"
}
```

#### `attributes` in response

```json
{ 
    "attributes" : {
        "type" : "Merchandise__c",
        "url" : "/services/data/v20.0/sobjects/Merchandise__c/a00D0000008oWP8IAM"
     },
    "Id" : "a00D0000008oWP8IAM",
    "OwnerId" : "005D0000001KyEIIA0",
    "IsDeleted" : false,
    "Name" : "Example Merchandise",
    "CreatedDate" : "2012-07-12T17:49:01.000+0000",
    "CreatedById" : "005D0000001KyEIIA0",
    "LastModifiedDate" : "2012-07-12T17:49:01.000+0000",
    "LastModifiedById" : "005D0000001KyEIIA0",
    "SystemModstamp" : "2012-07-12T17:49:01.000+0000",
    "Description__c" : "Merch with external ID",
    "Price__c" : 10.0,
    "Total_Inventory__c" : 100.0,
    "Distributor__c" : null,
    "MerchandiseExtID__c" : 123.0
}
```

# Authentification

Flow from [SalesForce API]:

1. Web server flow, where the server can securely protect the consumer secret.
2. User-agent flow, used by applications that cannot securely store the consumer secret.
3. Username-password flow, where the application has direct access to user credentials.


[GitHub Enterprise API]:https://developer.github.com/enterprise/2.3/v3/
[What Every Developer should know about HTTP]:https://www.amazon.com/gp/product/B0076Z6VMI/ref=oh_aui_d_detailpage_o00_?ie=UTF8&psc=1
[Best practices for a pragmatic restful API]:http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api
[Atlassian REST API]:https://docs.atlassian.com/confluence/REST/latest/
[RFC 6570]:http://tools.ietf.org/html/rfc6570
[SalesForce API]:https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm
[SalesForce SObject API]:https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_get_field_values.htm
