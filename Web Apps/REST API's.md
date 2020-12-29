# REST API's

<details>

<summary>Index</summary>

- [REST API's](#rest-apis)
  - [Introduction](#introduction)
    - [Guiding Principles of REST](#guiding-principles-of-rest)
    - [Resources](#resources)
  - [Open Api Specification](#open-api-specification)
  - [URL's](#urls)
    - [Best practices](#best-practices)
      - [Resources](#resources-1)
    - [Version](#version)
      - [Resources](#resources-2)
    - [Formats](#formats)
      - [Resources](#resources-3)
    - [URL Depth](#url-depth)
    - [Payload formats](#payload-formats)
      - [Resources](#resources-4)
    - [Good RESTful URL examples](#good-restful-url-examples)
      - [Resources](#resources-5)
    - [Bad RESTful URL examples](#bad-restful-url-examples)
      - [Resources](#resources-6)
  - [HTTP methods and status Codes](#http-methods-and-status-codes)
    - [HTTP Response principles](#http-response-principles)
      - [No values in keys](#no-values-in-keys)
      - [No internal-specific names](#no-internal-specific-names)
      - [Metadata should only contain direct properties of the response set, not properties of the members of the response set](#metadata-should-only-contain-direct-properties-of-the-response-set-not-properties-of-the-members-of-the-response-set)
      - [Use code status](#use-code-status)
        - [2xx - Success](#2xx---success)
        - [3xx - Redirect](#3xx---redirect)
        - [4xx - Client Error](#4xx---client-error)
        - [5xx - Server Error](#5xx---server-error)
      - [The response have to be standardized](#the-response-have-to-be-standardized)
        - [Success](#success)
          - [GET /posts.json](#get-postsjson)
          - [GET /posts/2.json](#get-posts2json)
          - [DELETE /posts/2.json](#delete-posts2json)
        - [Fail](#fail)
          - [POST /posts.json (with data body: "Trying to creating a blog p](#post-postsjson-with-data-body-trying-to-creating-a-blog-p)
        - [Error](#error)
          - [GET /posts.json](#get-postsjson-1)
      - [Resources](#resources-7)
    - [Examples of Methods and Responses](#examples-of-methods-and-responses)
      - [Resources](#resources-8)
  - [Version](#version-1)
    - [Resources](#resources-9)
  - [Batching results](#batching-results)
    - [Resources](#resources-10)
  - [Mock response](#mock-response)
    - [Example](#example)
    - [Resources](#resources-11)
  - [Security](#security)
    - [CORS](#cors)
      - [Resources](#resources-12)
  - [Management state with HATEOAS](#management-state-with-hateoas)
    - [Resources](#resources-13)
  - [Documentation](#documentation)
    - [Software to auto generate docs](#software-to-auto-generate-docs)
    - [Resources](#resources-14)

</details>

## Introduction

A REST API (also known as RESTful API) is an application programming interface that conforms to the constraints of REST architecture. REST stands for representational state transfer.

An API, or application programming interface, is a set of definitions and protocols for building and integrating application software.

REST is acronym for REpresentational State Transfer. It is architectural style for distributed hypermedia systems and was first presented by Roy Fielding in 2000 in his famous dissertation.

Like any other architectural style, REST also does have it’s own 6 guiding constraints which must be satisfied if an interface needs to be referred as RESTful. These principles are listed below.

### Guiding Principles of REST

1. **Client--server** -- By separating the user interface concerns from the data storage concerns, we improve the portability of the user interface across multiple platforms and improve scalability by simplifying the server components.
2. **Stateless** -- Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server. Session state is therefore kept entirely on the client.
3. **Cacheable** -- Cache constraints require that the data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable. If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests.
4. **Uniform interface** -- By applying the software engineering principle of generality to the component interface, the overall system architecture is simplified and the visibility of interactions is improved. In order to obtain a uniform interface, multiple architectural constraints are needed to guide the behavior of components. REST is defined by four interface constraints: identification of resources; manipulation of resources through representations; self-descriptive messages; and, hypermedia as the engine of application state.
5. **Layered system** -- The layered system style allows an architecture to be composed of hierarchical layers by constraining component behavior such that each component cannot "see" beyond the immediate layer with which they are interacting.
6. **Code on demand (optional)** -- REST allows client functionality to be extended by downloading and executing code in the form of applets or scripts. This simplifies clients by reducing the number of features required to be pre-implemented.

The key abstraction of information in REST is a resource. Any information that can be named can be a resource: a document or image, a temporal service, a collection of other resources, a non-virtual object (e.g. a person), and so on. REST uses a resource identifier to identify the particular resource involved in an interaction between components.

The state of the resource at any particular timestamp is known as resource representation. A representation consists of data, metadata describing the data and hypermedia links which can help the clients in transition to the next desired state.

### Resources

- [Red Hat](https://www.redhat.com/en/topics/api/what-is-a-rest-api)
- [Restfulapi](https://restfulapi.net/)

## [Open Api Specification](http://spec.openapis.org/oas/v3.0.3)

## URL's

### Best practices

- URLs should include nouns, not verbs.
- Use plural nouns only for consistency (no singular nouns).
- Use HTTP methods (HTTP/1.1) to operate on these resources:
- Use HTTP response status codes to represent the outcome of operations on resources.

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_RESTful_urls.html#use-restful-service-urls)

### Version

An API URL **may** contain a version number preceding.If not (anonymous version), then it **should** be understood that it always refers to the last vertsion but it **should not** be considere stable.

Example:
> GET /v1/path/to/resource HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_RESTful_urls.html#versioning)

### Formats

Allow users to request formats like JSON or XML, for example:

- <http://example.gov/api/v1/magazines.json>
- <http://example.gov/api/v1/magazines.xml>

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_RESTful_urls.html#formats)

### URL Depth

The structure of the URL endpoint **should be** like *resource/identifier/resource*. If the URL goes deeper thad that consider re structure your URL / API.

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_RESTful_urls.html#url-depth)

### Payload formats

The three patterns of payload format encoding most frequently found in the wild are:

        HTTP headers (e.g. Content-Type: and Accept:)
        GET parameters (e.g. &format=json)
        resource label (e.g. /foo.json)

This patters are week by themeself so use HTTP headers and Get parameters or resource labels

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_RESTful_urls.html#api-payload-formats)

### Good RESTFUL URL examples

List of magazines:

```
GET /api/v1/magazines.json HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

Filtering and sorting are server-side operations on resources:

```
GET /api/v1/magazines.json?year=2011&sort=desc HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

A single magazine in JSON format:

```
GET /api/v1/magazines/1234.json HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

All articles in (or belonging to) this magazine:

```
GET /api/v1/magazines/1234/articles.json HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

All articles in this magazine in XML format:

```
GET /api/v1/magazines/1234/articles.xml HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

Specify query parameters in a comma separated list:

```
GET /api/v1/magazines/1234.json?fields=title,subtitle,date HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

Add a new article to a particular magazine:

```
POST /api/v1/magazines/1234/articles.json HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_RESTful_urls.html#good-restful-url-examples)

### Bad RESTful URL examples

Non-plural noun:

```
GET /magazine HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

```
GET /magazine/1234 HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

Verb in URL:

```
GET /magazine/1234/create HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

Filter outside of query string:

```
GET /magazines/2011/desc HTTP/1.1
Host: www.example.gov.au
Accept: application/json, text/javascript

```

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_RESTful_urls.html#bad-restful-url-examples)

## HTTP methods and status Codes

Use the different HTTP methods help mantain clean and understable URL's, also methods and status code help consumers utilise your API.

### HTTP Response principles

#### No values in keys

  For example `{"125":"Environment"}` is bad, `{"id: "125","name": "Environment"}` is good.
  This is a problem because the key is supposed to be the name of the value. In the second example (good) the keys are descriptions of their coresponding values.

#### No internal-specific names

  For example the name "node"

#### Metadata should only contain direct properties of the response set, not properties of the members of the response set

    Author note:
    > what?

#### Use code status

  This increase the information given to the users without the need of added in the response data

  This is a list of common used response codes:

##### 2xx - Success

  | Response Code | Meaning | Explanation        |
  | ------------- | ------- | ------------------ |
  | 200           | Ok      | everything alright |
  | 201           | Created |                    |

##### 3xx - Redirect

  | Response Code | Meaning | Explanation |
  | ------------- | ------- | ----------- |

##### 4xx - Client Error

  | response Code | Meaning              | Explanation                                                                                                                                                                                                           |
  | ------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | 400           | Bad request          | the server could not understand the request and the client **should not** repeat it                                                                                                                                   |
  | 401           | Unauthorized         | The request need authentication                                                                                                                                                                                       |
  | 403           | Forbiden             | The server understood the request, but is refusing to fulfill it. Authorization will not help and the request SHOULD NOT be repeated                                                                                  |
  | 404           | Not Found            | The server has not found anything matching the Request-URI.                                                                                                                                                           |
  | 405           | Not Allowed          | The method specified in the Request-Line is not allowed for the resource identified by the Request-URI.                                                                                                               |
  | 422           | Unprocessable Entity | The server understand the request and the media type is correct, but an error but was unable to process the contained instructions. This is usefull for incorrect parameters or client didn't follow the requirements |

##### 5xx - Server Error

  | Response Code | Meaning               | Explanation                                                                                    |
  | ------------- | --------------------- | ---------------------------------------------------------------------------------------------- |
  | 500           | Internal Server Error | The server encountered an unexpected condition which prevented it from fulfilling the request. |

#### The response have to be standardized

Author notes:
> There are some standards for how an API has to send the response, personally i like JSend.

- **What?** - Put simply, JSend is a specification that lays down some rules for how [JSON](http://json.org/) responses from web servers should be formatted. JSend focuses on application-level (as opposed to protocol- or transport-level) messaging which makes it ideal for use in [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)-style applications and APIs.
- **Why?** - There are lots of web services out there providing JSON data, and each has its own way of formatting responses. Also, developers writing for JavaScript? front-ends continually re-invent the wheel on communicating data from their servers. While there are many common patterns for structuring this data, there is no consistency in things like naming or types of responses. Also, this helps promote happiness and unity between backend developers and frontend designers, as everyone can come to expect a common approach to interacting with one another.
- **Hold on now, aren't there already specs for this kind of thing?** - Well... no. While there are a few handy specifications for dealing with JSON data, most notably [Douglas Crockford](http://www.crockford.com/)'s [JSONRequest](http://www.json.org/JSONRequest.html) proposal, there's nothing to address the problems of general application-level messaging. More on this later.
- **(Why) Should I care?** - If you're a library or framework developer, this gives you a consistent format which your users are more likely to already be familiar with, which means they'll already know how to consume and interact with your code. If you're a web app developer, you won't have to think about how to structure the JSON data in your application, and you'll have existing reference implementations to get you up and running quickly.

A basic JSend-compliant response is as simple as this:

```JSON
  {
      status : "success",
      data : {
          "post" : {
            "id" : 1,
            "title" : "A blog post",
            "body" : "Some useful content" 
          }
      }
  }
```

When setting up a JSON API, you'll have all kinds of different types of calls and responses. JSend separates responses into some basic types, and defines required and optional keys for each type:

| Type    | Description                                                                                         | Required Keys   | Optional Keys |
| ------- | --------------------------------------------------------------------------------------------------- | --------------- | ------------- |
| success | All went well, and (usually) some data was returned.                                                | status, data    |               |
| fail    | There was a problem with the data submitted, or some pre-condition of the API call wasn't satisfied | status, data    |               |
| error   | An error occurred in processing the request, i.e. an exception was thrown                           | status, message | code, data    |

  Errors **should** be send in the response and they **should** be as descriptive and specific as possible. They also **should** include a message fot the end-user **whenever is possible**
  
##### Success

When an API call is successful, the JSend object is used as a simple envelope for the results, using the data key, as in the following:

###### GET /posts.json

```JSON
{
    status : "success",
    data : {
        "posts" : [
            { "id" : 1, "title" : "A blog post", "body" : "Some useful content" },
            { "id" : 2, "title" : "Another blog post", "body" : "More content" },
        ]
     }
```

###### GET /posts/2.json

```JSON
{
    status : "success",
    data : { "post" : { "id" : 2, "title" : "Another blog post", "body" : "More content" }}
}
```

###### DELETE /posts/2.json

```JSON
{
    status : "success",
    data : null
}
```

Required keys:

- status: Should always be set to "success".
- data: Acts as the wrapper for any data returned by the API call. If the call returns no data (as in the last example), data should be set to null.

##### Fail

When an API call is rejected due to invalid data or call conditions, the JSend object's data key contains an object explaining what went wrong, typically a hash of validation errors. For example:

###### POST /posts.json (with data body: "Trying to creating a blog p

```JSON
{
    "status" : "fail",
    "data" : { "title" : "A title is required" }
}
```

Required keys:

- status: Should always be set to "fail".
- data: Again, provides the wrapper for the details of why the request failed. If the reasons for failure correspond to POST values, the response object's keys SHOULD correspond to those POST values.

##### Error

When an API call fails due to an error on the server. For example:

###### GET /posts.json

```JSON
{
    "status" : "error",
    "message" : "Unable to communicate with database"
}
```

Required keys:

- status: Should always be set to "error".
- message: A meaningful, end-user-readable (or at the least log-worthy) message, explaining what went wrong.

Optional keys:

- code: A numeric code corresponding to the error, if applicable
- data: A generic container for any other information about the error, i.e. the conditions that caused the error, stack traces, etc.

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_HTTP_methods.html#http-response-principles)
- [List of response codes and explanation](https://www.restapitutorial.com/httpstatuscodes.html)
- [JSend](https://github.com/omniti-labs/jsend)

### Examples of Methods and Responses

Author Note:
> The examples below where edited to follow JSend standard.

`GET/magazines`

List all magazines contained within the /magazines resource

```JSON
GET /magazines HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

```

A response of "200 OK" indicating that the request has succeeded.

```JSON
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
    "status" : "success",
    "data" : { ... }
}

```

Status Codes:
| Status Code                                                                       | Meaning                                 |
| --------------------------------------------------------------------------------- | --------------------------------------- |
| [200 OK](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1)        | no error                                |
| [404 Not Found](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.5) | the "magazines" resource does not exist |

`POST/magazines`

Create new magazine within the /magazines resource

```JSON
POST /magazines HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

{
    "status" : "success",
    "data" : { ... }
}

```

A response of "201 Created" indicates that the request has been fulfilled.

The URI of the new resource is provided in the response

```JSON
HTTP/1.1 201 Created
Vary: Accept
Content-Type: text/javascript

{
    "status" : "success",
    "data" : { 
      "id: "1234",
     }
}

```

However, no effect if the resource already exists.

```JSON
HTTP/1.1 405 Method Not Allowed
Vary: Accept
Content-Type: text/javascript


{
    "status" : "error",
    "message" : "Unable to create a magazine with ID of 1234 because a magazine with that ID already exists",
    "code" : "444444",
    "info" : "http://api.example.gov/v1/documentation/errors/444444.html"
    "data" : {
      "error": "Unable to create duplicate magazine 1234",
    }
}

```

| Status Code                                                                                | Meaning                              |
| ------------------------------------------------------------------------------------------ | ------------------------------------ |
| [201 Created](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.2)            | magazine created                     |
| [405 Method Not Allowed](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.6) | unable to create "magazine" resource |

`PUT/magazines`

Replace all magazines in the /magazines resource with those in the request

```
PUT /magazines HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

[ ... ]

```

200 indicates that the request has succeeded.

```
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
    status : "success",
    data : { 
      "id: "1234",
     }
}

```

| Status Code                                                                | Meaning            |
| -------------------------------------------------------------------------- | ------------------ |
| [200 OK](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1) | magazines replaced |

`PUT/magazines/1234`

Replace the /magazines/1234 resource with the representation in the request

```JSON
PUT /magazines/1234 HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

{
    "status" : "success",
    "data" : { ... }
}

```

200 indicates that the request has succeeded.

```JSON
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
    "status" : "success",
    "data" : { 
      "id: "1234",
     }
}

```

| Status Code                                                                | Meaning                 |
| -------------------------------------------------------------------------- | ----------------------- |
| [200 OK](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1) | magazine 1234  replaced |

`DELETE/magazines`

Delete all magazines from the /magazines resource

```
DELETE /magazines HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

```

200 indicates that the request has succeeded.

```JSON
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
    "status" : "success",
    "data" : { 
      "id: "1234",
     }
}

```

| Status Code                                                                | Meaning               |
| -------------------------------------------------------------------------- | --------------------- |
| [200 OK](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1) | all magazines deleted |

`DELETE/magazines/1234`

Delete the magazine resource /magazines/1234

```JSON
DELETE /magazines/1234 HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

```

200 indicates that the request has succeeded.

```JSON
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

```

| Status Code                                                                | Meaning               |
| -------------------------------------------------------------------------- | --------------------- |
| [200 OK](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1) | magazine 1234 deleted |

`HEAD /magazines`

List metadata about the /magazines resource, such as last-modified-date.

```JSON
HEAD /magazines HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

```

200 indicates that the request has succeeded.

```JSON
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
    "status" : "success",
    "data" : { ... }
}

```

| Status Code                                                                | Meaning                  |
| -------------------------------------------------------------------------- | ------------------------ |
| [200 OK](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1) | magazines metadata found |

`HEAD /magazines/1234`

List metadata about /magazines/1234, such as last-modified-date.

```JSON
HEAD /magazines HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

```

200 indicates that the request has succeeded.

```JSON
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
    "status" : "success",
    "data" : { ... }
}

```

| Status Code                                                                | Meaning                            |
| -------------------------------------------------------------------------- | ---------------------------------- |
| [200 OK](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1) | metadata about magazine 1234 found |

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/use_HTTP_methods.html#examples)

## Version

Never release an API without a version number. Version should be intergers, not decimals numbers, prefix with 'v'.

Example:

- Good: v1, v2, v3
- Bad: v-1.1, v1.2, 1.3

Maintain API's at least one version back.

Author note:
> this doesn't have to do with the project / software release version, right?

### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/versioning.html#use-versions)

## Batching results

If no limit is specified, return results with a default limit.

To get records 51 through 75 do this:

```Text
  GET /magazines?limit=25&offset=50 HTTP/1.1
  Host: example.gov.au
  Accept: application/json, text/javascript

```

offset=50 means, 'skip the first 50 records'

limit=25 means, 'return a maximum of 25 records'

Information about record limits and total available count should also be included in the response. Example:

```JSON
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
  "metadata": {
    "resultset": {
      "count": 227,
      "offset": 25,
      "limit": 25
    }
  },
  "results": [...]
}

```

### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/batching_results.html#batching-results)

## Mock response

It's suggested that each resource accept a 'mock' parameter on the testing server. Passing this parameter should return a mock (example) data response (bypassing the back-end)

These methods would not result in an article being posted, it is only a simulation.

### Example

Example 1 - GET mock list of magazines

**Request mock list of magazines**

```
GET /api/v1/magazines.json?mock=True HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

```

**Response list of mock magazines**

```
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
  "metadata": {
    "resultset": {
      "count": 123,
      "offset": 0,
      "limit": 10
    }
  },
  "results": [
    {
      "id": "1234",
      "type": "magazine",
      "title": "Public Water Systems",
      "tags": [
        {"id": "125", "name": "Environment", "url": "http://api.example.gov.au/v1/tags/125"},
        {"id": "834", "name": "Water Quality"}
      ],
      "created": "1231621302"
    },
    {
      "id": 2351,
      "type": "magazine",
      "title": "Public Schools",
      "tags": [
        {"id": "125", "name": "Elementary"},
        {"id": "834", "name": "Charter Schools"}
      ],
      "created": "126251302"
    }
  ]
}

```

Example 2 - GET individual mock magazine

**Request mock magazine**

```
GET /api/v1/magazines/1234?format=json&mock=True HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

```

**Response mock magazine**

```
HTTP/1.1 200 OK
Vary: Accept
Content-Type: text/javascript

{
  "id": "1234",
  "type": "magazine",
  "title": "Public Water Systems",
  "tags": [
    {"id": "125", "name": "Environment"},
    {"id": "834", "name": "Water Quality"}
  ],
  "created": "1231621302"
}

```

Example 3 - POST article to mock magazine

**Post an article to mock magazine 1234**

```
POST /api/v1/magazines/1234/articles?mock=True HTTP/1.1
Host: example.gov.au
Accept: application/json, text/javascript

{
  "title": "Raising Revenue",
  "author_first_name": "Jane",
  "author_last_name": "Smith",
  "author_email": "jane.smith@example.gov",
  "date": "2014-06-22",
  "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ante ut augue..."
}

```

### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/mock.html#mock-behaviour)

## Security

### CORS

It is likely that many of your API consumers will want to mashup your API service with services from other agencies or private sector domains using purely client-side applications (for example, mobile apps or single page apps). Agencies should support this model by delivering Cross-Origin Resource Sharing (CORS) enabled services by default.

There’s a good description of CORS with examples from Mozilla under ‘Overview’

[CORS by Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

Granting JavaScript clients basic access to your resources simply requires adding one HTTP Response Header, namely:

```JSON
 Access-Control-Allow-Origin: *
 Access-Control-Allow-Origin: <http://example.com:8080>

```

The asterisk wild-card permits scripts hosted on any site to load your resources; listing a specific `<base URI>` will permit scripts hosted on the specified site -- and no others -- to load your resources.

This is compatible with both XHR `[XMLHttpRequest](http://www.w3.org/TR/XMLHttpRequest/)` and XDR `[XDomainRequest](http://msdn.microsoft.com/en-us/library/cc288060(VS.85).aspx)`, and is [supported by all the major Web browsers](http://www.w3.org/Security/wiki/Comparison_of_CORS_and_UM#CORS_2).

#### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/cors.html#support-cross-domain-mashups-with-cors)
- [W3 Wiki](https://www.w3.org/wiki/CORS_Enabled)

## Management state with HATEOAS

“Hypermedia As The Engine Of Application State” (HATEOAS) is a RESTful technique that can make consumer applications simpler and more robust. In many applications, the allowed actions on a resource depend on the state of that resource. Rather than require the consumer to understand and code for the allowed states, HATEOAS provides a means for the server to say what is allowed. The concept is best explained by example.

Consider a bank account number 12345 with a positive balance of $100. A REST query on that resource might return a response indicating that subsequent allowed actions are deposit, withdraw, or transfer:

```JSON
{
  "account_number”:”12345”’
  “balance”: 100.00,
  “links”:[
    {“rel”: "deposit",  “href”:"/account/12345/deposit"},
    {“rel”: "withdraw", “href":"/account/12345/withdraw"},
    {“rel”: "transfer", “href”:"/account/12345/transfer"}
  ]
}
```

But if the same account is overdrawn by $25 then the only allowed action is deposit:

```JSON
{
  "account_number”:”12345”’
  “balance”: -25.00,
  “links”:[
    {“rel”: "deposit",  “href”:"/account/12345/deposit"}
  ]
}
```

There is no universally accepted format for representing links between two resources in JSON. You may choose to adopt the above format, or you may decide to send links in HTTP response headers.

```JSON
HTTP/1.1 200 OK
...
Link: <10/employees>; rel="employees"
```

Both are absolutely valid solutions.

### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/hateos.html#management-state-with-hateoas)
- [Resful Api](https://restfulapi.net/hateoas/)

## Documentation

All APIs **must** include documentation targeted at the developer that will consume your API.

The best way to ensure that your API documentation is current and accurate is to embed it within your API implementation and then generate the documentation using literate programming techniques, or a framework such as <http://apidocjs.com/>, <http://swagger.io/>, or <http://raml.org/index.html>.

There are a number of sites offering guidance on providing high quality API documentation:

- <http://www.programmableweb.com/news/web-api-documentation-best-practices/2010/08/12>
- <http://bradfults.com/the-best-api-documentation/>

Some good examples of API documentation include:

- <https://dev.twitter.com/overview/documentation>
- <https://stripe.com/docs/api#charges>
- <https://www.twilio.com/docs/api/rest>

### Software to auto generate docs

- [Swagger](https://swagger.io/)
- [APIDOC](https://apidocjs.com/)
- [RAML](https://raml.org/index.html)
- [Sphinx](https://www.sphinx-doc.org/en/master/)
- [MkDocs](https://www.mkdocs.org/)

> Sphinx y MkDocs works with [Read the Docs](https://docs.readthedocs.io/en/stable/index.html)

### Resources

- [Api Guide](https://apiguide.readthedocs.io/en/latest/build_and_publish/documentation.html#document-your-api)
