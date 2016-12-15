# HTTP stream meeting 1


### Initial Agenda:
* Current discussion status roundup
* Value Types vs. Reference Types
* Use of NSHTTPURLRequest/Response
* Experiences of adding HTTP/2 support to Node.js 

### Attendees:
* Chris Bailey
* Alex Blewitt
* Alfredo Delli Bovi 
* Ben Cohen 
* Michael Chiu 

### Minutes:

_C vs Swift Implementations:_

Some current implementations:  

| Framework | HTTP 1.x Parser | HTTP/2 Parser | Request Type | Response Type | Notes |
|-----------|-----------------|---------------|--------------|---------------|-------|
| Kitura    | c-http parser   | N/A           | Class        | Class         |       |
| Perfect   | c-http parser(1)| Swift parser  | Class        | Class         |(1) HTTP 1.x parser used to be pure Swift |
| Swifter   | Swift parser    | N/A           | Class        | Enum          |       |
| Vapor     | Swift parser    | N/A           | Class (2)    | Class (2)     |(2) Switched to classes from structs |
| Zewo      | c-http parser   | N/A           | Struct (3)   | Struct (3)    |(3) Class used for stream backed Body fields |
| spartanX  | Swift parser    | N/A           | Struct       | Struct        |       |

Notes:  
(1) Perfect originally implemented their own HTTP 1.x parser in Swift, but switched to using the c-http parse from Node.js  
(2) Vapor originally implemented HTTP request and response as structs, but switch to using classes  
(3) Zewo uses structs for HTTP request and response, however the Body field is an enum. Where the enum is a stream, it is backed by a class.  

_Let's assume we're going to re-use existing C libraries for HTTP 1.x and HTTP/2:_  
* When doing a new implementation of existing functionality the new implementation is inherently going to have more bugs, simply due to the lack of available time in the field and being "battle tested" (c.f. Apache Harmony vs existing Java Class Library code)
* There's also the additional effort to maintain and bug fix, and keep up with any new enhancements
* In terms of performance, the only scope for a Swift implementation to really exceed a C implementation is likely around inlining (across the Swift/C boundary) and any type conversions (ie, across the C/Swift API boundary).
* This allows us to concentrate efforts on developing the right Swift API - we can always subsequently go back and revisit the underlying implementation.

  **However...**  
* We have to make sure that the underlying C API does not influence the Swift API surface:
  * Things like memory management from C driving the design etc
  * We could potentially mitigate this by ensuring the API would also make sense if applied to a non-Swift implementation (eg. that from Vapor or Swifter) as a one-off verification.
* We should be more wary of non-battle tested C APIs. We should look to see how much usage the "nghttp2" library for HTTP/2 is getting to see if it falls into this category.
* Licensing issues were raised around using the c-http parser from Node.js as its MIT licensed code.
  * There are no legal issues preventing the use of MIT licensed code in Apache 2 projects, and its already done elsewhere in Swift (libkqueue for example). We should follow up with the Core team to understand if there's any issues.


_Value types vs Reference Types:_  
* We should probably use the term “semantics” rather than types, because behaviors and types are separate.
* There's a strong desire to reuse the Foundation types, so we should focus in the short term in making sure that they are right. 
* Foundation was originally reference only, and we’ve started to add value semantics, but this is not complete in all cases. Rather than looking at where Foundation is right now, we should look at what types they should eventually be.
  * Really we need there to be a conversation between Ben and Tony Parker/Philippe Hausler to determine the direction for the Foundation types.
* Currently we believe that, in general, value semantics make sense, with the use of `inout` for middlewares, but there is the question around the mixing of reference and value semantics (ie, a struct wrapping a stream as a reference type).
  * Building a map/flow diagram of how a request is handled and used by middlewares will help to model the interactions with requests/responses, and show better what semantics should be used.

_Experiences of adding HTTP/2 support to Node.js_  
* Significant progress has been made in Node.js to adopt the `nghttp2` library
* Presentation from James Snell at Node Interactive is online:  
  https://www.youtube.com/watch?v=7uNGKCao8gA&t=1157s&list=PLfMzBWSH11xYaaHMalNKqcEurBH8LstB8&index=19


### Next steps:
* Include Tony Parker and Philippe Hausler in a discussion on the direction for request/response types in Foundation
* Discuss the use of MIT licensed code with the Swift Core Team
* Build a flow diagram for request handling and the use of middlewares
* Start to build an outline proposal for the HTTP parsing library for use as a Swift Evolution "pitch"
