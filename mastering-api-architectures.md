# Mastering API Architecture

> This is based on book from Mastering API Architecture by James Gough, Daniel Bryant, and Matthew Auburn

This book is to people who want to build their career towards API development

- This book helps in Design, test and build API's
- Build API's in architecture prospective
- Deploy gateways and service mesh
- Identify vulnerabilities in API architecture and implement security

## API

> An API represents an abstraction of the underlying implementation and to effectively model the exchange of information.

An API is of Two Types based on API Invocation:

- In-Process (local to Application such as invocation of methods or objects from another class)
- Out of Process (data traversing across network, such as Local network, VPC or Internet)

<strong>NOTE</strong>: From the Analogy of Building Conference Application, A complete API request is a series of requests with In-Process and Out-of-Process API calls.

There are two types of components in controlling API traffic

- North-South traffic(controlled by API gateways)
- East-West traffic(handled by infrastructure components like Kubernetes and Service mesh)

#### Introduction to REST API's

> REST: REpresentational State Transfer is a set of architectural constraint, most commonly applied on HTTP as an underlying transport layer protocol([refer](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm))

- On a High-level, REST API stands for transfer of states between producer and consumer, where producer models the state and consumer can interact with it.
- Requests from Producer -> consumer are stateless, i.e producer doesn't know any information about previous request, where for chain of requests, client should sent any required information to the producer for processing.
- It's a layered system, abstracting the complexity of systems sitting behind the REST interface. as consumer should not know or care whether they are interacting with database or a service.

#### How REST API's Headers look like ?

```http
GET http://mastering-api.com/attendees
Accept: application/json
---
200 OK
Content-Type: application/json
{
    "displayName": "Jim",
    "id": 1
}
```

Here When a consumer request a Producer, it requests the with `GET` method and with `Accept: application/json` where Producer Respond with `Content-Type: application/json` and with status `200 OK`

> REST is straightforward a stateless meaning no client state is stored on the server. where client must pass context back to server on subsequent requests.

There are 4 levels with respect to Richardson’s maturity heuristics and their application to RESTful APIs

- Level 0 -> HTTP/ RPC `/attendees`
- Level 1 -> Resources `GET /attendees/1`
- Level 2 -> Verbs (Methods) `GET /attendees/1`, `DELETE ...`, `PUT ...`
- Level 3 -> Hypermedia Controls (Response from server include object, using which we can update or delete `Chatty Experience`)

#### Introduction to Remote Procedure Calls (RPC) APIs

> A Remote Procedure Call (RPC) involves calling a method in one process but having it execute code in another process.

- The Key difference between REST and RPC is state, REST by definition stateless whereas RPC state depends on the implementation.

### A Brief about GraphQL

(In layman terms, we can define GraphQL as a language used to query the target Producer graph using its QL and get only the desired result)

> GraphQL introduces a technology layer over existing services, datastores, and APIs that provides a query language to query across multiple sources. The query language allows the client to ask for exactly the fields required, including fields that span across multiple APIs.

The GraphQL schema provides the connection and extends the domain model, allowing the customer to specify exactly what is required on the consumer side. This works extremely well for modeling a user interface and also reporting systems or data warehousing–style systems.

GraphQL excels when a consumer requires uniform API access over a wide range of interconnected services.

[Open list of API Standards](https://github.com/masteringapi/rest-api-standards)

> We should not mention PII(Personal Identifiable Information) as part of URL, as they may be cached or stored in server logs.

#### HTTP Status Codes

| Status Code | Definition                            |
| ----------- | ------------------------------------- |
| 2XX         | Indicate Success Response             |
| 3XX         | Redirects, to access external sources |
| 4XX         | Client-Side Error with `message`      |
| 5XX         | Server-Side Failures                  |

#### Semantic Versioninig

A `major version` such as (`1`.5.2) introduces noncompatible changes with previous versions of the API. There is likely going to be a migration guide and tracking as consumers upgrade to the new API.

A `minor version` such as (1.`5`.2) introduces a backward compatible change with the previous version of the API.

A `patch version` such as (1.5.`2`)does not change or introduce new functionality but is used for bug fixes on an existing Major.Minor version of functionality.

> OpenAPI Specifications are an important part of an API program, and when combined with tooling, versioning, and lifecycle, they are invaluable.

#### Implementing RPC with gRPC

gRPC is more strict compared to REST OpenAPI, few cases are as follows

- Adding a new service or new method is backward compatible as is adding a field to a message, but care is required.
- Any field added must not be mandatory otherwise backward compatibility will break.
- Removing a field or renaming a field will break compatibility, as will changing the data type of a field.
- Changing the field number is also an issue as field numbers are used to identify fields on the wire.
- The restrictions of encoding with gRPC mean the definition must be very specific.
- Extra fields and ordering do not matter in OpenAPI, and therefore versioning and compatibility is even more important when it comes to gRPC

> gRPC cannot be queried directly from a browser without additional libraries, however you can install gRPC UI to use the browser for testing. grpcurl also provides a command-line tool

#### Modeling Exchanges and Choosing API Format

In the case of `High-Traffic Services` and `Large Exchange Payloads` we need to consider which API protocol to choose based on performance and API parsing and exchanges between services.

#### HTTP/2 Performance Benefits

In HTTP/2, Multiplexing allows us to perform all individual requests over a single HTTP/2 connection.

gRPC uses HTTP/2 by default and reduces the size of exchange by using a binary protocol.

> HTTP/3 is on the way and it will change everything. HTTP/3 uses QUIC, a transport protocol built on UDP.

On a whole, If bandwidth is a concern or cost, then gRPC will provide an advantage, in particular as content payloads increase significantly in size. gRPC may be beneficial compared to REST if payload bandwidth is a cumulative concern or the service exchanges large volumes of data. If large volumes of data exchanges are frequent, it is also worth considering some of the asynchronous capabilities of gRPC.

Additionally, gRPC is best for east-west exchanges and RESTful API is best for north-south exchanges and also it depends in few cases.

## Testing APIs

An API should not return anything that differs from what is documented.
