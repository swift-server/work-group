# HTTP stream meeting 2


### Initial Agenda:
* Review of draft HTTP API Pitch 
  * https://docs.google.com/document/d/1ErHA8RXLiTGvOPHNY0KtbWCvwR1IUz_2ffi7CxCUo_4/edit
* Discussion of key points:
  * Use of URLRequest/Response
  * Value Types vs. Reference Types

### Attendees:
* Chris Bailey
* Ben Cohen
* Carl Brown
* Stevey Brown
* Tony Parker
* Gregor Milos
* Shmuel Kallner
* Alex Blewitt
* Allen
* Chuck Goddard
* George
* Johannes Weiss
* Ludovic Dewailly
* Marcin Kliks
* Nasser Ebrahim
* Steve Algernon
* Michael Papp
* Thomas Catterall

### Minutes:

_Use of value types vs. reference types for request and response_ 
* General consensus is in favour of using a value types for request and response.
  * The argument that the should be references as they are passed around and mutated really don’t hold
  * It should be noted that the reason why there is still NSURLRequest/Response (reference types) was because a subclass exists, rather than the intend that they should be reference types.
  * The use of value types will help with reference cycles in closures (like middlewares) which you otherwise need to use weak self for.
  * Should also help with reducing some of the ARC overhead
* ARC overhead won’t necessarily be removed if the struct/value types has references inside it - and the body data is really a stream which has to be a reference type
  * In Foundation, request and response is just the headers, the body data is a side stream so they can be separated
  * This is done URLSession (as with downloadTask) into a file or a stream (and the same would be true for responses).
  * Can be thought of like sequence, which is a value type for which you can get an iterator which is a reference type
  * Separate experience from Johannes is creating a framework which has request/response separate from the body stream.
    * Request and response are value types
    * Handler provides a BodyProcessor which is called when chunks of data become available
    * This is especially important when the client is using Chunked transfer encoding, which some frameworks currently don’t attempt to handle.
* General consensus in separating the request and response headers (metadata) away from the body, which can be handled separately either by a handler API or a closure.
* How do we handle HTTP trailers if we separate headers and body stream?
  * Trailers are in the body stream and arrive after the headers are complete, but add to the headers
  * These aren’t well specified, and probably need to be handled by whatever is processing the stream anyway.

_Use of Foundation based types for request and response_ 
* It’s accepted that the Foundation types don’t match the requirements for general request and response types today as their designed for a specific set of use cases.
* We should figure out what the “right answer” should be for Swift (without regard to Objective-C compatibility), and then see how that fits into the existing types
  * There’s definitely scope to extend or modify the existing types
  * But we’d need a migration plan so that existing users aren’t broken

_Next Steps:_ 
* Update draft pitch with feedback
* Define the required contents for the request and response types
  * How should be store the header metadata itself?
  * Should data be fully processed eagerly or lazily?
  * How do we handle the various header parsing rules?
* Define approach to handling the body stream separately to the header metadata

