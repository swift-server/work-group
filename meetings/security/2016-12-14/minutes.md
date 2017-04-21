# Swift Server APIs: Security stream meeting 1

### Initial Agenda:
* Current discussion status roundup
* Review of BlueSSLService, a layer on top of OpenSSL and macOS Secure Transport libraries:  BlueSSLService Review
* Next Steps

### Attendees:
* Chris Bailey
* David Sperling
* Gelareh Taban
* Alfredo Delli Bovi
* Bill Abt
* Alex Blewitt

# Minutes:

_Scope of the Security APIs:_  
* The scope of what's eventually intended is the full set of APIs, spanning across secure transport (SSL/TLS), crypto, and keychain/certificate management, etc
* The aim is also to provide a consistent set of APIs across both clients and servers, although not all APIs may be available in every case
* Which crypto depends on what’s available (and whether there are requirements above/beyond what we get from the macOS and/or OpenSSL/LibreSSL libs).

_Review of approach taken in BlueSSLService:_  
* BlueSSLService covers the "secure transport" part of the APIs. There's also a BlueCryptor library that covers crypto.
* It provides a service that adds onto an existing socket library conforming to a protocol. The only implementation of that is currently BlueSocket, but it could be easily modified to work with other socket implementations.
  * 6 protocol methods need to be implemented in the socket library.
  * A method in the SSL service to let you override the connection verification process to allow for specialized connection verification on an application basis. 
* The initial implementation of BlueSSLService uses OpenSSL on all platforms (including macOS), but was then modified to use SecureTransport on macOS.
  * The APIs are very different between OpenSSL and SecureTransport, and there was some struggle with the SecureTransport documentation.
  * OpenSSL provides much more flexibility for configuration. macOS/SecureTransport is limited to using pkcs#12, although there are internal APIs for dealing with other formats (such as PEM) that are not exposed.
  * Do we need support for PEM, etc? Probably - it’s much more prevalent in Linux/server use cases.
    * This might be because of usability, and only exposing what users need. With the addition of server use cases, this may need to change.
  * For Cipher suites, SecureTransport uses the hex IANA value to select cipher suites whereas OpenSSL lets you use text abbreviations (corresponding to the IANA values), as well as AND/OR logic.
* The result is that you get more capabilities on Linux from OpenSSL than you get on macOS from SecureTransport
* Additionally BlueSSLService doesn’t work on iOS because some of the SecureTransport APIs aren’t exposed.
  * But that's not a problem if these APIs aren't required there (ie. the user required function is provided by things like URLSession)

_Use of OpenSSL vs LibreSSL:_  
* OpenSSL is being used as it provides FIPS certification, whereas LibreSSL does not
  * There's a number of other forks of OpenSSL, but its not believed that any of the others is FIPS certified. Additionally most of the forks are subsets of the function.
  * Reusing OS libs also makes it easier to get FIPS certification as they are already certified on macOS and iOS and there is a certified version of OpenSSL available for Linux.

_Review of BlueCryptor for Crypto:_


* BlueCryptor attempts to do the same thing for Crypto, using CommonCrypto on iOS and macOS, and OpenSSL on Linux.
* In CommonCrypto, the function that is missing is RSA. Similar to the issue with other file formats in BlueSSLService, RSA is there in the library, but not exposed publicly.  In OpenSSL, RSA is available and the API is similar enough to the CommonCrypto API that it could be easily exposed in BlueCryptor as well.

_Keychain Services:_
* Nothing has yet been tried for keychain services. Keychain services is great on macOS/iOS, but there is no equivalent in Linux
* Linux just relies on certificates etc being present on the file system
* A lot of Linux servers, particularly Java based ones, use a CMS (Certificate Management System) to manage certificates and keys.  This is similar to the services provided by the Keychain API on Apple platforms.
* Further work is required to understand if we need to implement something here, or expect the user to deal with certificate management themselves (on a per-OS basis).

_Use of BlueSSLService and BlueCryptor as a prototype implementation:_  
* Should we use BlueSSLService and BlueCryptor as a prototype implementation, and use that to work on the API surface?
* This seems like a reasonable approach

### Next Steps:
* Discuss the implemented, but not exposed, function in SecureTransport and CommonCrypto with Luke Hiesterman
* Carry out more investigation on the need (if any) for common certificate/keychain management
* Start to build an outline proposal for the Security libraries for use as a Swift Evolution "pitch" 
