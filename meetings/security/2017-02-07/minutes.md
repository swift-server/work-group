
# Swift Server APIs: Security stream meeting 2

## Initial Agenda:
- Current discussion status roundup
- Review of draft pitch: https://github.com/swift-server/security/blob/master/README.md
- The API design
- API differences between platforms (if any)

If you have items you want to make sure are on the agenda, please add them below:

## Attendees:
- Gelareh Taban
- Joannis Orlandos
- Bill Abt
- Dave Sperling
- Logan Wright
- Chris Bailey
- Stevey Brown

## Minutes:

Scope of library:
- MongoKitten also does some of its own MD5 checksum hashing. It should really get this from a standard lib - so the “Server APIs” for security shouldn’t just limit itself to TLS but also crypto functionality. 
- The aim isn’t just to do TLS and implement APIs for “server specific” use cases - we need to solve the wider problem of having consistency for all security/crypto across Linux and Darwin platforms.
- *Decision:* Server Security APIs initially to cover TLS and crypto functionality, similar to OpenSSL.

LibreSSL vs OpenSSL:
- MongoKitten uses LibreSSL (from vapor) and using OpenSSL (elsewhere) can cause symbol conflicts during build. We need to consolidate on a single implementation.
- LibreSSL vs OpenSSL in Vapor: decision was based on following factors:
  - Issues where there’s two users of OpenSSL at the same time on Darwin. 
      - N/A since won’t be using OpenSSL on Darwin
  - Easier instructions for compiling the code in
      - N/A if link against library
  - Some chat/forum discussion that implied that LibreSSL doesn’t have all of the vulnerabilities that exist in OpenSSL. 
  - LibreSSL APIs seemed a little easier to work with for transport. LibreSSL was also faster (10x?) for crypto
- LibreSSL is a subset of OpenSSL functionality, and one that doesn’t have FIPS compliance. Is this an issue? Probably for long term “enterprise” usage, especially for government work.
- We want to have a layer over OpenSSL and SecureTransport/CommonCrypto, so switching OpenSSL <-> LibreSSL under the same API should be possible.
- *Decision:* Use OpenSSL on Linux

Dynamic vs static linking of OpenSSL:
- Compiling to vs. linking to the security library. 
- Vapor had some problems with determining location of library on different distros of Linux or macOS  which can be problematic during run. 
  - N/A for macOS or unsupported distros.
- *Decision:* 
  - In the short term, linking on both Linux and Darwin. 
  - In the longer term,  if security library becomes part of the Swift tool chain, we could potentially compile-in on Linux (removing the need for dependencies).

New requirement: Support blocking and non/blocking I/O

New requirement: API to be Swifty
- Need to define what a “Swifty” API is!!! Value types vs. Reference types, etc. String handling?

Missing functionality in underlying library
- What do we do where platforms don’t have equivalent crypto capabilities on all platforms? We shouldn’t provide just the lowest common denominator, we should make it possible to report capabilities. If Darwin platforms are lacking, we should work with Apple to add new cyphers if needed.
- ALPN APIs missing from Secure Transport APIs for TLS 1.2

Isolation from I/O protocol:
- Streams vs. sockets as input for SSL - being able to abstract the socket away so we’re just giving a stream of bytes would be ideal.
- Similar to SSLEngine which is basically just a “state machine” that handles encrypting / decrypting via passing in buffers. This way it is easy to hook this in for Sockets that are either blocking or non-blocking or either just in processing pipelines that have no notion of sockets at all.
- Example: Netty has an implementation of such an SSLEngine that uses OpenSSL under the hood (via BIO abstraction) and so provide a fast dropping replacement for the JDK implementation. 
  - https://github.com/netty/netty/blob/4.1/handler/src/main/java/io/netty/handler/ssl/ReferenceCountedOpenSslEngine.java
  - https://github.com/netty/netty-tcnative/blob/1.1.33/openssl-dynamic/src/main/java/org/apache/tomcat/jni/SSL.java
- *Decision:* add to requirements


