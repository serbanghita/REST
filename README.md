# History

The paper [Architectural Styles and the Design of Network-based Software Architectures] by
Roy Thomas Fielding introduces a series of *patterns* that offers software companies a faster and easier way to build and integrate web service APIs. Instead of defining of set of standards that supported multiple protocols and payload formats, Fielding suggested the use of the HTTP specification itself as a starting point. 

Since there are a variety of HTTP verbs already (e.g. GET, POST, PUT, DELETE, PATCH), and response codes provide details
on the success or failure of the call (e.g. 200 OK, 404 NOT FOUND, etc) most of the work was already done. Services can accept incoming payloads in a variety of formats, using HTTP request headers to indicate the type(s) of data formats desired including media such as images and videos.

Rather than requiring a specification, Fielding encouraged the use of common patterns on top of
these specifications. Calling it *REST* ("__Representational State Transfer__"), Fielding suggested that
services *should be stateless*, just as HTTP is stateless, further simplifying the service implementation
requirements.

From [A Practical Approach to API Design]

### [Richardson Maturity Model]

* **Level 1** - tackles the question of handling complexity by using divide and conquer, breaking a large service endpoint down into multiple resources. (Example: RPC-style service)
* **Level 2** - introduces a standard set of verbs so that we handle similar situations in the same way, removing unnecessary variation. (Example: RPC-style service that behaves differently on POST and GET)
* **Level 3** - introduces discoverability, providing a way of making a protocol more self-documenting. (HATEOAS)


# Designing

1. Identify participants
2. Identify activities
3. Break each activity into steps
4. Create and group API definitions and methods
5. Validate your API by testing



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

 > The newly created resource can be referenced by the URI(s) 
   returned in the entity of the response, with the most specific URI
   for the resource given by a **Location header** field. The response
   **SHOULD include an entity** containing a list of resource
   characteristics and location(s) from which the user or user agent can
   choose the one most appropriate. The entity format is specified by
   the media type given in the Content-Type header field.

*Specs:* http://tools.ietf.org/html/rfc2616#section-10.2.2
*Example:* http://docs.stormpath.com/rest/product-guide/#creating-resources

  > There's no absolute standard as to how to represent hypermedia controls.
  
From [Richardson Maturity Model]

*303 See Other* (since HTTP/1.1)
The response to the request can be found under another URI using a GET method. When received in response to a 
POST (or PUT/DELETE), it should be assumed that the server has received the data and the redirect should be 
issued with a separate GET message.

#### POST reponse code, link and body

If all goes well, the service replies with a response code of 201 to indicate that there's a new resource in the world.

```
HTTP/1.1 201 Created
Location: slots/1234/appointment
[various headers]

<appointment>
  <slot id = "1234" doctor = "mjones" start = "1400" end = "1450"/>
  <patient id = "jsmith"/>
</appointment>
```

The 201 response includes a location attribute with a URI that the client can use to GET the current state of that resource in the future. The response here also *includes a representation of that resource* to save the client an extra call right now.

From [Richardson Maturity Model]

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

# Hypermedia

  > There's no absolute standard as to how to represent hypermedia controls. What I've done here is to use the current recommendations of the REST in Practice team, which is to follow ATOM [RFC 4287] I use a `<link>` element with a uri attribute for the target URI and a rel attribute for to describe the kind of relationship. A well known relationship (such as `self` for a reference to the element itself) is bare, any specific to that server is a fully qualified URI. ATOM states that the definition for well-known `linkrels` is the [Registry of Link Relations]. As I write these are confined to what's done by ATOM, which is generally seen as a leader in level 3 restfulness.

From [Richardson Maturity Model]

# Authentification

Flow from [SalesForce API]:

1. Web server flow, where the server can securely protect the consumer secret.
2. User-agent flow, used by applications that cannot securely store the consumer secret.
3. Username-password flow, where the application has direct access to user credentials.
 
# Debugging

Debug long output with headers included.

```
curl -i -s -v https://api.github.com/users/serbanghita 2>&1 | less
```

Basic authentification.

```
curl -u "serbanghita" https://api.github.com
```

OAUTH2 authentification using headers

```
curl -H "Authorization: token OAUTH-TOKEN" https://api.github.com
```

POST-ing on a regular form

```
curl -X POST http://secure.avangate.com/cpanel/ -d email="test@test.com" -d password="123456" -d Login="Login"
```



[Architectural Styles and the Design of Network-based Software Architectures]:http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm
[Richardson Maturity Model]:http://martinfowler.com/articles/richardsonMaturityModel.html
[A Practical Approach to API Design]:https://leanpub.com/restful-api-design
[GitHub Enterprise API]:https://developer.github.com/enterprise/2.3/v3/
[What Every Developer should know about HTTP]:https://www.amazon.com/gp/product/B0076Z6VMI/ref=oh_aui_d_detailpage_o00_?ie=UTF8&psc=1
[Best practices for a pragmatic restful API]:http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api
[Atlassian REST API]:https://docs.atlassian.com/confluence/REST/latest/
[RFC 6570]:http://tools.ietf.org/html/rfc6570
[SalesForce API]:https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm
[SalesForce SObject API]:https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_get_field_values.htm
[RFC 4287]:https://tools.ietf.org/html/rfc4287#section-4.2.7
[Registry of Link Relations]:https://tools.ietf.org/html/rfc4287#section-7.1
