# Status

:warning: This repository contains historical information about the Server APIs Work Group.  This work is now being progressed in the [Server](https://forums.swift.org/c/development/server) category on the Swift Forums.  All interested parties are invited to participate on the forums.

## Server APIs Work Group

The Server APIs Work Group is responsible for steering the [Swift Server APIs](http://swift.org/server-apis/) project, which is an evolving set of Swift libraries developed as part of the Swift open source project to provide fundamental capabilities for building server-oriented software.

The work group consisting of a core team, stakeholders from the server-side Swift community, and anyone who wants to get involved. The work group consists of three roles: core team member, stakeholder and contributor. Participants may have more than one role in the work group.

Everyone is welcome to contribute to the Server APIs Work Group through participating in a range of activities including joining as a stakeholder, participating in design discussions, asking or answering questions on the mailing lists, reporting or triaging bugs or by submitting pull requests to the project(s) for implementation or tests.

### <a name="focus-areas"></a>Current Focus Areas
The work group is initially focussing on the creation of API proposals for base networking, security/encryption and HTTP parsing:

* **Base Networking**: Provide a portable interface for low level socket based network based I/O, including TCP/IP and UDP protocols, IPv4 and IPv6 support and domain name resolution. Support should be provided to create and use both synchronous and asynchronous non-blocking connections.

* **Security and Encryption**: Provide common cryptographic constants and cyphers along with keychain and certificate management, and SSL/TLS based secure transport. This must integrate with the base networking support to provide secure sockets, and with the HTTP parsing library to provide HTTPS support.

* **HTTP and WebSockets**: Provide low level HTTP parsing, including HTTP, HTTP/2 and WebSocket support making it possible, in conjunction with the security and networking APIs, to create secure HTTP and WebSocket servers.

### <a name="steering-team"></a>Steering Team
Analogous to the primary Core Team for Swift, the work group has a steering team that is responsible for providing overall technical direction, ensuring co-ordination both between the various API efforts (for example around Network, Security and HTTP integration for HTTPS) and with the wider Swift Core Libraries and language. Membership of the steering team is contribution based and is expected to evolve over time.

The initial steering team consists of:

* Chris Bailey ([@seabaylea](https://github.com/seabaylea), IBM Kitura)
* Logan Wright ([@LoganWright](https://github.com/LoganWright), Vapor)
* Paulo Faria  ([@paulofaria](https://github.com/paulofaria), Zewo)
* Steve Algernon ([@salgernon](https://github.com/salgernon), Apple)

### <a name="stakeholders"></a>Stakeholders
The work group also has stakeholders who represent server-side frameworks or applications. They are responsible for providing early input on use cases and API design as part of the iterative design and implementation process, and to adopt the new APIs into their frameworks.

Joining and leaving the work group as a stakeholder is a straightforward process. The only requirement is to raise a Pull Request to add or remove your name from the stakeholder list in this project, which will act to add or remove you from invites to formal work group discussions.

The initial stakeholders consists of (alphabetically):

* Ah Shone ([@tasktinkle](https://github.com/tasktinkle), Baidu)
* Alex Blewitt ([@alblue](https://github.com/alblue), Apple)
* Alfredo Delli Bovi ([@adellibovi](https://github.com/adellibovi))
* Andrew Dunn ([@Andrew-Dunn](https://github.com/Andrew-Dunn))
* Bas Broek ([@basthomas](https://github.com/basthomas))
* Ben Cohen ([@airspeedswift](http://github.com/airspeedswift), Apple)
* Billy Tobon ([@billyto](http://github.com/billyto), Rent the Runway)
* Carl Brown ([@carlbrown](http://github.com/carlbrown), IBM)
* Cătălin Stan ([@thecatalinstan](https://github.com/thecatalinstan), Criollo)
* Damian Kolakowski ([@glock45](https://github.com/glock45), Swifter & swiftx)
* Dan Appel ([@danappelxx](https://github.com/danappelxx), Zewo)
* Daniel Dunbar ([@ddunbar](https://github.com/ddunbar), Apple)
* Danielle Tomlinson ([@dantoml](https://github.com/dantoml), Jay & Other OSS)
* David Ask ([@davidask](https://github.com/davidask), Zewo)
* David Sperling ([@dsperling](https://github.com/dsperling), Smith Micro)
* Eleftherios Laskaridis ([@laskaridis](https://github.com/laskaridis), eTravel)
* Emanuel Guerrero ([@eman6576](https://github.com/eman6576))
* Farzad Nazifi ([@euwars](https://github.com/euwars), boon)
* Gelareh Taban ([@gtaban](https://github.com/gtaban), IBM)
* Gianluca Tranchedone ([@gtranchedone](https://github.com/gtranchedone))
* Gregor Milos ([@gmilos](https://github.com/gmilos), Apple)
* Gwynne Raskind ([@gwynne](https://github.com/gwynne))
* Ian Partridge ([@ianpartridge](https://github.com/ianpartridge), IBM)
* J. Morgan Lieberthal ([@baberthal](https://github.com/baberthal))
* Jack Lawrence ([@jackhl](https://github.com/jackhl), Apple)
* Jacopo Andrea Giola ([@JGiola](https://github.com/jgiola))
* Jason Toffaletti ([@toffaletti](https://github.com/toffaletti), Apple)
* Joannis Orlandos ([@joannis](https://github.com/joannis), OpenKitten)
* Johannes Weiß ([@weissi](https://github.com/weissi), Apple)
* John Lin ([@johnlinvc](https://github.com/johnlinvc))
* Jonathan Thornton ([@jonblatho](https://github.com/jonblatho), Loop Weather Services)
* Kelvin Çobanaj ([@kelvincobanaj](https://github.com/kelvincobanaj))
* Kuan Huang ([@widehuang](https://github.com/Widehuang), Baidu)
* Kyle Jessup ([@kjessup](https://github.com/kjessup), Perfect)
* Laurent Gaches([@lgaches](https://github.com/lgaches))
* Marcin Kliks ([@vi4m](https://github.com/vi4m), Zewo)
* Max Desiatov ([@explicitcall](https://github.com/explicitcall), Astrocat)
* Maxim Veksler ([@maximveksler](http://github.com/maximveksler), Sugar So What)
* Ludovic Dewailly ([@ldewailly](https://github.com/ldewailly), Apple)
* Luke Hiesterman ([@gravisman](https://github.com/gravisman), Apple)
* Marc Hoffman ([@dwarfland](https://github.com/dwarfland), RemObjects Software, Elements Compiler)
* Michael Chiu ([@michael-yuji](https://github.com/michael-yuji), SX0)
* Nic Jackson ([@nicholasjackson](https://github.com/nicholasjackson), notonthehighstreet.com)
* Patrick Bohrer ([@pbohrer](https://github.com/pbohrer), IBM)
* Phil J. Łaszkowicz ([@siilime](https://github.com/siilime), Omnijar Studio)
* Piers Mainwaring ([@piersadrian](https://github.com/piersadrian))
* Ricardo Borelli ([@rabc](https://github.com/rabc), Zewo)
* Rick Mann ([@jetforme](https://github.com/jetforme), Latency: Zero, LLC)
* Robert Dickerson ([@rfdickerson](https://github.com/rfdickerson), IBM Kitura)
* Robert Payne ([@robertjpayne](https://github.com/robertjpayne), Zewo)
* Ryan Collins ([@rymcol](https://github.com/rymcol))
* Sahand Nayebaziz ([@sahandnayebaziz](https://github.com/sahandnayebaziz), Hypertext)
* Sam Liu ([@ontouchstart](https://github.com/ontouchstart))
* Sasha Milic ([@SashaMilic](https://github.com/sashamilic), OpenRatio)
* Scott Lessans ([@slessans](https://github.com/slessans), Nourish Technology)
* Stevey Brown ([@Steveybrown](https://github.com/steveybrown))
* Tanner Nelson ([@tannernelson](https://github.com/tannernelson), Vapor)
* Thiago Holanda ([@unnamedd](https://github.com/unnamedd), Zewo)
* Thomas Catterall ([@swizzlr](https://github.com/swizzlr))
* Thomas Paul Mann ([@thomaspaulmann](https://github.com/thomaspaulmann), Swish)
* Tim Burks ([@timburks](https://github.com/timburks), Google)
* Tom Doron ([@tomerd](https://github.com/tomerd), Apple)
* Tripta Gupta ([@neurosaurus](https://github.com/neurosaurus), Capital One)
* Tyler Cloutier ([@cloutiertyler](https://github.com/cloutiertyler), Edge)
* Tyler Stromberg ([@AquaGeek](https://github.com/AquaGeek))
* Veck Hsiao ([@fbukevin](https://github.com/fbukevin), Sanity)
* Wassim Seifeddine  ([@wassimseif](https://github.com/wassimseif))
* Yuki Takei ([@noppoMan](https://github.com/noppoMan), Slimane)


### Additional Information
More information can be found in the [Server APIs pages](http://swift.org/server-apis/) of [swift.org](http://swift.org), or by posting to the [swift-server-dev](https://lists.swift.org/mailman/listinfo/swift-server-dev) mailing list.
