## Understanding URIs
1. Rule: Hyphens (-) should be used to improve readability
   - http://api.example.com/blogs/test-this
1. Rule: Underscores (_) should not be used in URIs
1. Rule: Forward slash separator (/) must be used to indicate a hierarchical relationship
1. Rule: Lowercase letter should be preferred in URI paths
   - correct: http://api.example.com/blogs/test-this
   - Incorrect: http://api.example.com/blogs/TEST-this
1. Rule: File extensions should not be included in URIs
   - http://api.example.com/blogs/test-this.json 

**A document resource is a singular concept that is akin to an object instance or database record.**
**A collection is a server-managed directory of resources.**

1. Rule: A singular noun should be used for document names
   - http://api.example.com/leagues/teams/trebuchet
1. Rule: A plural noun should be used for collection names
   - http://api.example.com/leagues/teams/trebuchet/players
1. Rule: A verb phrase should be used for controller names
   - http://api.example.com/students/morgan/register 

**Controller resources are like executable functions with parameters and return values; inputs and outputs.**
1. Rule: CRUD function names should not be used in URIs
   - Correct: DELETE /users/1234
   - Incorrect GET /deleteUser?id=1234
   - Incorrect: GET /deleteUser/1234
   - Incorrect: DELETE /deleteUser/1234
   - Incorrect: POST /users/1234/delete
1. Rule: The query component of a URI may be used to filter collections or stores
   - GET /users
   - GET /users?role=admin
1. Rule: The query component of a URI should be used to paginate collection or store results
   - GET /users?pageSize=25&pageStartIndex=50
1. Rule: The query component of a URI should be used to support partial responses
   - GET /users/morgan?fields=(firstName, birthDate)

## Common Statuses 
1. Rule: 201 (Created) must be used to indicate successful resource creation
1. Rule: 204 (No Content) should be used when the response body is intentionally empty
1. Rule: 400 (Bad Request) may be used to indicate nonspecific failure
1. Rule: 401 (Unauthorized) must be used when there is a problem with the clients credentials 
1. Rule: 403 (Forbidden) should be used to forbid access regardless of authorization state
1. Rule: 405 (Method Not Allowed) must be used when the HTTP method is not supported
1. Rule: 500 (Internal Server Error) should be used to indicate API malfunction


## MetaData Design
1. Rule: Last-Modified should be used in responses
1. Rule: Cache-Control, Expires, and Date response header should be used to encourage caching
   - You can take advantage of caching to reduce client-perceived latency, to increase reliability, and to reduce the load on an API’s servers.
   - Cache-Control: max-age=60, must-revalidate
   - Date: Tue, 15 Nov 2022 08:12:31 GMT
   - Expires: Thur, 01 Dec 2022 16:00:00 GMT
1. Rule: Expiration caching headers should be used with 200 (OK) responses and optionally on 4xx responses (Negative caching)
   - Set expiration caching headers in responses to successful GET and HEAD requests
1. Rule: Custom HTTP headers must not be used to change the behavior of HTTP methods
1. Rule: A consistent form should be used to represent errors/error responses
1. Rule: Schemas should be used to manage representational form versions 
