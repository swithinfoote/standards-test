#  Introduction

The Strategy for a Digital Public Service is "a call to action for the
public service to operate in the digital world in a more modern and
efficient way --- delivering the outcomes that Aotearoa New Zealand
needs."

It envisions a future where agencies prioritise the creation of open
Application Programming Interfaces (APIs) to enable reuse of data,
transactions and rules, which, in turn, creates an opportunity for
greater cooperation and interoperability between agencies to
dramatically improve service design and delivery.

Agencies need focused guidance, approaches and techniques to help
increase their knowledge and skills around APIs. There is a wide range
in the level of knowledge and skill regarding API design and delivery
across government agencies. Hence this document tries to offer a balance
of guidance for those new to APIs along with quick lookup standards,
which should assist agencies in achieving consistency and commonality in
their API deliverables.

1.  []{#_heading=h.36ei31r .anchor}**Scope**

This document set aims to provide a set of high-level standards with
design and implementation guidance, along with low-level API best
practices to guide government agencies in their development of APIs.

-   **Part A -- API Concepts and Management 2021\
    **Looks at the business context for APIs within government and
    articulates the principles and considerations that could impact an
    agency when creating APIs. It looks at APIs in the context of their
    impact on the organisation as well as across government and public
    services through to commercial innovation. Version 1.0 published in
    2016 was called API Standard and Guidelines - Part A -- Business.

-   **Part B -- API Security 2021\
    **Part B contains the API Security reference architecture and
    technical details for implementing API Security. Version 1.0
    published in 2016 was called API Standard and Guidelines - Part A --
    Technical but has been split into a Part B - Security and Part C --
    Development for this version 2.0.

-   **Part C -- Development\
    **Part C (This document) contains the technical details for API
    Development, including general API implementation standards for API
    developers & consuming application developers. Version 1.0 published
    in 2016 was called API Standard and Guidelines - Part A -- Technical
    but has been split into a Part B - Security and Part C --
    Development for this version 2.0.

The guidance in this document set is intended to apply for all API
standards and protocols, however much of the guidance is oriented to
REST APIs.

Applicable technical standards are referenced throughout the document
set and are intended to provide detailed guidance for developers of API
standards.

Examples presented in this document are purely illustrative examples and
do not represent recommended API design and/or data content requirements
for NZ Government.

The document will use hypothetical or actual use cases with a government
context to illustrate practical application of the concepts described.

1.  []{#_heading=h.45jfvxd .anchor}**Target Audience**

The target audience for this document -- Part C Development - is
primarily solution designers and API developers within, or contracted
to, agencies and organisations within the public service.

Additionally, compliance and assurance personnel may be interested, as
well, in terms of assessing alignment with the standards and guidelines.

2.  []{#_heading=h.2koq656 .anchor}**Definition of API**

APIs and associated examples in this document are primarily ***Web
APIs*** or APIs that are accessible via the http(s) protocol. There are
some notable exceptions such as asynchronous APIs. An API however should
not be confused with a service. It is true that web services are, by
definition, APIs however not all APIs are web services. An API is an
interface that enables one application to communicate with another
application, but the communication protocol is agnostic.

It is important to stress that for the purposes of this document we are
discussing web APIs that enable interoperability and not software
engineering principles.

# API Design and Development

This section looks at APIs from a development perspective and offers the
guidelines and standards required to support government agencies in
designing, developing and governing APIs. The intended audience for this
section of the document are ***technical*** for example developers,
architects or API designers.

When reading this document consider the implications on you as an
agency. Fundamentally, APIs should make interoperability with your
agency a simple, but more importantly a consistent process.

This section will cover areas of key consideration such as good API
design, correct use of the http protocol, version control and various
technical standards.

## API Artefacts

There are some fundamental artefacts which comprise an API deliverable:

-   Interface specification, accessible via some form of catalogue

-   API code and policies

-   Tests

-   Service Level Agreement (SLA) for the API, identifying performance,
    availability etc.

These artefacts are the responsibility of the API developer and should
be mandated as a minimum set of deliverables when developing an API. All
of these artefacts must be managed in a source code management system
(SCM) so that changes can be tracked and collaborative development can
be performed.

## API Design

Application developers will invest heavily in using your API. They will
invest in learning the design and behaviour of your API, in developing
and testing around your API and may even invest in developing an entire
business model on your API.

Good API designs will attract more developers. Conversely, bad API
designs will drive away developers and drive up costs -- support costs,
maintenance costs and operating costs.

### When is an API appropriate?

In the past, the default reaction to a requirement for capability has
been to develop a web application. This is now gravitating towards APIs
as the default. So, when is it better to build an API than a web
application? Below are some situations where an API may be more
appropriate:

-   When commercial organisations or NGOs are screen scraping data from
    the agency's website

-   When the agency holds a single authoritative source of the truth

-   Where there is a need for (near real time) information exchange with
    a partner agency

-   When parts of a business process are (or may be) outsourced

-   When the agency's service can be included as part of a larger
    business process

-   When an agency needs internal systems to interact with cloud-based
    COTS solutions (SaaS)

-   Where businesses require easy access to (public) information

-   Where commercial organisations want to build capability into their
    own applications which will benefit the public (mobile/web apps)

-   When an agency expects other parties to act as agents or
    intermediaries for their services

-   When an agency expects to support service delivery across multiple
    channels

### Types of API

There are several different types of API and the type you choose may
depend on the technical use cases that you apply to both consumption and
provision of your API.


| API Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Usage                                                                                                                                                                                                                                                  |
|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **REST**    | Representational State Transfer (REST) is the most common and well understood API type. REST should be considered an architectural style for developing distributed hypermedia systems. There is a wealth of information and tooling to support the definition and creation of REST APIs. Typically, a REST API will have a well-defined and strongly typed schema definition (OpenAPI) where strict compliance can be achieved.                                    | Creating distributed system where a set of API resources are well defined. If medium latency resource creation or modification (POST, PUT, DELETE) is required then typically a REST API is a better fit. Typically used for synchronous interactions. |
|             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                        |
| **GraphQL** | GraphQL is an open source query and manipulation language developed by Facebook primarily designed to empower API consumers to consume only the data that they require. A common criticism of REST is that only the entire resource is available for consumption, sometimes referred to as “over fetching”, however with GraphQL the client decides the data that it requires. GraphQL also has a strongly typed schema (GraphQL Schema Definition Language – SDL). | An API that has a widely distributed client set with a variety of data requirements. Particularly well suited to high read (GET) clients                                                                                                               |
|             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                        |
**Asynchronous APIs**|AsyncAPI is an open source initiative to create an event-driven and asynchronous API standardization and development tooling. The AsyncAPI specification, inspired by the OpenAPI specification, describes and documents event-driven APIs in a machine-readable format.|Creating distributed systems where a set of API resources are well defined. Typically used for asynchronous interactions and event driven architectures. Also, useful when developing APIs that front workflows or long running orchestrations.|
| | | |
|**gRPC**|gRPC is a modern open source high performance Remote Procedure Call (RPC) framework that can run in any environment. |Creating distributed systems that require highly performant and scalable API's. gRPC makes use of binary data rather than just text which makes the communication more compact and more efficient. |In gRPC, a client application can directly call a method on a server application on a different machine as if it were a local object, making it easier for you to create distributed applications and services. This is enabled by a formal Interface Definition Language (IDL). gRPC utilizes Protocol Buffers by default, you can make it work with other data formats, such as JSON. |

Example Technical Use Case Synchronous/Asynchronous API

The illustrative example below demonstrates a combination of a
synchronous API and an asynchronous API.

```plantuml
@startuml

title "Example Use Case - Synchronous/Asyncronous Claims API"

actor "Customer" as C
actor "Service\nProvider" as P
entity "Service Provider\nSystem" as SPS
entity "Notification Endpoint" as NE
control "Claims API" as CA
entity "Agency Core System" as ACS
!pragma teoz true
==Register==
SPS -[#Pink]> CA : POST /register
note right of SPS
    This call is to enable the service provider
    to register their notification endpoint. Note
    that this is illustrative only. In reality most
    consumers will register with an agency using a
    developer portal or equivalent and create client
    application credentials with registered notification
    endpoint(s).
end note

CA -[#Pink]> SPS : Return registraiotn details
==Create Claim==
{start} C -[#Blue]> P : Access funded product\nor service
P -[#Blue]> SPS : Create claim details
SPS -[#Green]> CA : Register claim
CA -[#Pink]> ACS : Create claim
ACS -[#Pink]> ACS : Create claim and\nassign to workflow
ACS -[#Pink]> CA : Return claim identifier and status
CA -[#Green]> SPS : Return claim id and status
SPS -[#Blue]> P
{end} P -[#Blue]> C
{start} <-> {end} : Synchronous
==Subscribe to events==
SPS -[#Green]> CA : SUB claims/{claimId}
==Receive Updates==
{asstart} C -[hidden]-> P
ACS -[#Pink]> ACS : Workflow udate
ACS -[#Green]x CA : PUB claims/{claimId}
CA -[#Green]> SPS : Receive subscription message
alt Web Hook
    CA -[#Green]> NE : Send hook notification
    NE -[#Pink]> SPS : Forward notification
end
SPS -[#Pink]> P : Notify
{asend} P -[#Blue]> C : Notify
{asstart} <-> {asend} : Asynchronous

legend
    |= Color |= Type |= Description |
    | <size:11><back:#Green>           </back></size>|    <&arrow-right> | API Interaction |
    | <size:11><back:#Blue>           </back></size>|    <&arrow-right> | Human Interaction |
    | <size:11><back:#Pink>           </back></size>|    <&arrow-right> | System Interaction |
endlegend

@enduml
```

![](media/image7.png){width="5.901388888888889in"
height="7.579166666666667in"}

[]{#_heading=h.2ce457m .anchor}*Figure 48: Asynchronous Claims API*

The example above has 2 associated API specifications. The first is an
OpenAPI specification that describes the "Create Claim" and "Get Claim"
RESTful interactions and the second is an AsyncAPI specification that
describes the "Receive Updates" interaction. These example
specifications have been provided in the appendix of this document for
reference -- see [[Synchronous/Asynchronous Example
Specifications]{.underline}](#_heading=h.2vor4mt)

### API Design Principles

This section assumes that API Principles defined in section 4 of Part A
of this standard have already been read.

#### Future-Focused Design 

APIs should not be tightly coupled to legacy applications, exposing
whatever capabilities the legacy system offered. Nor should they be
designed to work in the way the legacy system currently works.

Instead they should be consumer driven -- so built to expose the
resources that consumers need, whether those resources are in legacy
systems or new. There should not be a drive to expose an entire product
via the API, or wait for the perfect backend system to be available.
Just offer as much as is practically useful, then evolve it to meet
needs. Design the API interface to be abstracted from the backend, so
that backend systems can be changed or replaced over time without
needing to change the interface.

The aim is to be future-focused (whilst still pragmatic) and develop
APIs to meet future needs. A good example of being future focussed is
building APIs to support HATEOAS (Hypermedia as the Engine of
Application State). This is where an API, in response to a consuming
application\'s request, is programmed to return hyperlinks (URLs) which
indicate the options for subsequent actions or information. See
[[section 2.7.7]{.underline}](#hateoas) for more details on HATEOAS.

#### Layering

When designing and developing an API it is important to consider that an
API is made up of distinct functional layers:

-   Security

-   Caching

-   Representation

##### Security

Every API will have a security component. It is important to recognise
that this is not only authentication and authorisation for access to an
API, it also includes threat protection (DDoS, SQL Injection, Cross site
scripting etc.) as well as availability and quality of service (QoS).
When designing and developing APIs it is often cost effective to create
a common framework that handles security for all APIs. See the
associated document, Part B, API Security, for more details.

##### Caching

Caching can dramatically improve the performance of an API. When
designing APIs consider what, when and where to cache. Understanding how
data is changed and how often it is changed is an important
consideration, as well as which layer it is most appropriate to cache
at. A common caching strategy should be developed for APIs that would
benefit from it. See [[section 2.12]{.underline}](#caching) for more
details.

##### Representation

When designing and developing an API it is important to consider the
representation of that API. This commonly includes an interface
specification that fully describes the API. To ensure the success of an
API it should be easy to consume driving a well-considered
representation layer.

![C:\\Users\\Josie\\AppData\\Local\\Microsoft\\Windows\\INetCache\\Content.Word\\API
Layers.png](media/image13.png){width="3.0104166666666665in"
height="4.6875in"}

[]{#_heading=h.2jxsxqh .anchor}*Figure 49: API Layering*

#### Standards-Based

Web standards have rapidly become powerful agreements, which span not
just local regions but are internationally accepted and enable
commonality and consistency. Using standard HTTP and URLs, the core
technologies of the web, along with standards such as JSON and OAuth
ensures that agencies are not creating bespoke or proprietary
technologies.

Hence the principle is to build to the latest versions of existing open
and accepted standards e.g. 

-   HTTP

-   OpenAPI

-   AsyncAPI

-   REST

-   JSON

-   OAuth

-   OIDC

Refer to the [[appendix]{.underline}](#_heading=h.3hej1je) for detailed
information about relevant standards.

### Designing an API

When designing an API, it is important to perform business process
analysis to ensure that API development is business-driven rather than
technology-driven. Technology driven projects rarely meet customers'
needs in the long run, so it important to gain background in who could
be using the API, for what. As mentioned previously, co-design is
fundamental to driving the right API development. To help identify
potential partners to involve in the co-design, consider:

-   processes which currently depend on information the API could expose

-   processes which require a capability an API could expose

Some actors will be human (e.g. application developers) whilst some
actors will be the systems which will interact with, or depend on, the
API. There may be different types of actors, some public sector, some
commercial entities, some public.

When representatives for the potential actors are identified, start
co-designing with these representatives. First and foremost, consider
the requirements for the API. Application developers often couch their
requirements in terms of how the API should work, rather than what the
API needs to do. Don't get bogged down in the variety of proposed
solutions from each developer: focus on extracting their true
requirements by performing functional analysis (e.g. use cases) and data
flow analysis. Then identify resources and work out the granularity
needed (see sections [[2.2.4 Designing an
API]{.underline}](#designing-an-api) & [[2.2.7
Granularity]{.underline}](#granularity)).

It is especially important that security and information privacy impacts
are identified up front and addressed early on in the design process.
Assess the information being passed and the types of access different
customers and/or consuming applications should have to the API. This
will help drive development of security policies alongside the design of
the API.

One common pitfall in API design is to map all existing data tables onto
resources and develop the associated CRUD capabilities into an API.
Usually this results in a poor API design and tightly couples the API
design to the underlying data structure. Another common pitfall is to
design APIs as an extension to, or way into, monolithic legacy systems.
This should be avoided as it tightly couples the API to the legacy
system. Both of these pitfalls will create issues for both provider and
consumers in the long term.

At this point in the design process, agility is probably more important
than completeness. Share early design thoughts and interface
specifications with the developer community and quickly make changes in
response to their feedback. Work through some sequence diagrams with
them to help pin down API interactions and inform API design thinking.

The correct API design will likely not please every developer, so don't
try to be all things to all developers. A rule of thumb is that you are
probably on the right track if most developers are a *little* unhappy,
but all are able to achieve their aims with the proposed design.

It is important not to try to bypass evolution steps and try to build
for all potential use cases right from the offset. For a more measured
progression towards API delivery, start simple and focus on a single
channel or interaction initially. By building onto these simple building
blocks, API evolution over time naturally progress towards omnichannel
applications. 

### Design Considerations

The following considerations emerge when looking to develop APIs in the
public sector:

-   Understand your data, understand your consumers. Before starting
    work on APIs, gain a good understanding of what data you hold, the
    complexity of that data, its relationships to other data, the
    downstream dependents on that data and potential consumers of the
    data. It is also a good idea to understand your consumers\' drivers
    and downstream usage or customers. 

-   Design for REST. If the interaction appears RESTful then develop a
    REST API, e.g. one-to-many. In some cases however, a gRPC or GraphQL
    API may be appropriate and are supported by this document. REST APIs
    are widely understood, easier to govern and suitable for most
    interoperability use cases. It is also important to note here that
    if there is an appropriate supported standard such as Fast Health
    Interoperability Resource (FHIR) then the resources defined in that
    standard should be used rather than a set of agency defined
    resources.

-   The information supplied via an API may still be dependent on
    overnight batch processes for update. It is worth making the
    information's timeliness and update period clear to potential
    consumers of the API.

-   APIs should not be used to handle large batch transfers because of
    the atomic nature of the usage i.e. if one single data write fails
    then the whole batch fails. APIs work better for multiple individual
    update transactions.

### Design Driven Development

**[Required]{.smallcaps}**

When building APIs, a Design Driven Approach must be taken.

This includes:

-   Interface specification first

-   Iterative approach

-   Continuous integration/testing

#### Interface Specification First

The best way to design an API is in collaboration with potential
consumers of that API. Creating the interface specification first makes
it easier for application developers to see what the API is going to
offer and how it could be used. Their early feedback will ensure that
the API design is heading on the right track and will be usable and
appropriate to their needs. Using a simple modelling language to define
the interface specification makes it easy to view and edit API
definitions. See [[section 2.2.8]{.underline}](#interface-specification)
for more information about defining interface specifications.

#### Iterative Approach

It has been acknowledged that big bang releases rarely deliver business
or customer benefit. An iterative approach, with ongoing releases
offering gradual improvement or evolving capability, gives a finer tuned
delivery, better sense of momentum, illustrates progress and enables
third parties to coordinate efforts with API developments. ICT.govt.nz
Accelerate
([[https://www.ict.govt.nz/guidance-and-resources/accelerate/]{.underline}](https://www.ict.govt.nz/guidance-and-resources/accelerate/))
offers a framework which supports this kind of development and has
guidance on how to deliver transformational projects.

An iterative approach incorporates continuous improvement, which
recognises the need to support continuing evolvement of the API beyond
the first delivery. The API is a product whose capabilities should
undergo continuing improvements based on consumer feedback, performance
analytics and emerging needs. This aligns to Phase 6 in the Accelerate
framework.

#### Automation First

Automation provides a quick turnaround for informing API developers
about breaking changes being submitted by developers who are all working
on the same code base or product (e.g. API). The idea is that all
developers submit code changes as often as possible (e.g. into a version
control system), allowing code to go through an automated, integrated
build process which ensures that nothing has broken the build. This
build process could happen many times a day. Any errors are quickly
identified and alerted to the team who can rectify them in a timely
fashion.

Tests can be written against the interface specification quite early on
in the development process by developing just enough API code to enable
the test to be run (stubs). The tests can then be incorporated into the
automated build process, giving early warning of regression test
failures. API code should not be able to progress through SDLC
environments until successful test execution.

### Granularity

There is a question as to how fine-grained an API resource should
be. APIs should be designed at the lowest practical level of granularity
because this makes each service simpler and allows them to be combined
in ways that suit the application developer. The key principle is to
design services that can be re-used and combined in different ways, and
not tie the application developer to a specific way of working or
sequence of API consumption just because that is how it is configured or
built in the back end.

If an API offers very fine-grained resources, then consuming
applications end up having to make many more calls to the API in order
to collect all the information they need, resulting in chattier
communications. On the other hand, if the API is based on very coarse
grained resources (returning everything about the resource) the response
payloads could end up being enormous, may not support all API
application developers' needs, and the API could become cumbersome to
use and maintain.

There may also be a need for varying granularity within one API,
depending on the purpose and use of that API. For example, if a blogging
API was being created, it may make sense to offer a coarse grained
resource for posting a new blog entry as a bundle of content including
pictures, sound, keywords as well as the textual blog entry. But when
offering the ability to like or comment on a blog entry it would make
sense, for clarity and ease of use, to offer these as separate
sub-resources, one for indicating a \'like\' and one for submitting a
comment.  

It is important to aim for a granularity which will prevent business
logic from leaking into the API e.g. requiring API calls to be made in a
certain sequence to meet with internal business processes. With the
blogging example, consider the impact of a fine-grained API being
offered for posting blog entries, with separate calls for adding images,
sounds and metadata. If metadata is mandatory, then the API application
developer needs to ensure that every blog post call is followed by a
metadata call. This puts the onus on the application developer to get
the sequence of calls correct and could lead to inconsistent data if
they do not adhere to the rules. It also leads to close coupling between
the consuming application and the API, and if the business logic changes
in the future there is a downstream impact on all application
developers, requiring them to modify their applications.

General guidelines are:

-   Don\'t aim for the finest granularity - an API should be built
    around each discrete and updateable resource

-   There does not need to be a one-to-one mapping between a manual
    service and a corresponding API; APIs should support the process but
    not try to encapsulate the process

-   A rough guide is to have one API operation for each entity lifecycle
    state transition

-   Resources can be identified by reviewing a business process and
    identifying the key entities which underpin the process. Any
    entities which the organisation manages or maintains throughout its
    full lifecycle will be potential API resources. There is typically
    one API operation for each entity lifecycle state transition.

-   There should be only one API function for one business outcome (e.g.
    change an address)

-   Consider using query parameters in URLs for different granularity of
    resources. For example, /passengers.json could return a list of
    names, whilst /passengers.json?detail=full could return detailed
    information about each passenger in a list.

### Interface Specification

An API represents a contract between the provider and the consumer for
access to provider resources. Because API consumption is a programmatic
exercise, it is important to have a clear definition of what the API
offers and how those API resources are to be accessed. This definition
is the interface specification. 

The interface specification should be designed in advance of developing
the API, as the act of working out the specification often helps think
through all the issues that could impact the design of the underlying
resource-handling code. It also helps consuming application developers
to review the capabilities being offered to see if the capabilities meet
their needs before they start developing to the specification. When
outsourcing API development, the interface specification can be written
in abstract as a means of defining the API the vendor should build. The
specification can be handled as a separate entity, is version
controllable, and it should be possible to use it as the main API
documentation or reference.  

There are several API modelling languages available for defining the
interface specification. Some are proprietary (e.g. RAML, API Blueprint)
whilst others are machine-readable but not human readable (e.g. WADL).
The most commonly used API modelling language today is an open standard
known as the OpenAPI Specification (formerly Swagger) maintained by the
Open API Initiative. This initiative is supported by many of the main
commercial entities in IT (Google, IBM, Microsoft, Atlassian, Paypal
etc.). It offers a standard, programming language-agnostic (JSON/YAML)
interface to REST APIs which allows both humans and computers to
discover and understand the capabilities of the service. For an example
of a Swagger interface specification see Appendix C - Example Interface
Specification.

It is important to use a modelling language to define the API interface
specification as essentially it is text or code and can be maintained
using source code management systems.

**[Recommended]{.smallcaps}**

Use [[OpenAPI/Swagger]{.underline}](https://openapis.org/) as the
interface specification language for all APIs being developed.

### Orchestration

As a general rule using APIs as an orchestration tool is not
recommended. This is due to the complexity that this can introduce to an
API architecture. That said, however, simple orchestration may in some
cases be appropriate. An example of this may be a mashup API that
creates a new logical API resource by combining related data held in two
or more back end systems.

A mashup is not appropriate when you create an API that merges two
distinct API products together. If a consumer requires this
functionality the mashup should be performed by the consuming
application.

Other examples of simple orchestration could include mediation such as
message transformation (JSON to XML or canonical message model
transformation).

### Software Development Kits (SDK)

**[Recommended]{.smallcaps}**

It is recommended that API Providers offer an SDK to developers of
consuming applications.

An SDK can be considered the implementation toolset for use of an
agency's APIs. By providing developers with an SDK they can build
applications faster without having to understand all of the API's
complexities. An SDK should provide sample code that explains the
functionality of your API to potential application developers.

An example of a public service API SDK can be found at the [[US
Department of Labour GitHub
repository](http://usdepartmentoflabor.github.io/Ruby-Sample-App/)]{.underline}
Publication/Catalogue

Once an API is in sufficient state to be offered to API consumers, the
API definition should be published to an API catalogue. The primary API
discoverer is the developer, so an external API must be well documented,
and provide accurate and up-to-date guidance via the catalogue.

Government are considering options for a central point of discovery for
externally accessible public sector APIs.

**[Recommended]{.smallcaps}**

Publishing to a catalogue is recommended for internal APIs.

**[Required]{.smallcaps}**

Publishing to a catalogue is required for external APIs.

## Architectural and Deployment Patterns

The table below identifies some architectural and deployment patterns
that bear further investigation. There are a number of vendor specific
references that are also available however this document does not
recommend any particular one.

+------------------------------+---------------------------------------+
| Pattern                      | Reference                             |
+==============================+=======================================+
| Microservices                | [[https://martinfowler                |
|                              | .com/microservices/]{.underline}](htt |
|                              | ps://martinfowler.com/microservices/) |
+------------------------------+---------------------------------------+
| API Management               | [[https://nordicapis.com/under        |
|                              | standing-api-management-api-gateway-a |
|                              | nd-api-manager/]{.underline}](https:/ |
|                              | /nordicapis.com/understanding-api-man |
|                              | agement-api-gateway-and-api-manager/) |
+------------------------------+---------------------------------------+
| Observability                | [[http                                |
|                              | s://martinfowler.com/articles/domain- |
|                              | oriented-observability.html]{.underli |
|                              | ne}](https://martinfowler.com/article |
|                              | s/domain-oriented-observability.html) |
|                              |                                       |
|                              | [[https://www.oreilly                 |
|                              | .com/library/view/distributed-systems |
|                              | -observability/9781492033431/ch04.htm |
|                              | l]{.underline}](https://www.oreilly.c |
|                              | om/library/view/distributed-systems-o |
|                              | bservability/9781492033431/ch04.html) |
+------------------------------+---------------------------------------+
| API Publication / Discovery  | [[https://apievangelis                |
|                              | t.com/2021/02/11/gathering-my-thought |
|                              | s-on-api-discovery/]{.underline}](htt |
|                              | ps://apievangelist.com/2021/02/11/gat |
|                              | hering-my-thoughts-on-api-discovery/) |
+------------------------------+---------------------------------------+
| Hybrid Deployments           | [[                                    |
|                              | https://nordicapis.com/making-sense-o |
|                              | f-a-multi-cloud-api-approach/]{.under |
|                              | line}](https://nordicapis.com/making- |
|                              | sense-of-a-multi-cloud-api-approach/) |
+------------------------------+---------------------------------------+
| Service Mesh                 | [[https://n                           |
|                              | ordicapis.com/introduction-to-service |
|                              | -mesh/]{.underline}](https://nordicap |
|                              | is.com/introduction-to-service-mesh/) |
|                              |                                       |
|                              | [[https://www.oreilly.com/libr        |
|                              | ary/view/the-enterprise-path/97814920 |
|                              | 41795/ch01.html]{.underline}](https:/ |
|                              | /www.oreilly.com/library/view/the-ent |
|                              | erprise-path/9781492041795/ch01.html) |
+------------------------------+---------------------------------------+

[]{#_heading=h.1a346fx .anchor}*Table 20: Architectural and Deployment
Patterns*

## HTTP Verbs

Access to REST APIs must be via the standard HTTP verbs: GET, PUT, POST,
DELETE in line with the [[W3C
Standard]{.underline}](https://www.w3.org/2001/tag/doc/whenToUseGet.html)
namely:

+-------------+--------------------------------------------------------+
| **Verb**    | **Common Usage**                                       |
+=============+========================================================+
| GET         | For retrieval of information                           |
|             |                                                        |
|             | If the interaction is more like a question (i.e. it is |
|             | a safe operation such as a query)                      |
+-------------+--------------------------------------------------------+
| POST        | To create a piece of information or resource item      |
|             |                                                        |
|             | To spawn an action                                     |
|             |                                                        |
|             | If the interaction is like placing an order            |
|             |                                                        |
|             | If the interaction changes the state of the resource   |
|             | in a way that the user would perceive (e.g. a          |
|             | subscription to a service)                             |
|             |                                                        |
|             | If the user be held accountable for the results of the |
|             | interaction                                            |
+-------------+--------------------------------------------------------+
| PUT         | To update an existing resource item                    |
|             |                                                        |
|             | To replace an existing resource item                   |
+-------------+--------------------------------------------------------+
| DELETE      | To delete a resource item                              |
+-------------+--------------------------------------------------------+
| OPTIONS     | To retrieve information about what the consumer is     |
|             | allowed to do with the resource                        |
+-------------+--------------------------------------------------------+
| PATCH       | Not recommended due to complexity                      |
+-------------+--------------------------------------------------------+
| HEAD        | Rarely used, but used to retrieve metadata about a     |
|             | resource                                               |
+-------------+--------------------------------------------------------+

[]{#_heading=h.2981zbj .anchor}Table 22: HTTP Verbs

## URI Construction

URI construction is important in that it is the door through which
consumers enter to obtain agency resources. It should be intuitive and
easy to guess what an endpoint does just by looking at the URI and HTTP
verb, without needing to see a query string. As basic guidance, endpoint
URLs should advertise resources, and avoid verbs.

In some situations an implemented standard may define the URI structure
for you. A good example of this is Fast Health Interoperability
Resources (FHIR)
[[https://www.hl7.org/fhir/resource.html]{.underline}](https://www.hl7.org/fhir/resource.html)

### API Offering

**[Recommended]{.smallcaps}**

Is it recommended that agencies make it clear in the URL that their
offering is an API:

**Example**

> https://**api**.example.govt.nz

### Version

APIs should have a clear indication of the version, so that application
developers can ensure they are using the appropriate version for their
consuming application.

**[Recommended]{.smallcaps}**

Header-based versioning is recommended (see section [[2.10, API Version
Control]{.underline}](#api-version-control)); however, it is recognised
that some API infrastructure does not readily support header-based
versioning. 

URL-based versioning is a viable alternative, as the version number in
the URL should only change when major revisions have been made and the
interface has changed substantially without backwards compatibility. For
URL-based versioning the URI should include /vN with the major version
(N) and v as a prefix. Agencies should not include minor version numbers
when using version numbers in the API paths.

**Template**

> /v{version}/ 

**Example**

> #Get details for provider id 123435 -- version 1 of the API
>
> GET https://api.example.govt.nz/v1/providers/12345
>
> Accept: application/json
>
> Host: api.example.govt.nz
>
> #Get details for provider id 123435 -- version 2 of the API
>
> GET https://api.example.govt.nz/v2/providers/12345
>
> Accept: application/json
>
> Host: api.example.govt.nz

### Namespaces

For APIs where an agency holds multiple responsibilities which may
result in overlapping resource naming (for example MBIE could have the
resource \"accommodation\" in two contexts: tenancy/contracts,
tourism/contracts) it is recommended that namespaces be used to avoid
any ambiguity. The namespace would be the first noun in the URI and
should reflect the function of government being offered by this API.
Namespaces may be singular or plural, depending on the situation. 

**Template**

> /{version}/{namespace}/

**Example**

> /v1/biosecurity/

### Resources and Sub-resources

**[Recommended]{.smallcaps}**

Resource names should be noun-based, and collection resource names
should be plural nouns, e.g. /passengers in lower case. Resource naming
should be short, simple and clearly understandable. It should also be
human-guessable, avoiding technical or specialist terms where possible.

Sub-resources must appear under the resource they relate to, but should
go no more than three deep i.e.
/resource/id/sub-resource/id/sub-sub-resource. If you reach a third
level of granularity (sub-sub-resource), it may be worth reviewing your
resource construction to see if it is actually a combination of multiple
first or second level resources.

The URI references for resources should consistently use the same path
structure to refer to resources. Sub-namespace or sub-folders should be
avoided, to maintain path consistency. This allows application
developers to have a predictable experience in case they are building
URIs in code.

** Template**

> /{version}/{namespace}/{resource}/{resource-id}/{sub-resource}/{sub-resource-id}
>
> /{version}/{resource}/{resource-id}/{sub-resource}/{sub-resource-id}

**Example**

> https://api.example.govt.nz/v2/biosecurity/trusted-travellers/33245/arrivals/P100782
>
> https://api.example.govt.nz/v2/learners/43265/achievements/7281

### Word Separation

Hyphens have traditionally been used as word separators in URLs, as
search engines (particularly Google) prefer a hyphen to split words
because a hyphen is not a word character (as defined in regular
expression language). This has led to hyphens, or kebab-case, being the
de facto standard in the interests of readability and Search Engine
Optimization (SEO).

Therefore, in order to keep URLs consistently formatted, path and query
string parameters should be lower case with hyphen separators for
multiword names.

**Example**

> https://api.example.govt.nz/v1/example-service/search?sort-order=asc

### Query Arguments

Query arguments should be used to filter a response i.e. modify a
returning result set. 

The general rule is:

-   If it changes the behaviour of the result set then it should be a
    query argument 

-   If it changes the behaviour of the API then it should be in the path

Query arguments are generally used for:

-   Sorting or ordering the result set - e.g. sort-order=ascending

-   Pagination - pagination is a query argument because it effectively
    acts as a filter and limits the result set returned. This is
    particularly useful with large response data sets. When using
    pagination it is a good idea to inform the consumer where they can
    find previous and subsequent result sets using hypermedia as
    discussed in [[section 2.7.7]{.underline}](#hateoas) of this
    document.

**Example**

> \"\_links\": \[
>
> {
>
> \"rel\": \"next\",
>
> \"href\":
> \"https://api.example.govt.nz/v1/example-service/search?limit=5&start=5\"
>
> },
>
> {
>
> \"rel\": \"prev\",
>
> \"href\":
> \"https://api.example.govt.nz/v1/example-service/search?limit=5&start=0\"
>
> },
>
> {
>
> \"rel\": \"self\",
>
> \"href\": \"http://api.example.govt.nz/v1/example-service/search\"
>
> }
>
> \]

-   Limiting the result set - e.g. by specifying which fields to return.
    This approach can be complicated and is often a decision based on
    functionality vs complexity. For example, it may be desirable to be
    able to filter a result set to a specific set of objects. Whilst
    this is possible, it is not a recommended approach. If this kind of
    flexibility is required in an API it could be a good time to
    consider the use of [Open Data Protocol
    (OData](http://www.odata.org/)).

-   In cases where response filtering is used, providers should ensure
    that they use a JSON schema by default so that consumers have the
    ability to understand the entire resource and do not need to query
    the resource for the message structure.

**Example**

> #Get a filtered result set for a learner
>
> GET
> https://api.example.govt.nz/v2/learners/33245?fields=firstName,lastName,dateOfBirth
>
> {
>
> \"firstName\": \"Mary\",
>
> \"lastName\": \"Contrary\",
>
> \"dateOfBirth\": \"12-01-1974\",
>
> \"\_links\": \[
>
> {
>
> \"rel\": \"self\",
>
> \"href\":
> \"https://api.example.govt.nz/v2/learners/33245?fields=firstName,lastName,dateOfBirth\"
>
> }
>
> \]
>
> }

## HTTP Headers

### Request Headers

+--------------+------------------+--------+--------+--------+--------+
| Header       | Usage            | GET    | POST   | PUT    | DELETE |
+==============+==================+========+========+========+========+
| Accept       | Indicates        | Re     | Re     | Re     | N/A    |
|              | desired format   | quired | quired | quired |        |
|              | of the response  |        |        |        |        |
|              |                  |        |        |        |        |
|              | If set to a      |        |        |        |        |
|              | value that       |        |        |        |        |
|              | cannot be        |        |        |        |        |
|              | supported by the |        |        |        |        |
|              | server, API      |        |        |        |        |
|              | responds with    |        |        |        |        |
|              | 406 (not         |        |        |        |        |
|              | acceptable)      |        |        |        |        |
+--------------+------------------+--------+--------+--------+--------+
| Content-Type | Indicates the    | N/A    | Re     | Re     | N/A    |
|              | format of the    |        | quired | quired |        |
|              | payload provided |        |        |        |        |
|              | on the request   |        |        |        |        |
|              |                  |        |        |        |        |
|              | If not supported |        |        |        |        |
|              | by the server,   |        |        |        |        |
|              | API responds     |        |        |        |        |
|              | with             |        |        |        |        |
|              | 415 (Unsupported |        |        |        |        |
|              | Media Type)      |        |        |        |        |
+--------------+------------------+--------+--------+--------+--------+
| A            | To provide       | Req    | Req    | Req    | Req    |
| uthorization | authorization    | uired, | uired, | uired, | uired, |
|              | information --   | unless | unless | unless | unless |
|              | type and token,  | a      | a      | a      | a      |
|              | depending on     | public | public | public | public |
|              | authorization    | API    | API    | API    | API    |
|              | type             |        |        |        |        |
|              |                  |        |        |        |        |
|              | If token is not  |        |        |        |        |
|              | valid for the    |        |        |        |        |
|              | request, API     |        |        |        |        |
|              | responds with    |        |        |        |        |
|              | 401              |        |        |        |        |
|              | (Unauthorized)   |        |        |        |        |
+--------------+------------------+--------+--------+--------+--------+
| Acc          | Advertises what  | Should | Should | Should | N/A    |
| ept-Encoding | compression      | use    | use,   | use,   |        |
|              | algorithm the    |        | if     | if     |        |
|              | consuming        |        | re     | re     |        |
|              | application is   |        | sponse | sponse |        |
|              | able to          |        | body   | body   |        |
|              | understand       |        | ex     | ex     |        |
|              |                  |        | pected | pected |        |
|              | If encoding not  |        |        |        |        |
|              | supported by the |        |        |        |        |
|              | server, API      |        |        |        |        |
|              | responds with    |        |        |        |        |
|              | uncompressed     |        |        |        |        |
|              | response         |        |        |        |        |
+--------------+------------------+--------+--------+--------+--------+
| {API Key     | Send the API     | Req    | Req    | Req    | Req    |
| Header}      | Keys with every  | uired, | uired, | uired, | uired, |
|              | request          | if     | if     | if     | if     |
| Note: there  |                  | issued | issued | issued | issued |
| is no set    | If keys are not  |        |        |        |        |
| naming       | valid, API       |        |        |        |        |
| standard for | response with    |        |        |        |        |
| an API Key   | 401 (Not         |        |        |        |        |
| Header       | authorised)      |        |        |        |        |
+--------------+------------------+--------+--------+--------+--------+
| If_Modi      | Makes the        | Should | N/A    | N/A    | N/A    |
| fied_Since/I | request          | use    |        |        |        |
| f-None-Match | conditional; the |        |        |        |        |
|              | server will      |        |        |        |        |
|              | respond with the |        |        |        |        |
|              | resource only if |        |        |        |        |
|              | the specified    |        |        |        |        |
|              | condition is     |        |        |        |        |
|              | met.             |        |        |        |        |
|              |                  |        |        |        |        |
|              | If condition is  |        |        |        |        |
|              | not met, API     |        |        |        |        |
|              | responds with    |        |        |        |        |
|              | 304 (Not         |        |        |        |        |
|              | Modified)        |        |        |        |        |
+--------------+------------------+--------+--------+--------+--------+
| {Request     | Unique           | Should | Should | Should | Should |
| tracking     | identifier that  | use    | use    | use    | use    |
| Headers}     | can be used to   |        |        |        |        |
|              | trace a request  |        |        |        |        |
| Note: there  | throughout its   |        |        |        |        |
| is no set    | lifecycle        |        |        |        |        |
| naming       |                  |        |        |        |        |
| standard for |                  |        |        |        |        |
| a            |                  |        |        |        |        |
| transaction  |                  |        |        |        |        |
| ID header    |                  |        |        |        |        |
+--------------+------------------+--------+--------+--------+--------+

[]{#_heading=h.302dr9l .anchor}*Table 22: Request Headers*

### Response Headers

  ------------------------------------------------------------------------------------
  Response Headers   Usage                 GET        POST        PUT         DELETE
  ------------------ --------------------- ---------- ----------- ----------- --------
  Content-Type       Indicates the format  Required   Required,   Required,   N/A
                     type of the response             if response if response 
                                                      body        body        
                                                      returned    returned    

  Location           Indicates the         Required   Should use, N/A         N/A
                     absolute URI of the   for 302    if resource             
                     newly created         redirect   created                 
                     resource item                                            

  Content-Location   Indicates the         Should use Should use, Should use  N/A
                     absolute URI of the              if resource             
                     requested resource               returned                

  Cache-Control      Directives to control Should use Should use  Should use  N/A
                     caching behaviour                                        
                     external to the API                                      
                     layer (e.g. CDN                                          
                     caching)                                                 

  Expires            Used in conjunction   Should use Should use  Should use  N/A
                     with Cache-Control                                       
                     for backwards                                            
                     compatibility                                            

  ETag               Concurrency control   Should use Should use  Should use  Should
                     header                                                   use
  ------------------------------------------------------------------------------------

[]{#_heading=h.2eclud0 .anchor}*Table 23: Response Headers*

### Customer X-HTTP Headers

X- notation headers have been deprecated as per
[[RFC6648]{.underline}](https://tools.ietf.org/html/rfc6648)[^1] and
should not be used. This standard appreciates that X- notation headers
are widely used however this document recommends that where an agency is
defining a custom header the X- notation should not be used and the
agency defines a custom header notation that is relevant. For example,
*X-Request-Id* should be redefined as *Request-Id*.

## Returned Content

The returned content is the body of the message that the API returns in
response to a request. This usually relates to the resource that was
requested.

### Resource Scope

The amount of data to return about a resource depends on several
factors:

-   Business context - does all the resource information being returned
    have relevance to the business process or activity consumers will
    use it for?

-   Payload size and network efficiency - how much information does the
    resource contain, and is it so bulky it could impact network
    performance?

-   Usefulness - is the information in the returned content always
    useful to the consumer, or is it something they may need once but
    never again?

Analysis of the full resource data against these factors should help
determine how much resource data is returned in the response.

### Formats

REST responses should be of a format which is both human and machine
readable. Even if your initial consumer is via B2B, the API should be
designed, where possible, for all potential consumers. REST APIs should,
by default, return content in JSON format. But it is good practice to
support multiple message formats (e.g. XML, Multi-part MIME) and allow
consuming applications to request the format they wish to consume (in
line with the \"Design for the Consumer\" principle in Part A, section
4).

The response format required from a GET request must be indicated by the
consumer in their request using the Accept header. For example:

> #GET a resource and specify the response type
>
> https://api.example.govt.nz/crown-property/0219c539-5885-4ab6-a55b-b0de7537c426
>
> Accept: application/xml
>
> #Response
>
> \<?xml version=\"1.0\" encoding=\"UTF-8\" ?\>
>
> \<CrownProperyResponseBody
> xmlns=\"https://api.example.com/CrownProperyResponse\"\>
>
> \<id\>0219c539-5885-4ab6-a55b-b0de7537c426\</id\>
>
> \<category\>commercial\</category\>
>
> \<location\>
>
> \<streetName\>Northbound Boulevard\</streetName\>
>
> \<town\>Wellington\</town\>
>
> \<postalCode\>6011\</postalCode\>
>
> \<countryCode\>NZ\</countryCode\>
>
> \</location\>
>
> \<pricing\>
>
> \<rentFrequency\>annual\</rentFrequency\>
>
> \<currencyCode\>NZD\</currencyCode\>
>
> \<pricePerUnitArea\>
>
> \<price\>1000\</price\>
>
> \<units\>squareMetre\</units\>
>
> \</pricePerUnitArea\>
>
> \<transactionType\>rent\</transactionType\>
>
> \</pricing\>
>
> \<property_type\>office\</property_type\>
>
> \<areas\>
>
> \<internal\>
>
> \<minimum\>
>
> \<value\>183\</value\>
>
> \<units\>squareMetre\</units\>
>
> \</minimum\>
>
> \<maximum\>
>
> \<value\>188\</value\>
>
> \<units\>squareMetre\</units\>
>
> \</maximum\>
>
> \</internal\>
>
> \</areas\>
>
> \<detailedDescription\>
>
> \<text\>Free text describing the property in some way.\</text\>
>
> \</detailedDescription\>
>
> \<tenancy\>
>
> \<life_cycle_status\>tennanted\</life_cycle_status\>
>
> \<nextReviewDate\>2016-06-01\</nextReviewDate\>
>
> \</tenancy\>
>
> \</CrownProperyResponseBody\>

The request format for a request containing a request body (POST, PUT,
PATCH) must be supplied in the Content-Type request header. For example:

> #PUT (update) a resource
>
> https://api.example.govt.nz/crown-property
>
> Content-Type: application/json
>
> Accept: application/json
>
> #Request BODY
>
> {
>
> \"id\": \"0219c539-5885-4ab6-a55b-b0de7537c426\",
>
> \"category\": \"commercial\",
>
> \"location\": {
>
> \"streetName\": \"Northbound Boulevard\",
>
> \"town\": \"Wellington\",
>
> \"postalCode\": \"6011\",
>
> \"countryCode\": \"NZ\"
>
> },
>
> \"pricing\": {
>
> \"rentFrequency\": \"annual\",
>
> \"currencyCode\": \"NZD\",
>
> \"pricePerUnitArea\": {
>
> \"price\": 1000,
>
> \"units\": \"squareMetre\"
>
> },
>
> \"transactionType\": \"rent\"
>
> },
>
> \"property_type\": \"office\",
>
> \"areas\": {
>
> \"internal\": {
>
> \"minimum\": {
>
> \"value\": 183,
>
> \"units\": \"squareMetre\"
>
> },
>
> \"maximum\": {
>
> \"value\": 188,
>
> \"units\": \"squareMetre\"
>
> }
>
> }
>
> },
>
> \"detailedDescription\": \[
>
> {
>
> \"text\": \"Free text describing the property in some way.\"
>
> }
>
> \],
>
> \"tenancy\": {
>
> \"life_cycle_status\": \"vacant\",
>
> \"nextReviewDate\": \"2016-07-01\"
>
> }
>
> }

For a good example of this in action, see the tabbed format options for
presenting patient information on the FHIR[^2] site.

Where JSON format is used in responses, it must conform to the JSON
Standard
([[RFC7159]{.underline}](https://tools.ietf.org/html/rfc7159)[^3]). In
line with this standard, textual content should be UTF-8 encoded by
default, and any deviations from this must be limited.

It is inadvisable to use APIs for returning binary data such as images
in the response content; hyperlinks to images are the preferred returned
response. But where images *are* returned, ensure that the image
encoding is MIME, HTTP Multipart.

HTML is allowed, but is less flexible for consumer usage (e.g. how can
it be consumed by a native mobile app?), ties content to presentation
and loses its benefits when building a single page application. It also
reduces the ability to filter the content in transit for consumers who
have fine grained control on what they can access. However, it may be
necessary for some forms of API e.g. APIs with geospatial content.

Avoid using bespoke formats in returned content.

**[Recommended]{.smallcaps}**

Returned content format should be JSON by default.

**[Required]{.smallcaps}**

Requests for a specific return format must be defined in the Accept
header.

### Layout

Responses should be a JSON object (not an array) by default. Using an
array to return results limits the ability to include metadata about
results and limits the API\'s ability to add additional top-level
properties in the future. Don\'t use unpredictable properties. Parsing a
JSON response where properties are unpredictable (e.g. derived from
data) is difficult, and adds friction for clients.

**Example of good layout**

> {
>
> \"response_metadata\": {
>
> \"item1\": \"value1\",
>
> \"item2\": \"value2\"
>
> },
>
> \"responseArray\": \[
>
> {
>
> \"name\": \"entity1\",
>
> \"type\": \"good\"
>
> },
>
> {
>
> \"name\": \"entity2\",
>
> \"type\": \"good\"
>
> }
>
> \]
>
> }

**Example of bad layout**

> \[
>
> {
>
> \"name\": \"entity1\",
>
> \"type\": \"bad\"
>
> },
>
> {
>
> \"name\": \"entity2\",
>
> \"type\": \"bad\"
>
> }
>
> \]

### JSON Property Names

Within content, property names should conform to the following
guidelines:

-   Property names should be meaningful names with defined semantics

-   Property names must be camel-case ASCII strings

-   The first character must be a letter or underscore (\_)

-   Subsequent characters can be a letter, a digit, or underscore

-   Reserved JavaScript keywords should be avoided

### Consistency

Preserve backwards compatibility with existing consumers of the API by
returning expected fields and employing sensible default values for
missing fields. Keep consistency of terminology throughout, so that the
consumer is not misled. Avoid modifying the semantics of content to new
meanings, e.g. don't change a \'title\' field from meaning the title of
the page, to meaning the prefix for a name to the person's job title.

### Singletons vs. Collections

Some API GET calls will return a single resource item (e.g. GET
https://api.example.govt.nz/passengers/12345) whereas some calls will
return a collection of resource items (e.g. GET
https://api.example.govt.nz/passengers), and the handling and error
treatment can be different.

A single item will generally consist of all the pertinent fundamental
details about the resource, and the GET will return these fundamental
details.

**Example**

> #GET a single passenger resource by ID
>
> GET <https://api.example.govt.nz/passengers/12345>
>
> Accept: application/json,version=1.\*
>
> {
>
> "id": 12345,
>
> "names": {
>
> "firstName": "John",
>
> "middleName": "Howard",
>
> "lastName": "Doe",
>
> "preferredName": "Howie",
>
> "title": "Mr"
>
> },
>
> "addresses": \[
>
> {
>
> "type": "home",
>
> "address1": "1 Some Street",
>
> "address2": "Some Suburb",
>
> "address3": "Some City",
>
> "address4": null,
>
> "country": "New Zealand",
>
> "postcode": 1111
>
> },
>
> {
>
> "type": "business",
>
> "address1": "2 Work Street",
>
> "address2": "Work Suburb",
>
> "address3": "Work City",
>
> "address4": null,
>
> "country": "New Zealand",
>
> "postcode": 2222
>
> }
>
> \]
>
> }

If passenger 12345 did not exist, the HTTP return code would be 404.

If a requested sub resource did not exist e.g. addresses for passenger
54321: GET https://api.example.govt.nz/passengers/54321/addresses an
HTTP 404 response would not be valid. The correct response would contain
an empty array:

> #GET a single passenger address resource by ID
>
> GET https://api.example.govt.nz/passengers/54321/addresses
>
> Accept: application/json,version=1.\*
>
> {
>
> "id": 54321,
>
> "addresses": \[
>
> {
>
> "type": null,
>
> "address1": null,
>
> "address2": null,
>
> "address3": null,
>
> "address4": null,
>
> "country": null,
>
> "postcode": null
>
> }
>
> \]
>
> }

A collection will take the form of an array of the given resources,
including any related metadata. The collection returned should be the
complete set, leaving it to the consumer to reduce the quantity of
information returned by sending filters in the resource request (see
[[section 2.5.6, Query Arguments]{.underline}](#query-arguments)). The
only reason the collection should be filtered by the API provider is
based on the security context; the API consumer should only gain access
to what that consumer is allowed to see. It is advisable to aim for
consistent naming of collection resource fields, as this enables
application developers to create generic handling of the data from
across various resource collections offered by the API. Collection
resources should not contain binary attachments or other content that
will lead to large response payloads.

Note that the example below is contrived and it would be rare to expose
a resource collection as large as passengers.

**Example**

> #GET a collection of passenger resources
>
> GET <https://api.example.govt.nz/passengers>
>
> Accept: application/json,version=1.\*
>
> {
>
> "passengers": \[
>
> {
>
> "id": 12345,
>
> "names": {
>
> "firstName": "John",
>
> "middleName": "Howard",
>
> "lastName": "Doe",
>
> "salutation": "Mr John Doe",
>
> "title": "Mr"
>
> }
>
> },
>
> {
>
> "id": 98765,
>
> "names": {
>
> "firstName": "Mary",
>
> "middleName": "Pauline",
>
> "lastName": "Smith",
>
> "salutation": "Ms Mary Smith",
>
> "title": "Ms"
>
> }
>
> },
>
> {
>
> ".....lots more passengers here.....": "..."
>
> }
>
> \],
>
> "\_links": \[
>
> {
>
> "rel": "12345",
>
> "href": "https://api.example.govt.nz/passengers/12345"
>
> },
>
> {
>
> "rel": "98765",
>
> "href": "https://api.example.govt.nz/passengers/98765"
>
> },
>
> {
>
> ".....lots more links here.....": "..."
>
> }
>
> \]
>
> }

If there were no results from a query against a filter, e.g. passengers
booked on a specific flight
(GET https://api.example.govt.nz/passengers/flights/1234), the return
value would be a 200 response code, because the query is not invalid and
there may be such data in the future.

### HATEOAS

HATEOAS, or Hypermedia as the Engine of Application State, is the
principle of not just returning a response to a request, but also
returning links to other useful capabilities. So, if a POST has just
been used to create an item, the response could return links to options
to update the item, delete the item and view other items of the same
type. This makes it possible for UIs which utilise an API to be
automatically generated (in terms of hyperlinks) and adaptable to change
(response content links).

If a web page effectively captures a single state in time, then
hyperlinks are transitions to other states. The HATEOAS principle
suggests that REST should return not only response content (current
state) but also links to transitions to other states. This could result
in thinner clients and fatter APIs, and means UIs need to be built to
adapt to potential new transitions, but makes it possible to update all
UIs no matter what platform they sit on (mobile app, web application
etc.).

For example, consider the following representation of a person and
sequence of requests:

This example assumes that an address is a unique resource in its own
right and that people are associated with addresses. (This may not
always be a practical application and the example is used just to
illustrate the hypermedia concept.)

**1. User submits a request for a person record:**

\# Request person details:

> GET
> https://api.example.govt.nz/people/c70d37cf-3314-4a24-a2c3-0fca7ec0943f
>
> Host: www.example.com
>
> Accept: application/json;q=1.0

\# Response with person details:

> HTTP/1.1 200 OK
>
> Content-Location:
> https://api.example.govt.nz/people/c70d37cf-3314-4a24-a2c3-0fca7ec0943f
>
> Content-Type: application/json;charset=UTF-8
>
> Cache-control: max-age=3600,must-revalidate
>
> {
>
> \"personId\": \"d9e1a2f6-6bc9-46af-9dbb-50de7f6eacd5\",
>
> \"name\": \"Joe Bloggs\",
>
> \"email\": \"joe.bloggs@example.com\",
>
> \"addresses\": \[
>
> {
>
> \"id\": \"5046b8f2-e8aa-4ec9-a597-34d01af0fd32\",
>
> \"streetNumber\": \"12\",
>
> \"streetName\": \"Somewhere Street\",
>
> \"City\": \"Springfield\",
>
> \"type\": \"home\"
>
> },
>
> {
>
> \"id\": \"18a1a85c-3b1e-41b9-909c-668f2a803b69\",
>
> \"streetNumber\": \"1\",
>
> \"streetName\": \"Some Other Street\",
>
> \"City\": \"Springfield\",
>
> \"type\": \"business\"
>
> }
>
> \],
>
> \"\_links\": \[
>
> {
>
> \"rel\": \"self\",
>
> \"href\":
> \"https://api.example.govt.nz/people/d9e1a2f6-6bc9-46af-9dbb-50de7f6eacd5\"
>
> },
>
> {
>
> \"rel\": \"address1\",
>
> \"href\":
> \"https://api.example.govt.nz/addresses/046b8f2-e8aa-4ec9-a597-34d01af0fd32\"
>
> },
>
> {
>
> \"rel\": \"address2\",
>
> \"href\":
> \"https://api.example.govt.nz/addresses/18a1a85c-3b1e-41b9-909c-668f2a803b69\"
>
> }
>
> \]
>
> }

Assume an intermediate proxy were to cache that response as directed by
the cache control header.

**2. The user then updates the address details changing the street
number:**

\# Request to update the address details:

> PUT
> https://api.example.govt.nz/addresses/d9e1a2f6-6bc9-46af-9dbb-50de7f6eacd5
> HTTP/1.1
>
> Host: api.example.govt.nz
>
> Content-Type: application/json
>
> {
>
> \"streetNumber\": \"12a\",
>
> \"streetName\": \"Somewhere Street\",
>
> \"City\": \"Springfield\"
>
> }

\# Response that the update was successful:

> HTTP/1.1 204 No Content
>
> Location:
> https://api.example.govt.nz/addresses/046b8f2-e8aa-4ec9-a597-34d01af0fd32

If the user were now to re-fetch the person details again as per step 1,
the representation would contain a stale version of the address (street
number 12 instead of 12a) because the address representation had been
cached. This caching could occur anywhere along the network path
(including public internet) between the server and client.

Using hypermedia links for related resources improves the visibility of
the API and avoids these types of problems. Consider the revised person
representation below:

> {
>
> \"personId\": \"d9e1a2f6-6bc9-46af-9dbb-50de7f6eacd5\",
>
> \"name\": \"JoeBloggs\",
>
> \"email\": \"joe.bloggs@example.com\",
>
> \"addresses\": \[
>
> {
>
> \"rel\": \"self\",
>
> \"href\":
> \"https://api.example.govt.nz/addresses/5046b8f2-e8aa-4ec9-a597-34d01af0fd32\"
>
> },
>
> {
>
> \"rel\": \"self\",
>
> \"href\":
> \"https://api.example.govt.nz/addresses/18a1a85c-3b1e-41b9-909c-668f2a803b69\"
>
> }
>
> \],
>
> \"\_links\": \[
>
> {
>
> \"rel\": \"self\",
>
> \"href\":
> \"https://api.example.govt.nz/people/d9e1a2f6-6bc9-46af-9dbb-50de7f6eacd5\"
>
> }
>
> \]
>
> }

Using this approach, the embedded object is replaced with a link to the
"real" object. Although this approach requires a larger number of
network requests, it avoids the stale data problems and reduces payload
size, which is an important consideration for APIs being used by mobile
devices or over high latency networks.

## Consideration of state

In almost all cases a REST API should be entirely stateless. As part of
processing it is possible for an API to gather context and pass this to
a downstream system, however an API should not maintain that context for
future requests. This should not be confused with caching, as discussed
in [[section 2.12]{.underline}](#caching) of this document.

## Batch Handling & Transactions

APIs are not designed for large payloads i.e. batch handling for
retrieving or uploading batches of data. APIs are geared towards
stateless, usually synchronous, web-like requests for individual
discrete data transactions. However, batch handling can be achieved
through bundling multiple calls to the same API. This helps achieve
atomicity of transactions and aids recoverability in event of
errors.[^4]

When handling transactions, it is important to consider the
troubleshooting and recovery aspects of error handling. This includes
visibility of transaction progress and the ability to perform root cause
analysis. To achieve this, it is advisable that logging is performed on
all transactions coming through an API, with accurate timestamping, so
that monitoring tools can visualise transaction progress. It also
requires transaction identifiers (See [[section 2.6.1,]{.underline}
[Request Headers]{.underline}](#request-headers)) to be built into
transactional API calls to ensure the transaction is traceable
end-to-end.

In some cases, it may be deemed appropriate to provide an asynchronous
batch type capability using an API. This would usually be implemented in
a scenario where legacy system impact is a concern. An example of this
could be a bulk creation of person records in a database based on a
batch event in a consuming legacy application. In such a scenario it
would be preferable for the consuming application to treat each person
as a unique event and to POST to a person API for each new unique
resource. Whilst this may seem like an unnecessary overhead, by
individualising the transactions each success or error scenario can be
handled in its own right, and the consumer can be informed of their
transaction status. If this is not possible, due to some system
restriction, it is possible to asynchronously POST multiple person
details to an API. This type of interaction should not be attempted
synchronously as large batches will tie up HTTP threads and in some
cases require client/server timeout control.

**Example Request**

The following is an example of a singleton create person request:

> {
>
> \"names\": {
>
> \"firstName\": \"John\",
>
> \"middleName\": \"Howard\",
>
> \"lastName\": \"Doe\",
>
> \"salutation\": \"Mr John Doe\",
>
> \"title\": \"Mr\"
>
> }
>
> }

This is an example of a bulk person create API call:

> #POST a collection of person resources
>
> POST https://api.example.govt.nz/people
>
> Accept: application/json,version=1.\*
>
> {
>
> \"people\": \[
>
> {
>
> \"names\": {
>
> \"firstName\": \"John\",
>
> \"middleName\": \"Howard\",
>
> \"lastName\": \"Doe\",
>
> \"salutation\": \"Mr John Doe\",
>
> \"title\": \"Mr\"
>
> }
>
> },
>
> {
>
> \"names\": {
>
> \"firstName\": \"Mary\",
>
> \"middleName\": \"Pauline\",
>
> \"lastName\": \"Smith\",
>
> \"salutation\": \"Ms Mary Smith\",
>
> \"title\": \"Ms\"
>
> }
>
> },
>
> {
>
> \"\.....lots more people here\.....\": \"\...\"
>
> }
>
> \]
>
> }

**Example Response**

Note that the API is unable to respond with headers such as Location as
this request should be treated as asynchronous.

> 200 OK

## API Version Control

### API Version Control Methods

There are two main API versioning methodologies commonly used. There are
positives and negatives to both approaches and a large amount of debate
over which is the most "RESTful". Rather than stipulate a methodology to
use in this standard, below is a description of each methodology in
order of preference. Both, however, are acceptable. What is more
important is that APIs are versioned and that there is an understanding
of when and why to version an API.

#### Accept Header Versioning

This is usually considered the most RESTful way to version APIs because
the resource path remains "pure" and it is possible to provide more
version flexibility for clients. It is, however, technically more
difficult to implement, and in many cases commercial API
management/gateway products do not support or work well with this
approach.

Header based versioning should be performed using the Accept header
where a consuming application requests an API version as defined in an
Accept header. Wildcards (\*) are used by the consuming application to
indicate acceptance of the latest major or minor version of an API.

**Example**

> #Get details for provider id 123435 -- latest minor version of the API
>
> GET https://api.example.govt.nz/providers/12345
>
> Accept: application/json, version=1.\*
>
> Host: api.example.govt.nz
>
> #Get details for provider id 123435 --version 1.1 of the API
>
> GET https://api.example.govt.nz/providers/12345
>
> Accept: application/json, version=1.1
>
> Host: api.example.govt.nz
>
> #Get details for provider id 123435 -- latest version of the API
>
> GET https://api.example.govt.nz/providers/12345
>
> Accept: application/json, version=\*
>
> Host: api.example.govt.nz

The response should include the version of the API that responded to the
client request in the **Content-Type** header.

**Example**

> Content-Type: application/json,version=1.2

#### URI (Path) Versioning

URL-based versioning is a viable alternative, as the version number in
the URL should only change when major revisions have been made and the
interface has changed substantially without backwards compatibility. For
URL-based versioning the URI should include /vN with the major version
(N) and v as a prefix. Agencies should not include minor version numbers
when using version numbers in the API paths.

This is probably the easiest method to implement, but a number of REST
purists feel that it compromises the URI and does not offer enough
flexibility to consumers. If there is a requirement to support a large
number of historical versions of APIs it can mean that there is
complexity introduced with the number of URIs to maintain.

**Example**

> #Query version of version 1 of the search API
>
> GET
> [[https://api.example.govt.nz/customers/v1/search?first-name=John&last-name=Smith&page-size=10]{.underline}](https://api.example.govt.nz/customers/v1/search?first-name=John&last-name=Smith&page-size=10)
>
> #Query version 2 of the search API
>
> GET
> https://api.example.govt.nz/customers/v2/search?first-name=John&last-name=Smith&page-size=10

The response should still indicate the version of the API that was
called. This can be done as above, using the **Content-Type** header or
in the **Location** header, as the version in the path indicates the API
that was called.

### When to Version

Simply put, an API should be versioned when a change is considered
breaking. One of the benefits of an API is that, if it is well designed,
there should be fewer breaking changes. In government however, there are
likely to be situations where legislative changes enforce a new version
of an API and deprecation of all previous versions.

#### Breaking Changes

A change is a breaking change if any consuming application requires
changes to work with the new version. i.e. the new version will not
successfully process messages provided by existing consumers. A breaking
change should be considered as a major version change e.g. 1.3 to 2.0.

Examples of breaking changes include:

-   The removal of any property from the response representation

-   The change of datatype for an existing property, or a change from
    optional to required

-   The removal of any resource, or HTTP Verb support

-   A change to the way errors are handled

-   Any change to existing resource URIs

#### Non-Breaking Changes

A change is non-breaking if any message that would have been processed
by the previous version will be successfully processed by the new
version (i.e. backwards compatible). This will enable an existing
consumer of the previous version to work with the new version without
requiring modification. A non-breaking change should be considered as a
minor version change e.g. 1.1 to 1.2.

Such changes include:

-   The addition of new properties to the JSON representation

-   The addition of new resources

-   The addition of support for new HTTP Verbs (new operations) on
    existing resources

-   Support for new custom headers, e.g. for request tracing

### Software Configuration Management

It is important to remember that version control is more than just
versioning the resource. An API will inherently have associated code and
artefacts. Consider what comprises an API and include these as a logical
artefact stored and managed in a software configuration management (SCM)
system. It is a good idea to try and capture all components in a format
that can be controlled by SCM. A good example of this is UML diagrams;
these cannot be version controlled unless captured in a text like
format. See
[[http://www.planttext.com/planttext]{.underline}](http://www.planttext.com/planttext)
or
[[https://www.websequencediagrams.com]{.underline}](https://www.websequencediagrams.com)
for examples of textual UML modelling.

An API artefact should, where possible, comprise the following:

-   Any API code

-   API specification (OpenAPI)

-   Unit test scripts such as
    [[JUnit]{.underline}](http://junit.org/junit5/) or
    [[Mocha]{.underline}](https://mochajs.org/).

-   Continuous integration support files such as grunt.js or Ant
    scripts.

## Search

Search should be implemented using GET requests with filters provided as
query string parameters (see 2.4.6, Query Arguments). Search can be used
by API consumers to filter or sort information they want from an API.
For instance, GET /groups/search?status=active would enable the consumer
to filter the groups resource on status. Alternatively, GET
/groups/search?status=active&sort=status,name enables the consumer to
return active groups ordered by status and name. It can also be useful
to allow the consumer to choose which fields they want back from the
API, so they only receive the content they need in the API response.

**Example**

> #Get a list of groups that are either active or inactive, sorted by
>
> #name and status
>
> GET
> https://api.example.govt.nz/groups/search?status=active,inactive&sort=name,status
>
> {
>
> \"groups\": \[
>
> {
>
> \"id\": \"0219c539-5885-4ab6-a55b-b0de7537c426\",
>
> \"name\": \"API lovers\",
>
> \"status\": \"active\"
>
> },
>
> {
>
> \"id\": \"1219c539-5885-4ab6-a55b-b0de7537c427\",
>
> \"name\": \"Developers\",
>
> \"status\": \"active\"
>
> },
>
> {
>
> \"id\": \"7219c539-5885-4ab6-a55b-b0de7537c42c\",
>
> \"name\": \"Risk analysts\",
>
> \"status\": \"active\"
>
> },
>
> {
>
> \"id\": \"3219c539-5885-4ab6-a55b-b0de7537c42h\",
>
> \"name\": \"Writers\",
>
> \"status\": \"active\"
>
> },
>
> {
>
> \"id\": \"g219c539-5885-4ab6-a55b-b0de7537c425\",
>
> \"name\": \"Authors\",
>
> \"status\": \"inactive\"
>
> }
>
> \],
>
> \"\_links\": \[
>
> {
>
> \"rel\": \"self\",
>
> \"href\": \"https://api.example.govt.nz/groups?sort=status,name\"
>
> },
>
> {
>
> \"rel\": \"API Lovers\",
>
> \"href\":
> \"https://api.example.govt.nz/groups/0219c539-5885-4ab6-a55b-b0de7537c426\"
>
> },
>
> {
>
> \"rel\": \"Developers\",
>
> \"href\":
> \"https://api.example.govt.nz/groups/1219c539-5885-4ab6-a55b-b0de7537c427\"
>
> },
>
> {
>
> \"rel\": \"Risk analysts\",
>
> \"href\":
> \"https://api.example.govt.nz/groups/7219c539-5885-4ab6-a55b-b0de7537c42c\"
>
> },
>
> {
>
> \"rel\": \"Writers\",
>
> \"href\":
> \"https://api.example.govt.nz/groups/3219c539-5885-4ab6-a55b-b0de7537c42h\"
>
> },
>
> {
>
> \"rel\": \"Authors\",
>
> \"href\":
> \"https://api.example.govt.nz/groups/g219c539-5885-4ab6-a55b-b0de7537c425\"
>
> }
>
> \]
>
> }

In rare circumstances it is possible that an extremely complex search
API may run into query string or URL length limitations, although this
is probably an indication that the design of the search operation is too
complicated. The exact length limit is server and client dependent. For
example, the Apache server has a default limit of 8KB, Microsoft IIS has
a default of 16KB, and many browsers are limited to around 2KB maximum
URL length.

Where the total length can potentially exceed 2KB, the only option is to
implement the search operation using the POST verb with an appropriately
designed request object to contain the search parameters.

**Template**

> POST /{version}/{namespace}/{search-resource}

**Example Request**

> POST /v1/people/person-search?page=5 HTTP/1.1
>
> Host: www.example.com
>
> Content-Type: application/json
>
> {
>
> \"startDateBefore\":\"2010-01-01\",
>
> \"position\": \"Manager\",
>
> \"businessUnit\": \"Operations\",
>
> . . . many other search parameters . . .
>
> }

**Example Response**

> HTTP/1.1 200 OK
>
> Content-Type: application/json
>
> {
>
> \"pageSize\": 10,
>
> \"page\": 5,
>
> \"totalItems\": 77,
>
> \"totalPages\": 8,
>
> \"items\": \[
>
> . . . lots of people objects here . . .
>
> \]
>
> \"\_links\": \[
>
> {
>
> \"rel\": \"first\",
>
> \"href\": \"https://www.example.com/v1/people/person-search?page=1\"
>
> },
>
> {
>
> \"rel\": \"prev\",
>
> \"href\": \" https://www.example.com/v1/people/person-search?page=4\"
>
> },
>
> {
>
> \"rel\": \"next\",
>
> \"href\": \" https://www.example.com/v1/people/person-search?page=6\"
>
> },
>
> {
>
> \"rel\": \"last\",
>
> \"href\": \" https://www.example.com/v1/people/person-search?page=8\"
>
> },
>
> \]
>
> }

Other considerations include special characters or filters that add
additional complexity due to URL encoding requirements. For example, the
search function might need to support "\<" or "\>" operators, or special
characters for non-English language support. Additionally, structured
query language (SQL) words should be avoided as common threat detection
filters may block requests containing words such as 'DROP', 'ALTER' or
'DELETE' in case they are SQL injection attacks. See [[OWASP XSS Cheat
Sheet]{.underline}](https://www.owasp.org/index.php/XSS_Prevention_Cheat_Sheet)
and [[OWASP SQL Injection Cheat
Sheet]{.underline}](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet)
for details.

Paging behaviour for search results should be consistent with the
interaction as described in [[section 2.5.6, Query
Arguments]{.underline}](#query-arguments). Pagination can be implemented
as a page number and page size, offset and limit, or continuation token,
depending on the scale and changeability of the search results.

Note: It is worth pointing out that since the HTTP protocol treats POST
operations as unsafe, the result is not cacheable. This applies even if
the response has a Cache-Control header included, so consider the
performance impacts on the API if this is a high-volume operation.

## Caching

Caching enables faster responses from APIs and reduces server load. It
is good for information which is frequently requested but does not
change very often. The aim is to retrieve information once but re-use
many times.

There are a number of caching methodologies available. This section
focuses on two types of caching that should be owned and controlled by
the provider, primarily for APIs.

### Response Cache

A response cache is a cache that contains the response to a GET request
on a unique resource. The response should be cached as close to the
consumer as possible while remaining inside the control boundaries of
the agency. Response caches are usually fast, in-memory caches. Many off
the shelf API gateway/management solutions provide a built-in response
cache. When using a response cache, agencies should ensure that they
understand and monitor their cache to ensure that stale objects are kept
to a minimum and that they have sufficient system memory to service
caching loads. This means ensuring that the cache is refreshed once a
user has updated the information or a cache timeout has occurred.

Consider the following example regarding response cache:

![](media/image9.png){width="4.994944225721785in"
height="8.70753937007874in"}

[]{#_heading=h.3abhhcj .anchor}*Figure 50: Caching sequence diagram*

### Object Cache

An object cache is used to cache objects that are fundamental to the
function of an API but may not change on a regular basis. For example,
an API may include a tax code validation step. Tax code references are
held in a back-end database. To prevent redundant requests to the
database, the API layer could cache tax codes in its object cache and
refer to these until the cache becomes invalid. The diagram below
details an example sequence.

![](media/image6.png){width="5.331773840769904in"
height="6.959839238845144in"}

[]{#_heading=h.49gfa85 .anchor}*Figure 51: Caching sequence diagram*

## Error Handling

Error handling is important because API consumers see the API as a black
box, and when an error occurs they need to know how to handle it. Hence
error responses need to be informative yet avoid information leakage
about the internals of the back-end system. Errors should be handled in
both a human- and machine-consumable way. When an error occurs, the
response body should contain:

-   The HTTP status code

-   An API-specific error code, which API support staff will be able to
    look up to identify what has gone wrong

-   A human readable error message (possibly including selective
    technical details if the API is a development/test release for
    developer consumption only)

### HTTP Status Codes

RESTful APIs should always use the standard HTTP error responses when an
error occurs, but different codes may be pertinent depending on the HTTP
verb being used and the quantity of data being retrieved (e.g., single
item vs. list/collection of data).

The following tables give an example of good practice use of HTTP error
codes:

  -----------------------------------------------------------------------
  GET Response Status                             
  Codes                                           
  ----------------------- ----------------------- -----------------------
  **Code**                **Meaning**             **Description**

  200                     OK                      The request was
                                                  successful, and the
                                                  response body contains
                                                  the representation
                                                  requested

  302                     FOUND                   A common redirect
                                                  response; you can GET
                                                  the representation at
                                                  the URI in the Location
                                                  response header

  304                     NOT MODIFIED            Your client\'s cached
                                                  version of the
                                                  representation is still
                                                  up to date

  401                     UNAUTHORIZED            The supplied
                                                  credentials, if any,
                                                  are not sufficient to
                                                  access the resource

  404                     NOT FOUND               The requested
                                                  representation was not
                                                  found

  429                     TOO MANY REQUESTS       Your application is
                                                  sending too many
                                                  simultaneous requests

  500                     SERVER ERROR            An internal server
                                                  error prevented return
                                                  of the representation
                                                  response

  503                     SERVICE UNAVAILABLE     We are temporarily
                                                  unable to return the
                                                  representation. Please
                                                  wait and try again
                                                  later.

  **POST or PUT Response                          
  Status Codes**                                  

  **Code**                **Meaning**             **Description**

  200                     OK                      The request was
                                                  successful, and the
                                                  resource was updated.
                                                  The response body
                                                  contains the updated
                                                  representation

  201                     CREATED                 The request was
                                                  successful, a new
                                                  resource was created,
                                                  and the response body
                                                  contains the
                                                  representation

  400                     BAD REQUEST             The data given in the
                                                  POST or PUT failed
                                                  validation. Inspect the
                                                  response body for
                                                  details

  401                     UNAUTHORIZED            The supplied
                                                  credentials, if any,
                                                  are not sufficient to
                                                  create or update the
                                                  resource

  404                     NOT FOUND                

  405                     METHOD NOT ALLOWED      You can\'t POST or PUT
                                                  to the resource

  429                     TOO MANY REQUESTS       Your application is
                                                  sending too many
                                                  simultaneous requests

  500                     SERVER ERROR            We couldn\'t create or
                                                  update the resource.
                                                  Please try again later

  **DELETE Response                               
  Status Codes**                                  

  **Code**                **Meaning**             **Description**

  204                     OK                      The request was
                                                  successful; the
                                                  resource was deleted

  401                     UNAUTHORIZED            The supplied
                                                  credentials, if any,
                                                  are not sufficient to
                                                  delete the resource

  404                     NOT FOUND                

  405                     METHOD NOT ALLOWED      You can\'t DELETE the
                                                  resource

  429                     TOO MANY REQUESTS       Your application is
                                                  sending too many
                                                  simultaneous requests

  500                     SERVER ERROR            We couldn\'t delete the
                                                  resource. Please try
                                                  again later
  -----------------------------------------------------------------------

[]{#_heading=h.25b2l0r .anchor}*Table 24: HTTP Status Codes*[^5]

Where a consumer attempts to call a non-existent API end point, respond
with a **501 Not Implemented** status code.

### API-Specific Error Code

Error responses need to supply enough information to allow the API
consumer to react appropriately to the error, yet not give away too
much. But when a critical error occurs it is important for the API
provider to be able to trace the root cause and fix it as soon as
possible.

One way of achieving this is to return an API-specific error code in the
response to consumer. When the consumer reports the error to the API
support team, the consumer can relate the associated API-specific code.
The support team can then look this code up and ascertain exactly what
has gone wrong and who needs to address it.

### Human-Readable Error Message

The human readable error message should be as informative as is useful
to an end customer, without offering too many technical details (e.g.
"An account with this ID already exists").

It is important to avoid revealing system information in the human
readable response, such as composition of the backend system (e.g.
component names), as this informs malicious consumers as to what
vulnerabilities and back doors to look for. It is also important not to
confirm or deny sensitive information, such as username in a
username/password combination, as this informs potential attackers which
criteria they have got correct.[^6]

In non-production instances of the API it may be appropriate to offer
more verbose error messages with some technical detail (e.g. "Body
should be a JSON object"). However, it is still recommended not to
reveal too much about the internal systems which underpin the API, as
non-production systems still reflect a lot of the composition of
production.

**Example**

> {
>
>     \"errors\": \[
>
>         {
>
>             \"code\": 12345,
>
>             \"description\": \"There has been an error - retrying the
> request will not succeed. Please contact support\"
>
>         },
>
>         {
>
>             \"code\": 98765,
>
>             \"description\": \"A more detailed description of the
> error if appropriate\"
>
>         }
>
>     \],
>
>     \"\_links\": \[
>
>         {
>
>             \"href\": \"https://support.example.govt.nz\",
>
>             \"rel\": \"support\"
>
>         }
>
>     \]
>
> }

# API Governance

API governance helps save time and money because it ensures that APIs
are built proactively to achieve specific goals and bring value to the
Agency. API governance also helps Agencies make intelligent decisions
regarding API programs and establish best practices for building,
deploying, and consuming APIs.

API Governance should include:

-   Specification and Resource Definitions -- governing contracts and
    resource definitions helps improve the consistency and reusability
    of APIs;

-   Style and Pattern Guidelines -- standardizing API design ensures
    APIs remain consistent and improve usability;

-   Automation -- establishing guardrails to make it easier to comply
    with policies than not. For example, API scaffolding that
    automatically generates security and audit componentry for APIs or
    build pipelines that enforce security policies, such as coding
    standards and security scans;

-   Lifecycle -- governing the lifecycle of an API, from publication to
    versioning and deprecation to retirement;

-   Tracking and Analytics -- keeping track of where APIs are deployed,
    who is using them and how they are being used. This information
    helps inform other aspects of API governance.

-   A robust code review process. Ensuring that your development teams
    understand the concepts laid out in this document and establishing a
    practice where collaborative code reviews are performed. It is
    recommended that software is developed using a branch strategy with
    at least one peer review required prior to code merge and
    deployment.

When your API designers and developers are on the same page regarding
APIs, the more efficient, valuable, and successful your API programs
will be. Governance is especially beneficial for Agencies that have a
large API program or microservices architectures. 

For more information, refer to
[[https://nordicapis.com/api-governance-how-important-is-it-for-api-strategy/]{.underline}](https://nordicapis.com/api-governance-how-important-is-it-for-api-strategy/)

# Glossary of terms

Below is a list of common terms. Terms in the Description column
highlighted in bold are described elsewhere in the Glossary.

  -----------------------------------------------------------------------
  Term                 Description
  -------------------- --------------------------------------------------
  Analytics            Analytics in the context of this document is the
                       capturing and reporting of API usage.

  Consumers            **Customers**, **API Consuming Applications** and
                       **Application Developers** who use the **API**.

  Consuming            This is any application (on any device) that
  Application          consumes an **API**.

  Context              Context in this document generally refers to
                       request context. For example, a **JWT Token** may
                       contain information about the customer initiating
                       an API request.

  Customers            People (or organisations) that use the **Consuming
                       Applications** to access the API resources the
                       **API Provider** is offering.

  Discovery            The ability for **Application Developers** to find
                       resources and associated APIs to use in their
                       **Consuming Applications**

  API                  Application Programming Interface - a piece of
                       software, which provides a way for other disparate
                       pieces of software (applications, systems) to talk
                       to one another.

  API Catalogue        The **API** delivery component that lists the
                       **APIs** offered, along with their **Interface**
                       **Specifications** and guidance on how to gain
                       access and use the **APIs**.

  API Developer        The organisation (or person) who creates the
                       **API** and maintains the **Interface
                       Specification** for the **API.**

  API Developer Portal The **API** delivery component that allows **API
                       Providers** to engage with, onboard, educate and
                       manage **Application Developers** whether inside
                       or outside the organisation. These management
                       activities will generally include registration,
                       documentation, analytics etc.

  API Gateway          The **API** delivery component that allows **API
                       Providers** to offer **APIs** to the outside
                       world. This component (physical or virtual) hosts
                       the APIs ready for **Consumers** to access. It
                       provides an **API Provider** with the ability to
                       control who has access to their APIs by enforcing
                       policies for access control. Some API gateways
                       also offer additional capabilities.

  API Manager          The **API** delivery component that allows **API
                       Providers** to control an **API's** visibility and
                       behaviour. It is usually exposed as a UI/console
                       to internal staff only, as it is seen as an
                       administration component. It offers a variety of
                       capabilities, including API registration and
                       catalogue administration.

  API Provider         Organisation who provides the **API** to expose a
                       resource (information or functionality) for
                       **Consumers**.

  Application          The software behind the **API** which provides the
                       business logic for the resource.

  Application          Software developer or organisation who builds
  Developer            **Consuming Applications** that use the **API**.
                       An application developer can be internal to your
                       agency, developers that work with trusted
                       partners, developers from other agencies or
                       developers from the private sector.

  Interface            Provides technical information to the **API
  Specification        Developer** community about the **API**. It
                       includes information about how the **API** works,
                       any access control features and any error
                       conditions.

  Product Manager      The product manager is usually a technical role.
                       They understand an agencies API landscape and are
                       owners of API management platforms.

  Product Owners       The product ownership function usually resides in
                       a business area rather than technology. The role
                       of the product owner is to understand the product
                       that the agency is trying to deliver and be able
                       to make decisions on the representation of the
                       product in an **API**.

  Publish              The act of releasing the interface specification
                       and associated API to a location accessible by
                       **Application Developers**

  Resource             The information or functionality exposed by the
                       **API**.

  State                State defines the point in time record of an
                       in-flight transaction. Some systems maintain *user
                       state* for a period of time to enable a
                       transaction to be continued from the point of last
                       recorded state. APIs are usually, but not always,
                       considered stateless.
  -----------------------------------------------------------------------

[]{#_heading=h.415t9al .anchor}*Table 6: Glossary of terms*

# Glossary of acronyms 

  -----------------------------------------------------------------------
  Acronym                             Definition
  ----------------------------------- -----------------------------------
  AD                                  Active Directory

  API                                 Application Programming Interface

  ASCII                               American Standard Code for
                                      Information Interchange

  CA                                  Certificate Authority

  CDN                                 Content Delivery Network

  DHE                                 Diffie-Hellman Ephemeral

  DMZ                                 Demilitarized Zone

  DoS                                 Denial of Service

  ECDHE                               Elliptic Curve DHE

  HATEOAS                             Hypermedia As The Engine Of
                                      Application State

  HPP                                 HTTP Parameter Pollution

  HTTP                                Hyper Text Transfer Protocol

  IETF                                Internet Engineering Task Force

  JSON                                JavaScript Object Notation

  JWA                                 JSON Web Algorithms

  JWE                                 JSON Web Encryption

  JWK                                 JSON Web Key

  JWS                                 JSON Web Signature

  JWT                                 JSON Web Token

  LDAP                                Lightweight Directory Access
                                      Protocol

  MAC                                 Message Authentication Code

  OWASP                               Open Web Application Security
                                      Project

  PBD                                 Primary Business Data

  RAML                                Rest API Modelling Language

  REST                                Representative State Transfer

  RFC                                 Request for Comments (IETF)

  RO                                  Resource Owner

  RS                                  Resource Server

  SAML                                Security Assertion Markup Language

  SCIM                                System for Cross-domain Identity
                                      Management

  SEO                                 Search Engine Optimization

  SLA                                 Service Level Agreement

  SOAP                                Simple Object Access Protocol

  SPML                                Service Provisioning Markup
                                      Language

  SQL                                 Structured Query Language

  SSO                                 Single Sign On

  STS                                 Security Token Service

  TBC                                 To Be Completed

  TBD                                 To Be Done

  TLS                                 Transport Layer Security
                                      (superseded SSL)

  URL                                 Uniform Resource Locator

  URI                                 Uniform Resource Identifier

  WSDL                                Web Service Definition Language

  XSD                                 XML Schema Definition

  WADL                                Web API Description Language

  XACML                               eXtensible Access Control Markup
                                      Language

  XML                                 eXtensible Markup Language

  YAML                                YAML Ain\'t Markup Language
  -----------------------------------------------------------------------

[]{#_heading=h.vgdtq7 .anchor}*Table 7: Glossary of acronyms*

# Further Reading

+-----------------------------------+-----------------------------------+
| OWASP REST Security               | [[https://www.owasp.org/index.php |
|                                   | /REST_Security_Cheat_Sheet]{.unde |
|                                   | rline}](https://www.owasp.org/ind |
|                                   | ex.php/REST_Security_Cheat_Sheet) |
+===================================+===================================+
| OWASP API Security Project        | [<https:                          |
|                                   | //www.owasp.org/index.php/OWASP_A |
|                                   | PI_Security_Project>]{.underline} |
+-----------------------------------+-----------------------------------+
| OWASP Top Ten Project             | [<https://owasp.org/w             |
|                                   | ww-project-top-ten/>]{.underline} |
+-----------------------------------+-----------------------------------+
| OWASP Secure Coding Principles    | [<http                            |
|                                   | s://www.owasp.org/index.php/Secur |
|                                   | e_Coding_Principles>]{.underline} |
+-----------------------------------+-----------------------------------+
| NZ Protective Security            | [[https://www.protectivesecuri    |
|                                   | ty.govt.nz/]{.underline}](https:/ |
|                                   | /www.protectivesecurity.govt.nz/) |
+-----------------------------------+-----------------------------------+
| Using HTTP Methods for RESTful    | [[http://www.restapitutorial.     |
| Services                          | com/lessons/httpmethods.html]{.un |
|                                   | derline}](http://www.restapitutor |
|                                   | ial.com/lessons/httpmethods.html) |
+-----------------------------------+-----------------------------------+
| Reserved JavaScript Keywords      | [[htt                             |
|                                   | p://www.w3schools.com/js/js_reser |
|                                   | ved.asp]{.underline}](http://www. |
|                                   | w3schools.com/js/js_reserved.asp) |
+-----------------------------------+-----------------------------------+
| REST API Resource Modelling       | [[htt                             |
|                                   | ps://www.thoughtworks.com/insight |
|                                   | s/blog/rest-api-design-resource-m |
|                                   | odeling]{.underline}](https://www |
|                                   | .thoughtworks.com/insights/blog/r |
|                                   | est-api-design-resource-modeling) |
+-----------------------------------+-----------------------------------+
| Government ICT Strategy           | [[                                |
|                                   | https://www.ict.govt.nz/strategy- |
|                                   | and-action-plan/strategy/]{.under |
|                                   | line}](https://www.ict.govt.nz/st |
|                                   | rategy-and-action-plan/strategy/) |
+-----------------------------------+-----------------------------------+
| OpenAPI Specification             | [[https                           |
|                                   | ://github.com/OAI/OpenAPI-Specifi |
|                                   | cation]{.underline}](https://gith |
|                                   | ub.com/OAI/OpenAPI-Specification) |
+-----------------------------------+-----------------------------------+
| HTTP 1.1 Standards RFCs           | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7230]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7230) |
|                                   |                                   |
|                                   | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7231]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7231) |
|                                   |                                   |
|                                   | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7232]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7232) |
|                                   |                                   |
|                                   | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7233]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7233) |
|                                   |                                   |
|                                   | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7234]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7234) |
|                                   |                                   |
|                                   | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7235]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7235) |
|                                   |                                   |
|                                   | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7236]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7236) |
|                                   |                                   |
|                                   | [[https://tools.ietf.o            |
|                                   | rg/html/rfc7237]{.underline}](htt |
|                                   | ps://tools.ietf.org/html/rfc7237) |
+-----------------------------------+-----------------------------------+

[]{#_heading=h.1ulbmlt .anchor}*Table 11: Further Reading*

# Appendix A -- HTTP Verbs

**[Required]{.smallcaps}**

## GET

GET is used:

-   For retrieval of information

-   If the interaction is more like a question (i.e. it is a safe
    operation such as a query)

The HTTP GET method is used to read (or retrieve) a representation of a
resource. It can be used to retrieve information about an individual
resource (e.g. customers/123456) or to retrieve a collection (list) of
resources (e.g. customers).

In the "happy" (non-error) path, GET returns a representation in JSON
and an HTTP response code of 200 (OK). In an error case, it most often
returns a 404 (NOT FOUND) or 400 (BAD REQUEST) if the requested resource
does not exist.

According to the HTTP specification, GET (along with HEAD) requests are
used only to read data and not change it. Therefore, they are considered
safe when used this way. That is, they can be called without risk of
data modification or corruption - calling it once has the same effect as
calling it 10 times. GET is idempotent, which means that making multiple
identical requests ends up having the same result as a single
request. Do not expose unsafe operations via GET - it should never
modify any resources on the server.

**Examples:**

> GET https://api.example.govt.nz/passengers/12345
>
> Accept: application/json,version=1.\*
>
> Accept-Encoding: gzip,deflate
>
> Host: api.example.com
>
> #Success Response
>
> Content-Length: 612
>
> Location: https://api.example.govt.nz/passengers/12345
>
> Date: Fri Jul 08 16:52:21 NZST 2016
>
> CorrelationID: 65347f577ade5f7750234abb
>
> Transaction-Id: 65347f577bde5949ac7bd448
>
> {
>
> \"id\": 12345
>
> \"names\": {
>
> \"firstName\": \"John\",
>
> \"middleName\": \"Howard\",
>
> \"lastName\": \"Doe\",
>
> \"salutation\": \"Mr John Doe\",
>
> \"title\": \"Mr\"
>
> },
>
> \"addresses\": \[
>
> {
>
> \"type\": \"home\",
>
> \"address1\": \"1 Some Street\",
>
> \"address2\": \"Some Suburb\",
>
> \"address3\": \"Some City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 1111
>
> },
>
> {
>
> \"type\": \"business\",
>
> \"address1\": \"2 Work Street\",
>
> \"address2\": \"Work Suburb\",
>
> \"address3\": \"Work City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 2222
>
> }
>
> \]
>
> }
>
> GET https://api.example.govt.nz/passengers/12345/flights
>
> GET https://api.example.govt.nz/schools/98765/learners

Some API GET calls will return a single resource item whilst some calls
will return a collection of resource items. See [[section 2.7.6
Singletons vs. Collections]{.underline}](#singletons-vs.-collections)
for more details

## POST

POST is used:

-   To create a piece of information or resource item

-   To spawn an action 

-   If the interaction is like placing an order

-   If the interaction changes the state of the resource in a way that
    the user would perceive (e.g. a subscription to a service)

-   If the user be held accountable for the results of the interaction

The POST verb is most-often utilized to create new resources. In
particular, it is used to create sub-resources: that is, subordinate to
some other (e.g. parent) resource. In other words, when creating a new
resource, POST to the parent and the API takes care of associating the
new resource with the parent, assigning an ID (new resource URI),
etc. On successful creation, POST returns an HTTP status 201, with a
Location header containing a link to the newly created resource.

POST is neither safe nor idempotent. It is therefore recommended for
non-idempotent resource requests. Making two identical POST requests
will most-likely result in two resources containing the same
information.

The body content of a POST request will differ to that of a PUT, as the
provider will create certain values such as a unique identifier for the
resource and its creation date.

In many cases a POST may have a small subset of the data that can exist
on a resource -- a subsequent PUT to the resource can be performed to
populate the data.

**Examples:**

> #Create a new passenger resource
>
> POST https://api.example.govt.nz/passengers
>
> {
>
> \"names\": {
>
> \"firstName\": \"John\",
>
> \"middleName\": \"Howard\",
>
> \"lastName\": \"Doe\",
>
> \"salutation\": \"Mr John Doe\",
>
> \"title\": \"Mr\"
>
> },
>
> \"addresses\": \[
>
> {
>
> \"type\": \"home\",
>
> \"address1\": \"1 Some Street\",
>
> \"address2\": \"Some Suburb\",
>
> \"address3\": \"Some City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 1111
>
> },
>
> {
>
> \"type\": \"business\",
>
> \"address1\": \"2 Work Street\",
>
> \"address2\": \"Work Suburb\",
>
> \"address3\": \"Work City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 2222
>
> }
>
> \]
>
> }

> #Successful resource creation response
>
> HTTP/1.1 201 Created
>
> Location: https://api.example.govt.nz/passengers/12345
>
> Content-Location: https://api.example.govt.nz/passengers/12345
>
> Content-Type: application/json
>
> {
>
> \"id\": 12345,
>
> \"names\": {
>
> \"firstName\": \"John\",
>
> \"middleName\": \"Howard\",
>
> \"lastName\": \"Doe\",
>
> \"salutation\": \"Mr John Doe\",
>
> \"title\": \"Mr\"
>
> },
>
> \"addresses\": \[
>
> {
>
> \"type\": \"home\",
>
> \"address1\": \"1 Some Street\",
>
> \"address2\": \"Some Suburb\",
>
> \"address3\": \"Some City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 1111
>
> },
>
> {
>
> \"type\": \"business\",
>
> \"address1\": \"2 Work Street\",
>
> \"address2\": \"Work Suburb\",
>
> \"address3\": \"Work City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 2222
>
> }
>
> \]
>
> }

## PUT

PUT is used:

-   To update an existing resource item

-   To replace an existing resource item

PUT is most-often utilized to update information, PUT-ing to a known
resource URI with the request body containing the newly updated
representation of the original resource.

However, PUT can also be used to create a resource in the case where the
resource ID is chosen by the consumer instead of by the API itself:
where PUT is to a URI that contains the value of a non-existent resource
ID. Again, the request body contains a resource representation. This
method of creation should be avoided if possible, or used sparingly. If
consumer-defined resource IDs are required, use POST to create the new
resource and provide the consumer-defined ID in the body representation
(see POST).

On a successful update, PUT returns 200 (or 204 if not returning any
content in the body). If using PUT to create, return HTTP status 201 on
successful creation. A body in the response is optional. It is not
necessary to return a link via a Location header in the creation case
since the consumer already knows the resource ID, having set it
themselves.

PUT is not a safe operation: it modifies (or creates) state on the
server, but it is idempotent. I.e. if you create or update a resource
using PUT and then make that same call again, the resource is still
there and still has the same state as it did with the first call.
However, were the PUT call to increment a counter within the resource,
the call is no longer idempotent. Sometimes this is necessary behaviour,
and it may be enough to document that the call is not idempotent.
However, it\'s recommended to keep PUT requests idempotent. It is
strongly recommended to use POST for non-idempotent requests.

It is good practice to perform a GET on a resource before you perform a
PUT. This means that the consuming application has the latest
representation of that resource. PUT should contain the entire resource
content in the message body. By performing a GET prior to the PUT the
consuming application can re-send the results of the GET with any
modifications.

When using a resource response cache, any PUT to a resource should
invalidate that cache or re-populate the cache with the updated
resource.

**Examples:**

> \# Get a resource
>
> GET https://api.example.govt.nz/passengers/12345/1w3r4y6u
>
> \# The response can be cached in a response cache with a cache key of
> the resource e.g. cachekey\_\_12345_1w3r4y6u
>
> \# Response Body
>
> {
>
> \"id\": \"1w3r4y6u\",
>
> \"passenger_name\": \"SMITH/NICOLAS\",
>
> \"pnr_number\": \"CG4X7U\",
>
> \"travel_class\": \"business\",
>
> \"seat\": \"74J\",
>
> \"auxiliary_fields\": \[
>
> {
>
> \"label\": \"Terminal\",
>
> \"value\": \"T1\"
>
> },
>
> {
>
> \"label\": \"Departure\",
>
> \"value\": \"30OCT 19:05\"
>
> }
>
> \],
>
> \"secondary_fields\": \[
>
> {
>
> \"label\": \"Boarding\",
>
> \"value\": \"18:30\"
>
> },
>
> {
>
> \"label\": \"Gate\",
>
> \"value\": \"D57\"
>
> },
>
> {
>
> \"label\": \"Seat\",
>
> \"value\": \"74J\"
>
> },
>
> {
>
> \"label\": \"Sec.Nr.\",
>
> \"value\": \"003\"
>
> }
>
> \],
>
> \"flight_info\": {
>
> \"flight_number\": \"KL0642\",
>
> \"departure_airport\": {
>
> \"airport_code\": \"JFK\",
>
> \"city\": \"New York\",
>
> \"terminal\": \"T1\",
>
> \"gate\": \"D57\"
>
> },
>
> \"arrival_airport\": {
>
> \"airport_code\": \"AMS\",
>
> \"city\": \"Amsterdam\"
>
> },
>
> \"flight_schedule\": {
>
> \"departure_time\": \"2016-01-02T19:05\",
>
> \"arrival_time\": \"2016-01-05T17:30\"
>
> }
>
> }
>
> }
>
> \# Put to a resource (update) changing the seat number
>
> PUT https://api.example.govt.nz/passengers/12345/flights/1w3r4y6u
>
> #The api invalidates cache object with key cachekey\_\_12345_1w3r4y6u
>
> {
>
> \"id\": \"1w3r4y6u\",
>
> \"passenger_name\": \"SMITH/NICOLAS\",
>
> \"pnr_number\": \"CG4X7U\",
>
> \"travel_class\": \"business\",
>
> \"seat\": \"10J\",
>
> \"auxiliary_fields\": \[
>
> {
>
> \"label\": \"Terminal\",
>
> \"value\": \"T2\"
>
> },
>
> {
>
> \"label\": \"Departure\",
>
> \"value\": \"30OCT 19:05\"
>
> }
>
> \],
>
> \"secondary_fields\": \[
>
> {
>
> \"label\": \"Boarding\",
>
> \"value\": \"18:30\"
>
> },
>
> {
>
> \"label\": \"Gate\",
>
> \"value\": \"D57\"
>
> },
>
> {
>
> \"label\": \"Seat\",
>
> \"value\": \"10J\"
>
> },
>
> {
>
> \"label\": \"Sec.Nr.\",
>
> \"value\": \"003\"
>
> }
>
> \],
>
> \"flight_info\": {
>
> \"flight_number\": \"KL0642\",
>
> \"departure_airport\": {
>
> \"airport_code\": \"JFK\",
>
> \"city\": \"New York\",
>
> \"terminal\": \"T1\",
>
> \"gate\": \"D57\"
>
> },
>
> \"arrival_airport\": {
>
> \"airport_code\": \"AMS\",
>
> \"city\": \"Amsterdam\"
>
> },
>
> \"flight_schedule\": {
>
> \"departure_time\": \"2016-01-02T19:05\",
>
> \"arrival_time\": \"2016-01-05T17:30\"
>
> }
>
> }
>
> }
>
> \# Response that update was successful
>
> HTTP/1.1 204 No Content
>
> Content-Location: /passengers/12345/flights/1w3r4y6u

## DELETE

DELETE is used:

-   To delete a resource item

DELETE is only used to delete a resource identified by a URI.

On successful deletion, DELETE returns an HTTP status 200 (OK) along
with a response body, and optionally the representation of the deleted
item, or a wrapped response. Alternatively, DELETE can return HTTP
status 204 (NO CONTENT) with no response body. 

DELETE operations are idempotent. If you DELETE a resource, it is
removed. Repeatedly calling DELETE on that resource ends up as the same
result: the resource is gone. However, calling DELETE on a resource a
second time will often return a 404 (NOT FOUND) since it was already
removed and therefore is no longer findable. This, in some opinion,
makes DELETE operations no longer idempotent, but the end-state of the
resource is the same. Returning a 404 is acceptable and communicates
accurately the status of the call. If calling DELETE were to decrement a
counter (within the resource), the DELETE call is no longer idempotent. 

**Example:**

> #Delete a resource
>
> DELETE https://api.example.govt.nz/passengers/12345/flights/1w3r4y6u

> #Response
>
> HTTP/1.1 204 No Content
>
> Content-Location: /passengers/12345/flights/1w3r4y6u

## OPTIONS

OPTIONS is used to retrieve information about what the consumer is
allowed to do with the Resource

## Other

PATCH is a valid HTTP verb, but is still in draft and its use is
discouraged due to complexity. An exception to this might be where an
agency adopted standard, such as FHIR
[[https://www.hl7.org/fhir/http.html#patch]{.underline}](https://www.hl7.org/fhir/http.html#patch),
supports the use of PATCH.

HEAD is used to retrieve metadata about a resource, such as when it was
last updated or the associated response headers. The response to a HEAD
request MUST NOT contain a body. If a response body is returned it MUST
be ignored.

# Appendix B -- HTTP Headers

**[Required]{.smallcaps}**

## Request Headers

Request headers are supplied by the consuming application and must
include the following elements:

-   Accept

-   Content-Type

-   Authorization

Header definitions can be found in
[[RFC2616]{.underline}](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)

### Accept

**[Required]{.smallcaps}**

An Accept header is required to indicate what format the consuming
application wants the information to be returned as (e.g. JSON or XML).
It is preferable for the consuming application to specify the response
content type that they expect, however it is acceptable to use the *'q'*
parameter to specify the quality of support.

**Examples**

> #Accept JSON and latest version
>
> Accept: application/json,version=\*
>
> #Prefer JSON, Accept XML and latest version 1 release
>
> Accept: application/json;q=1.0,application/xml;q=0.8,version=1.\*
>
> #Accept XML only and version 1.2 only
>
> Accept: application/xml;q=1.0,application/json;q=0.0,version=1.2

If the client has specified via the Accept header that it doesn't
support any formats provided by the API, the server should return an
HTTP 406 Not Acceptable response. The response should also include a
Link header with a link to documentation or help on supported formats.
The body of the representation should include an error message in human
readable plain text or HTML.

**Example Response**

> \# Response that indicates the request failed due to the client not
>
> \# supporting any response formats provided by the API
>
> HTTP/1.1 406 Not Acceptable
>
> Content-Type: text/plain
>
> This API does not support any of the requested content types specified
> in the HTTP Accept header. Please see
> http://www.example.com/api/documentation/widgetservice for details on
> the supported content types.

The Accept header is required, however the *'version'* and *'q'* are
recommended as this will depend on a provider's implementation and in
some cases technology choice.

### Content-Type

**[Required]{.smallcaps}**

The Content-Type header is required for all requests that include a
request body i.e. POST, PUT, DELETE.

**Example**

> #PUT https://api.example.govt.nz/v2/learners/33245
>
> Accept: application/json,version=1.\*
>
> Content-Type: application/json
>
> Authorization: Bearer x6TLB4JaomezC5rJ3CIl3KxxNinq
>
> {
>
> \"id\": \"33245\",
>
> \"names\":
>
> {
>
> \"firstName\": \"John\",
>
> \"middleName\": \"Howard\",
>
> \"lastName\": \"Doe\",
>
> \"salutation\": \"Mr John Doe\",
>
> \"title\": \"Mr\"
>
> },
>
> \"addresses\": \[
>
> {
>
> \"type\": \"home\",
>
> \"address1\": \"1 Some Street\",
>
> \"address2\": \"Some Suburb\",
>
> \"address3\": \"Some City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 1111
>
> },
>
> {
>
> \"type\": \"business\",
>
> \"address1\": \"2 Work Street\",
>
> \"address2\": \"Work Suburb\",
>
> \"address3\": \"Work City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 2222
>
> }
>
> \],
>
> \"qualifications\":\[
>
> {
>
> \"id\": \"1a4rf54ee345\",
>
> \"type\": \"Some type\",
>
> \"provider\": \"University of life\",
>
> \"providerId\": \"0o9i8u7y6tt\"
>
> },
>
> {
>
> \"id\": \"8u7y6t5r4ee\",
>
> \"type\": \"Another type\",
>
> \"provider\": \"School xyz\",
>
> \"providerId\": \"1q2w3e4r5tt\"
>
> }
>
> \]
>
> }

### Authorization

**[Required]{.smallcaps}**

Most API requests will be authorised. The Authorization header should be
used for this purpose and no other. Note that the Authorization header
is not the best place for an API Key.

The Authorization header is comprised of a type and a token depending on
the authorization type.

**Example**

> #OAuth Access Token
>
> Authorization: Bearer x6TLB4JaomezC5rJ3CIl3KxxNinq
>
> #HTTP Basic
>
> Authorization: Basic c29tZXVzZXI6c29tZSBwYXNzd29yZA==

### Accept-Encoding

**[Recommended]{.smallcaps}**

In some cases, especially where API responses are very large, it may be
worth compressing HTTP responses. (Note: where possible it is best to
avoid large payloads in API responses; however, this may not always be
possible.) An Accept-Encoding value of gzip instructs a provider that
supports HTTP compression that the consuming application supports
compressed responses.

**Example**

> Accept-Encoding: gzip,deflate

### API Key Header

**[Required]{.smallcaps}**

An API key issued to a consuming application should be sent with every
request made to the API. The name of the header is up to the agency, but
it should not be an X- prefixed header as this use is deprecated (see
2.5.3). Sometimes API keys are passed in URIs; however, this is not
considered best practice and should be avoided.

**Example**

> KeyID: pX680LyiKasUBWLuZJ8AVBHVQK03Ghtr

### If-Modified-Since/If-None-Match

**[Recommended]{.smallcaps}**

The If-Modified header is a pre-condition header used to instruct a
client on the validity of the resource requested. Note that
pre-condition handling is not required, but where appropriate should be
considered. Pre-condition control can be a complex topic so in some
cases the complexity may eclipse the value.

Conditional header standards are available in [[Hypertext Transfer
Protocol (HTTP/1.1): Conditional Requests
RFC7232](https://tools.ietf.org/html/rfc7232).]{.underline}

A consuming application can specify an If-Modified-Since header with a
date and time. The server checks the resource to see the last modified
time. If the last modification was before the date/time specified in the
header, the server will respond with an HTTP 304 status code telling the
consuming application that the resource they requested has not changed
and therefore there is no need to return the full payload in the
response.

When using If-Modified headers you should also implement ETag as
discussed in the [[headers section (2.6)]{.underline}](#http-headers).

**Example**

> \# Request with If-Modified-Since and If-None-Match headers
>
> If-Modified-Since: Wed, 18 Jun 2016 22:00:00 GMT
>
> If-None-Match: \"686897696a7c876b7e\"

The If-None-Match header indicates to the provider the ETag for the
resource that it currently holds for that resource.

**Example Response**

> \# Response that indicates the client's current representation is
> still
>
> \# valid
>
> HTTP/1.1 304 Not Modified
>
> ETag: \"686897696a7c876b7e\"
>
> Content-Length: 0

### Request tracking headers

**[Recommended]{.smallcaps}**

To support the tracking of API requests it is a good idea to apply a
transaction ID header that will enable analysts to trace a request
throughout its lifecycle. Note: there is no set naming standard for a
transaction ID header.

There are two common approaches to this: one is to request that the
consuming application generate a unique transaction ID and the provider
will capture it and respond with a corresponding correlation ID; the
second is to allow the provider to generate the transaction ID as close
to the edge of its domain as possible, and respond to the consuming
application with that transaction ID. In this case a consuming
application administrator or developer should capture and log that
transaction ID for audit purposes so that it can be relayed to agency
analysts if required.

**Example Request**

> #Request that includes a consuming application generated transaction
>
> #ID
>
> Request-Transaction-Id: c188cb0e-1a09-4184-890c-0f0bb2255425

**Example Response**

> #Response to a consuming application that provided a client generated
> #transaction ID
>
> Request-Transaction-Id: c188cb0e-1a09-4184-890c-0f0bb2255425
>
> Response-Correlation-Id: 514dbf50-4475-4e4d-86ee-e2001f158026
>
> #Response to a consuming application where there was no client
> #generated transaction ID
>
> #Note that the server has generated the transaction ID
>
> Response-Correlation-Id: c188cb0e-1a09-4184-890c-0f0bb2255425

## Response Headers

Response headers are supplied by the provider and must contain
Content-Type.

### Content-Type

**[Required]{.smallcaps}**

The Content-Type must be returned in the response, and indicate the
format type the response content is in e.g. Content-Type:
application/json. The Content-Type header should also include the
version of the API that processed the request e.g. Content-Type:
application/json,version=1.1

### Location

**[Recommended]{.smallcaps}**

Where a new resource item has been created (POST), the server should
respond with a 201 Created HTTP header and a Location header indicating
the URI of the newly created resource item e.g. Location:
https://api.example.govt.nz/v1/crown-property/198373

A location header should also be returned by a server when it sends a
3\*\* HTTP response, indicating a temporary or permanent redirection.

A location header can be, as recommended by this standard, absolute e.g.
Location: https://api.example.govt.nz/v1/crown-property/198373 or
relative e.g. Location: /v1/crown-property/198373

### Content-Location

**[Recommended]{.smallcaps}**

The Content-Location header indicates the location of the requested
resource. It should be an absolute and not a relative link.

**Example**

> #GET https://api.example.govt.nz/v1/crown-property/198373
>
> Content-Type: application/json
>
> Content-Location: https://api.example.govt.nz/v1/crown-property/198373
>
> {
>
> \"propertyid\": 12345,
>
> \"address1\": \"1 Some Street\",
>
> \"address2\": \"Some Suburb\",
>
> \"address3\": \"Some City\",
>
> \"address4\": null,
>
> \"country\": \"New Zealand\",
>
> \"postcode\": 1111,
>
> \"type\": \"commercial\"
>
> }

### Cache-Control

**[Recommended]{.smallcaps}**

It is important to consider caching when designing APIs, to ensure that
the APIs you build can perform at scale. The Cache-Control header is
only concerned with caching that occurs externally to the API layer.
Common examples may be client-side caching or caching within a Content
Delivery Network (CDN). This header should not be concerned with caching
mechanisms within the API layer such as response caches or object
caches, which require a different caching strategy.

The Cache-Control header is comprised of the following:

-   **private\|public**: This indicates if the cache is specific to the
    consumer or not -- a setting of private will prevent the cache from
    being persisted in a public cache.

-   **no-cache:** This instructs a cache to revalidate the resource
    every time**.**

-   **no-store:** This instructs a cache not to store the response. It
    also ensures that no part of the request is stored too.

-   **max-age:** This instructs the cache on expiry time. This can be
    used but it makes more sense to use the Expires header discussed
    below.

-   **s-max-age:** Similar to the above, however it refers to a shared
    cache hence only relevant to CDNs and other intermediary caches.

-   **must-revalidate:** This instructs the client to resend request
    headers and receive confirmation that the resource has not changed.

-   **proxy-revalidate:** Similar to the above, however specific to
    shared caches.

**Example**

> \# Example caching response
>
> HTTP/1.1 200 OK
>
> Date: Wed, 06 Jul 2016 21:14:52 GMT
>
> Expires: Wed, 06 Jul 2016 22:14:52 GMT
>
> Cache-Control: private,max-age=14400,must-revalidate
>
> Content-Type: application/json

Care should be taken when using caches, especially shared or public
caches. In some cases it may be more prudent to use the no-cache
directive to ensure that content is not cached outside your network.
This does not rule out caching within your API layer. For more
information on API caching please see [[section
2.12]{.underline}](#caching).

HTTP Cache Control standards can be found in [[Hypertext Transfer
Protocol (HTTP/1.1): Caching
RFC7234]{.underline}](https://tools.ietf.org/html/rfc7234)[^7]

### Expires

**[Recommended]{.smallcaps}**

When using Cache-Control you should include an Expires header in the
response for backward compatibility.

### ETag (Entity Tag)

**[Recommended]{.smallcaps}**

The ETag header is a concurrency control header, and when in a response
it is a tag that the consuming application can use when making a
subsequent request to a resource. Note that pre-condition handling is
not required, but where appropriate should be considered. Pre-condition
control can be a complex topic so in some cases the complexity may
eclipse the value.

> \# Response with ETag Header
>
> \# Consuming application would send this ETag in an If-None-Match
> #request header
>
> ETag: \"686897696a7c876b7e\"

## Custom X- HTTP Headers

X- notation headers have been deprecated as per
[[RFC6648]{.underline}](https://tools.ietf.org/html/rfc6648)[^8] and
should not be used. This is because the X- name often became a standard,
making the X-notation inaccurate (e.g. x-gzip became gzip) and requiring
support for both the X- and the non-X- notation. Common uses of the X-
headers are examples such as the X-HTTP-Method-Override header or the
X-Forwarded-For header.

Where an agency feels that a custom HTTP header is required that is not
available within the current HTTP standard they can use a custom header
without the X- prefix.

# Appendix C -- Example Interface Specification

The following illustrates a sample API Interface Specification. The
specification is written in Swagger and visualised here (for
readability) via a Confluence plugin however most API Developer Portal
products will support importing OpenAPI specifications.

![](media/image1.png){width="4.96875in" height="4.208333333333333in"}

[]{#_heading=h.33zd5kd .anchor}*Figure 52: Example Agency API -- delete
customer*

![](media/image5.png){width="5.010416666666667in"
height="4.770833333333333in"}

[]{#_heading=h.1j4nfs6 .anchor}*Figure 53: Example Agency API -- get
customer details*

![DIAAP-API-Spec-Part2](media/image11.png){width="4.9in" height="8.5in"}

[]{#_heading=h.434ayfz .anchor}*Figure 54: Example Agency API -- modify
customer*

![DIAAP-API-Spec-Part3](media/image8.png){width="4.4in" height="8.8in"}

[]{#_heading=h.2i9l8ns .anchor}*Figure 55: Example Agency API -- create
customer*

The raw JSON and YAML is below. This is best viewed via the Swagger
editor
[[http://editor.swagger.io/#/]{.underline}](http://editor.swagger.io/#/)

To view, simply open the OpenAPI editor as above and paste the contents
of the JSON or YAML examples into the editor window.

**JSON**

> {
>
> \"swagger\": \"2.0\",
>
> \"info\": {
>
> \"version\": \"2.0.0\",
>
> \"title\": \"Example Agency API\",
>
> \"description\": \"A sample API specification demonstrating OpenAPI
> capabilities - this is for example purposes only\",
>
> \"termsOfService\":
> \"https://developer.example.govt.nz/termsandconditions/\",
>
> \"contact\": {
>
> \"name\": \"Example Agency API team\",
>
> \"email\": \"exampleteam@api.govt.nz\",
>
> \"url\": \"https://agency.govt.nz\"
>
> }
>
> },
>
> \"host\": \"api.example.govt.nz\",
>
> \"basePath\": \"/v2\",
>
> \"paths\": {
>
> \"/customers/{customerId}\": {
>
> \"get\": {
>
> \"parameters\": \[
>
> {
>
> \"name\": \"customerId\",
>
> \"in\": \"path\",
>
> \"description\": \"Unique ID of customer\",
>
> \"required\": true,
>
> \"type\": \"string\"
>
> }
>
> \],
>
> \"tags\": \[
>
> \"get customer details\"
>
> \],
>
> \"description\": \"Returns details for a customer given a unique
> customer ID\\n\",
>
> \"security\": \[
>
> {
>
> \"AuthorizationCode\": \[
>
> \"customerRead\"
>
> \]
>
> }
>
> \],
>
> \"produces\": \[
>
> \"application/json\"
>
> \],
>
> \"responses\": {
>
> \"200\": {
>
> \"description\": \"OK - Successful\",
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/customerDetailsResponse\"
>
> }
>
> },
>
> \"default\": {
>
> \"description\": \"Error response\",
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/errorModel\"
>
> }
>
> }
>
> }
>
> },
>
> \"put\": {
>
> \"tags\": \[
>
> \"modify customer\"
>
> \],
>
> \"description\": \"Updates a customer's details\",
>
> \"consumes\": \[
>
> \"application/json\"
>
> \],
>
> \"produces\": \[
>
> \"application/json\"
>
> \],
>
> \"parameters\": \[
>
> {
>
> \"name\": \"customerId\",
>
> \"in\": \"path\",
>
> \"description\": \"Unique ID of customer\",
>
> \"required\": true,
>
> \"type\": \"string\"
>
> },
>
> {
>
> \"name\": \"body\",
>
> \"in\": \"body\",
>
> \"required\": true,
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/customerRequestModel\"
>
> }
>
> }
>
> \],
>
> \"responses\": {
>
> \"200\": {
>
> \"description\": \"Updated resource successfully\"
>
> },
>
> \"default\": {
>
> \"description\": \"Error response\",
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/errorModel\"
>
> }
>
> }
>
> },
>
> \"security\": \[
>
> {
>
> \"AuthorizationCode\": \[
>
> \"customerWrite\"
>
> \]
>
> }
>
> \]
>
> },
>
> \"delete\": {
>
> \"tags\": \[
>
> \"delete customer\"
>
> \],
>
> \"description\": \"Deletes an existing customer resource\",
>
> \"consumes\": \[
>
> \"application/json\"
>
> \],
>
> \"produces\": \[
>
> \"application/json\"
>
> \],
>
> \"parameters\": \[
>
> {
>
> \"name\": \"customerId\",
>
> \"in\": \"path\",
>
> \"description\": \"Unique ID of customer\",
>
> \"required\": true,
>
> \"type\": \"string\"
>
> }
>
> \],
>
> \"responses\": {
>
> \"200\": {
>
> \"description\": \"Deleted resource successfully\"
>
> },
>
> \"default\": {
>
> \"description\": \"Error response\",
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/errorModel\"
>
> }
>
> }
>
> },
>
> \"security\": \[
>
> {
>
> \"AuthorizationCode\": \[
>
> \"customerDelete\"
>
> \]
>
> }
>
> \]
>
> }
>
> },
>
> \"/customers\": {
>
> \"post\": {
>
> \"tags\": \[
>
> \"create customer\"
>
> \],
>
> \"description\": \"Creates a new customer. API will create a customer
> resource and, if successful, return a hyperlink to the created
> resource\",
>
> \"consumes\": \[
>
> \"application/json\"
>
> \],
>
> \"produces\": \[
>
> \"application/json\"
>
> \],
>
> \"parameters\": \[
>
> {
>
> \"name\": \"body\",
>
> \"in\": \"body\",
>
> \"required\": true,
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/customerRequestModel\"
>
> }
>
> }
>
> \],
>
> \"responses\": {
>
> \"201\": {
>
> \"description\": \"Created resource successfully\",
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/\_links\"
>
> }
>
> },
>
> \"default\": {
>
> \"description\": \"Error response\",
>
> \"schema\": {
>
> \"\$ref\": \"#/definitions/errorModel\"
>
> }
>
> }
>
> },
>
> \"security\": \[
>
> {
>
> \"AuthorizationCode\": \[
>
> \"customerCreate\"
>
> \]
>
> }
>
> \]
>
> }
>
> }
>
> },
>
> \"securityDefinitions\": {
>
> \"AuthorizationCode\": {
>
> \"type\": \"oauth2\",
>
> \"scopes\": {
>
> \"customerRead\": \"Grants read access to a customer resource\",
>
> \"customerWrite\": \"Grants write (update) access to an existing
> customer resource\",
>
> \"customerCreate\": \"Grants access to create a new customer
> resource\",
>
> \"customerDelete\": \"Grants access to delete an existing customer
> resource\"
>
> },
>
> \"flow\": \"accessCode\",
>
> \"authorizationUrl\": \"https://idm.example.govt.nz/oauth/authorize\",
>
> \"tokenUrl\": \"https://idm.example.govt.nz/oauth/access_token\"
>
> }
>
> },
>
> \"definitions\": {
>
> \"customerRequestModel\": {
>
> \"type\": \"object\",
>
> \"properties\": {
>
> \"names\": {
>
> \"type\": \"object\",
>
> \"properties\": {
>
> \"firstName\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers first name\"
>
> },
>
> \"middleName\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers middle name\"
>
> },
>
> \"lastName\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers last name\"
>
> },
>
> \"salutation\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers salutation - e.g. Mr John Doe\"
>
> },
>
> \"title\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers title - e.g. Ms, Mr, Mrs, Dr etc.\"
>
> }
>
> }
>
> },
>
> \"addresses\": {
>
> \"type\": \"array\",
>
> \"description\": \"An array of addresses. Unpopulated properties or
> items will be returned as null JSON objects.\",
>
> \"items\": {
>
> \"properties\": {
>
> \"addressType\": {
>
> \"type\": \"string\",
>
> \"description\": \"Address type - e.g. Home, Business\"
>
> },
>
> \"address1\": {
>
> \"type\": \"string\",
>
> \"description\": \"First line of the address e.g. 2 something street\"
>
> },
>
> \"address2\": {
>
> \"type\": \"string\",
>
> \"description\": \"Second line of address e.g. Khandallah\"
>
> },
>
> \"address3\": {
>
> \"type\": \"string\",
>
> \"description\": \"Third line of address e.g. Wellington\"
>
> },
>
> \"address4\": {
>
> \"type\": \"string\"
>
> },
>
> \"country\": {
>
> \"type\": \"string\",
>
> \"description\": \"This is a human readable country name e.g. New
> Zealand and not a country code\"
>
> }
>
> }
>
> }
>
> }
>
> }
>
> },
>
> \"customerDetailsResponse\": {
>
> \"type\": \"object\",
>
> \"required\": \[
>
> \"customerId\"
>
> \],
>
> \"properties\": {
>
> \"customerId\": {
>
> \"type\": \"string\",
>
> \"description\": \"Unique identifier for the customer resource - GUID
> format\"
>
> },
>
> \"names\": {
>
> \"type\": \"object\",
>
> \"properties\": {
>
> \"firstName\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers first name\"
>
> },
>
> \"middleName\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers middle name\"
>
> },
>
> \"lastName\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers last name\"
>
> },
>
> \"salutation\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers salutation - e.g. Mr John Doe\"
>
> },
>
> \"title\": {
>
> \"type\": \"string\",
>
> \"description\": \"Customers title - e.g. Ms, Mr, Mrs, Dr etc.\"
>
> }
>
> }
>
> },
>
> \"addresses\": {
>
> \"type\": \"array\",
>
> \"description\": \"An array of addresses. Unpopulated properties or
> items will be returned as null JSON objects.\",
>
> \"items\": {
>
> \"properties\": {
>
> \"addressType\": {
>
> \"type\": \"string\",
>
> \"description\": \"Address type - e.g. Home, Business\"
>
> },
>
> \"address1\": {
>
> \"type\": \"string\",
>
> \"description\": \"First line of the address e.g. 2 something street\"
>
> },
>
> \"address2\": {
>
> \"type\": \"string\",
>
> \"description\": \"Second line of address e.g. Khandallah\"
>
> },
>
> \"address3\": {
>
> \"type\": \"string\",
>
> \"description\": \"Third line of address e.g. Wellington\"
>
> },
>
> \"address4\": {
>
> \"type\": \"string\"
>
> },
>
> \"country\": {
>
> \"type\": \"string\",
>
> \"description\": \"This is a human readable country name e.g. New
> Zealand and not a country code\"
>
> }
>
> }
>
> }
>
> },
>
> \"\_links\": {
>
> \"type\": \"array\",
>
> \"description\": \"An array of related links relevant to the
> request/response.\",
>
> \"items\": {
>
> \"properties\": {
>
> \"rel\": {
>
> \"type\": \"string\",
>
> \"description\": \"A piece of information providing context for the
> link - e.g. self or accounts.\"
>
> },
>
> \"href\": {
>
> \"type\": \"string\",
>
> \"description\": \"A fully qualified URL to the resource.\"
>
> }
>
> }
>
> }
>
> }
>
> }
>
> },
>
> \"errorModel\": {
>
> \"type\": \"object\",
>
> \"properties\": {
>
> \"errors\": {
>
> \"type\": \"array\",
>
> \"items\": {
>
> \"description\": \"An array of error items containing error codes and
> descriptions. Note that the error descriptions will be normalised.\",
>
> \"properties\": {
>
> \"code\": {
>
> \"type\": \"integer\",
>
> \"format\": \"int32\",
>
> \"description\": \"An error code - should be used in conjunction with
> the HTPP response code.\"
>
> },
>
> \"description\": {
>
> \"type\": \"string\",
>
> \"description\": \"A short description of the error.\"
>
> }
>
> }
>
> }
>
> },
>
> \"\_links\": {
>
> \"type\": \"array\",
>
> \"items\": {
>
> \"properties\": {
>
> \"rel\": {
>
> \"type\": \"string\",
>
> \"description\": \"The relationship to the request e.g. self which
> contains the resource that was requested or {object name}, a link to a
> resource that is related to the requested resource\"
>
> },
>
> \"href\": {
>
> \"type\": \"string\",
>
> \"description\": \"A link to the related resource. In an error
> scenario this is likely to be something such as a link to a support
> portal.\"
>
> }
>
> }
>
> }
>
> }
>
> }
>
> },
>
> \"\_links\": {
>
> \"type\": \"array\",
>
> \"items\": {
>
> \"properties\": {
>
> \"rel\": {
>
> \"type\": \"string\",
>
> \"description\": \"The relationship to the request e.g. self which
> contains the resource that was requested or {object name}, a link to a
> resource that is related to the requested resource\"
>
> },
>
> \"href\": {
>
> \"type\": \"string\",
>
> \"description\": \"A link to the related resource\"
>
> }
>
> }
>
> }
>
> }
>
> }
>
> }

**YAML**

**OpenAPI 3.0**

> openapi: 3.0.0
>
> info:
>
> version: 2.0.0
>
> title: Example Agency API
>
> description: A sample API specification demonstrating OpenAPI
> capabilities - this is for
>
> example purposes only
>
> termsOfService: https:// api.example.govt.nz/termsandconditions/
>
> contact:
>
> name: Example Agency API team
>
> email: exampleteam@api.govt.nz
>
> url: https://agency.govt.nz
>
> paths:
>
> \"/customers/{customerId}\":
>
> get:
>
> parameters:
>
> \- name: customerId
>
> in: path
>
> description: Unique ID of customer
>
> required: true
>
> schema:
>
> type: string
>
> tags:
>
> \- get customer details
>
> description: \|
>
> Returns details for a customer given a unique customer ID
>
> security:
>
> \- AuthorizationCode:
>
> \- customerRead
>
> responses:
>
> \"200\":
>
> description: OK - Successful
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/customer\"
>
> default:
>
> description: Error response
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/errorModel\"
>
> put:
>
> tags:
>
> \- modify customer
>
> description: Updates a customer's details
>
> parameters:
>
> \- name: customerId
>
> in: path
>
> description: Unique ID of customer
>
> required: true
>
> schema:
>
> type: string
>
> requestBody:
>
> \$ref: \"#/components/requestBodies/customer\"
>
> responses:
>
> \"200\":
>
> description: Updated resource successfully
>
> default:
>
> description: Error response
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/errorModel\"
>
> security:
>
> \- AuthorizationCode:
>
> \- customerWrite
>
> delete:
>
> tags:
>
> \- delete customer
>
> description: Deletes an existing customer resource
>
> parameters:
>
> \- name: customerId
>
> in: path
>
> description: Unique ID of customer
>
> required: true
>
> schema:
>
> type: string
>
> responses:
>
> \"200\":
>
> description: Deleted resource successfully
>
> default:
>
> description: Error response
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/errorModel\"
>
> security:
>
> \- AuthorizationCode:
>
> \- customerDelete
>
> /customers:
>
> post:
>
> tags:
>
> \- create customer
>
> description: Creates a new customer. API will create a customer
> resource and, if
>
> successful, return a hyperlink to the created resource
>
> requestBody:
>
> \$ref: \"#/components/requestBodies/customer\"
>
> responses:
>
> \"201\":
>
> description: Created resource successfully
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/\_links\"
>
> default:
>
> description: Error response
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/errorModel\"
>
> security:
>
> \- AuthorizationCode:
>
> \- customerCreate
>
> servers:
>
> \- url: https:// api.example.govt.nz/v2
>
> components:
>
> parameters:
>
> Authorization:
>
> description: For demonstration purposes only - this should not be
> required in most
>
> situations as OAuth Authorization Code grant type implicity indicates
>
> this.
>
> name: Authorization
>
> in: header
>
> required: true
>
> schema:
>
> type: string
>
> default: \"Bearer \"
>
> requestBodies:
>
> customer:
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/customer\"
>
> required: true
>
> securitySchemes:
>
> AuthorizationCode:
>
> type: oauth2
>
> flows:
>
> authorizationCode:
>
> authorizationUrl: https:// api.example.govt.nz/web
>
> tokenUrl: https:// api.example.govt.nz/oauth2/token
>
> scopes:
>
> customerRead: Grants read access to a customer resource
>
> customerWrite: Grants write (update) access to an existing customer
> resource
>
> customerCreate: Grants access to create a new customer resource
>
> customerDelete: Grants access to delete an existing customer resource
>
> schemas:
>
> customer:
>
> type: object
>
> properties:
>
> customerId:
>
> type: string
>
> description: Unique identifier for the customer resource - GUID format
>
> readOnly: true
>
> names:
>
> type: object
>
> properties:
>
> firstName:
>
> type: string
>
> description: Customers first name
>
> example: Swithin
>
> middleName:
>
> type: string
>
> description: Customers middle name
>
> example: Henry
>
> lastName:
>
> type: string
>
> description: Customers last name
>
> example: Foote
>
> salutation:
>
> type: string
>
> description: Customers salutation - e.g. Mr John Doe
>
> example: Mr Swithin Henry Foote
>
> title:
>
> type: string
>
> description: Customers title - e.g. Ms, Mr, Mrs, Dr etc.
>
> example: Mr
>
> addresses:
>
> type: array
>
> description: An array of addresses. Unpopulated properties or items
> will be
>
> returned as null JSON objects.
>
> items:
>
> properties:
>
> addressType:
>
> type: string
>
> description: Address type - e.g. Home, Business
>
> example: Home
>
> address1:
>
> type: string
>
> description: First line of the address e.g. 2 something street
>
> example: 2 Queens Drive
>
> address2:
>
> type: string
>
> description: Second line of address e.g. Khandallah
>
> example: Khandallah
>
> address3:
>
> type: string
>
> description: Third line of address e.g. Wellington
>
> example: Wellington
>
> address4:
>
> type: string
>
> country:
>
> type: string
>
> description: This is a human readable country name e.g. New Zealand
> and not
>
> a country code
>
> example: New Zealand
>
> \_links:
>
> type: array
>
> readOnly: true
>
> description: An array of related links relevant to the
> request/response.
>
> items:
>
> properties:
>
> rel:
>
> type: string
>
> description: A piece of information providing context for the link -
> e.g.
>
> self or accounts.
>
> href:
>
> type: string
>
> description: A fully qualified URL to the resource.
>
> errorModel:
>
> type: object
>
> properties:
>
> errors:
>
> type: array
>
> items:
>
> description: An array of error items containing error codes and
> descriptions.
>
> Note that the error descriptions will be normalised.
>
> properties:
>
> code:
>
> type: integer
>
> format: int32
>
> description: An error code - should be used in conjunction with the
> HTPP
>
> response code.
>
> description:
>
> type: string
>
> description: A short description of the error.
>
> \_links:
>
> type: array
>
> items:
>
> properties:
>
> rel:
>
> type: string
>
> description: The relationship to the request e.g. self which contains
> the
>
> resource that was requested or {object name}, a link to a
>
> resource that is related to the requested resource
>
> href:
>
> type: string
>
> description: A link to the related resource. In an error scenario this
> is
>
> likely to be something such as a link to a support portal.
>
> \_links:
>
> type: array
>
> items:
>
> properties:
>
> rel:
>
> type: string
>
> description: The relationship to the request e.g. self which contains
> the
>
> resource that was requested or {object name}, a link to a resource
>
> that is related to the requested resource
>
> href:
>
> type: string
>
> description: A link to the related resource

**Swagger 2.0**

> #Example API Specification for Agency X
>
> #Author Swithin Foote Middleware New Zealand
>
> swagger: \'2.0\'
>
> info:
>
> version: 2.0.0
>
> title: Example Agency API
>
> description: A sample API specification demonstrating OpenAPI
> capabilities - this is for example purposes only
>
> termsOfService: https://developer.example.govt.nz/termsandconditions/
>
> contact:
>
> name: Example Agency API team
>
> email: exampleteam@api.govt.nz
>
> url: https://agency.govt.nz
>
> host: api.example.govt.nz
>
> basePath: /v2
>
> paths:
>
> /customers/{customerId}:
>
> get:
>
> parameters:
>
> \- name: customerId
>
> in: path
>
> description: Unique ID of customer
>
> required: true
>
> type: string
>
> tags:
>
> \- get customer details
>
> description: \|
>
> Returns details for a customer given a unique customer ID
>
> security:
>
> \- AuthorizationCode:
>
> \- customerRead
>
> produces:
>
> \- application/json
>
> responses:
>
> 200:
>
> description: OK - Successful
>
> schema:
>
> \$ref: \'#/definitions/customerDetailsResponse\'
>
> default:
>
> description: Error response
>
> schema:
>
> \$ref: \'#/definitions/errorModel\'
>
> put:
>
> tags:
>
> \- modify customer
>
> description: Updates a customer's details
>
> consumes:
>
> \- application/json
>
> produces:
>
> \- application/json
>
> parameters:
>
> \- name: customerId
>
> in: path
>
> description: Unique ID of customer
>
> required: true
>
> type: string
>
> \- name: body
>
> in: body
>
> required: true
>
> schema:
>
> \$ref: \"#/definitions/customerRequestModel\"
>
> responses:
>
> 200:
>
> description: Updated resource successfully
>
> default:
>
> description: Error response
>
> schema:
>
> \$ref: \'#/definitions/errorModel\'
>
> security:
>
> \- AuthorizationCode:
>
> \- customerWrite
>
> delete:
>
> tags:
>
> \- delete customer
>
> description: Deletes an existing customer resource
>
> consumes:
>
> \- application/json
>
> produces:
>
> \- application/json
>
> parameters:
>
> \- name: customerId
>
> in: path
>
> description: Unique ID of customer
>
> required: true
>
> type: string
>
> responses:
>
> 200:
>
> description: Deleted resource successfully
>
> default:
>
> description: Error response
>
> schema:
>
> \$ref: \'#/definitions/errorModel\'
>
> security:
>
> \- AuthorizationCode:
>
> \- customerDelete
>
> /customers:
>
> post:
>
> tags:
>
> \- create customer
>
> description: Creates a new customer. API will create a customer
> resource and, if successful, return a hyperlink to the created
> resource
>
> consumes:
>
> \- application/json
>
> produces:
>
> \- application/json
>
> parameters:
>
> \- name: body
>
> in: body
>
> required: true
>
> schema:
>
> \$ref: \"#/definitions/customerRequestModel\"
>
> responses:
>
> 201:
>
> description: Created resource successfully
>
> schema:
>
> \$ref: \'#/definitions/\_links\'
>
> default:
>
> description: Error response
>
> schema:
>
> \$ref: \'#/definitions/errorModel\'
>
> security:
>
> \- AuthorizationCode:
>
> \- customerCreate
>
> securityDefinitions:
>
> AuthorizationCode:
>
> type: oauth2
>
> scopes:
>
> customerRead: Grants read access to a customer resource
>
> customerWrite: Grants write (update) access to an existing customer
> resource
>
> customerCreate: Grants access to create a new customer resource
>
> customerDelete: Grants access to delete an existing customer resource
>
> flow: accessCode
>
> authorizationUrl: https://idm.example.govt.nz/oauth/authorize
>
> tokenUrl: https://idm.example.govt.nz/oauth/access_token
>
> definitions:
>
> customerRequestModel:
>
> type: object
>
> properties:
>
> names:
>
> type: object
>
> properties:
>
> firstName:
>
> type: string
>
> description: Customers first name
>
> middleName:
>
> type: string
>
> description: Customers middle name
>
> lastName:
>
> type: string
>
> description: Customers last name
>
> salutation:
>
> type: string
>
> description: Customers salutation - e.g. Mr John Doe
>
> title:
>
> type: string
>
> description: Customers title - e.g. Ms, Mr, Mrs, Dr etc.
>
> addresses:
>
> type: array
>
> description: An array of addresses. Unpopulated properties or items
> will be returned as null JSON objects.
>
> items:
>
> properties:
>
> addressType:
>
> type: string
>
> description: Address type - e.g. Home, Business
>
> address1:
>
> type: string
>
> description: First line of the address e.g. 2 something street
>
> address2:
>
> type: string
>
> description: Second line of address e.g. Khandallah
>
> address3:
>
> type: string
>
> description: Third line of address e.g. Wellington
>
> address4:
>
> type: string
>
> country:
>
> type: string
>
> description: This is a human readable country name e.g. New Zealand
> and not a country code
>
> customerDetailsResponse:
>
> type: object
>
> required:
>
> \- customerId
>
> properties:
>
> customerId:
>
> type: string
>
> description: Unique identifier for the customer resource - GUID format
>
> names:
>
> type: object
>
> properties:
>
> firstName:
>
> type: string
>
> description: Customers first name
>
> middleName:
>
> type: string
>
> description: Customers middle name
>
> lastName:
>
> type: string
>
> description: Customers last name
>
> salutation:
>
> type: string
>
> description: Customers salutation - e.g. Mr John Doe
>
> title:
>
> type: string
>
> description: Customers title - e.g. Ms, Mr, Mrs, Dr etc.
>
> addresses:
>
> type: array
>
> description: An array of addresses. Unpopulated properties or items
> will be returned as null JSON objects.
>
> items:
>
> properties:
>
> addressType:
>
> type: string
>
> description: Address type - e.g. Home, Business
>
> address1:
>
> type: string
>
> description: First line of the address e.g. 2 something street
>
> address2:
>
> type: string
>
> description: Second line of address e.g. Khandallah
>
> address3:
>
> type: string
>
> description: Third line of address e.g. Wellington
>
> address4:
>
> type: string
>
> country:
>
> type: string
>
> description: This is a human readable country name e.g. New Zealand
> and not a country code
>
> \_links:
>
> type: array
>
> description: An array of related links relevant to the
> request/response.
>
> items:
>
> properties:
>
> rel:
>
> type: string
>
> description: A piece of information providing context for the link -
> e.g. self or accounts.
>
> href:
>
> type: string
>
> description: A fully qualified URL to the resource.
>
> errorModel:
>
> type: object
>
> properties:
>
> errors:
>
> type: array
>
> items:
>
> description: An array of error items containing error codes and
> descriptions. Note that the error descriptions will be normalised.
>
> properties:
>
> code:
>
> type: integer
>
> format: int32
>
> description: An error code - should be used in conjunction with the
> HTPP response code.
>
> description:
>
> type: string
>
> description: A short description of the error.
>
> \_links:
>
> type: array
>
> items:
>
> properties:
>
> rel:
>
> type: string
>
> description: The relationship to the request e.g. self which contains
> the resource that was requested or {object name}, a link to a resource
> that is related to the requested resource
>
> href:
>
> type: string
>
> description: A link to the related resource. In an error scenario this
> is likely to be something such as a link to a support portal.
>
> \_links:
>
> type: array
>
> items:
>
> properties:
>
> rel:
>
> type: string
>
> description: The relationship to the request e.g. self which contains
> the resource that was requested or {object name}, a link to a resource
> that is related to the requested resource
>
> href:
>
> type: string
>
> description: A link to the related resource

[]{#_heading=h.xevivl .anchor}

# Appendix D - Synchronous/Asynchronous Example Specifications

**OpenAPI 3.0**

To visualise paste content below into the OpenAPI editor here
[[https://editor.swagger.io/]{.underline}](https://editor.swagger.io/)

> openapi: 3.0.0
>
> info:
>
> version: 1.0.0
>
> title: Example Agency Claims API
>
> description: A sample API specification demonstrating OpenAPI
> capabilities - this is for
>
> example purposes only
>
> termsOfService: https:// api.example.govt.nz/termsandconditions/
>
> contact:
>
> name: Example Agency API team
>
> email: exampleteam@api.govt.nz
>
> url: https://agency.govt.nz
>
> paths:
>
> \"/claims\":
>
> get:
>
> description: Retrieve details of a claim
>
> tags:
>
> \- get claim
>
> security:
>
> \- AuthorizationCode:
>
> \- read:claims
>
> responses:
>
> 200:
>
> description: OK
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/claims\"
>
> post:
>
> description: Create a claim
>
> tags:
>
> \- Create CLaim
>
> security:
>
> \- AuthorizationCode:
>
> \- write:claims
>
> requestBody:
>
> \$ref: \"#/components/schemas/createClaim\"
>
> responses:
>
> \"201\":
>
> description: Created
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/claims\"
>
> default:
>
> description: Error response
>
> content:
>
> application/json:
>
> schema:
>
> \$ref: \"#/components/schemas/errorModel\"
>
> components:
>
> securitySchemes:
>
> AuthorizationCode:
>
> type: oauth2
>
> flows:
>
> authorizationCode:
>
> authorizationUrl: https:// api.example.govt.nz/web
>
> tokenUrl: https:// api.example.govt.nz/oauth2/token
>
> scopes:
>
> read:claims: Grants read access to a claim resource
>
> write:claims: Grants write (update) access to an existing claims
> resource
>
> schemas:
>
> createClaim:
>
> description: Create Claim Model
>
> type: object
>
> properties:
>
> customerName:
>
> type: string
>
> example: \"John Henry Ford\"
>
> claimDetail:
>
> type: string
>
> description: Claims details
>
> example: This is a long string describing the claim for
> evaluation\...\...
>
> claims:
>
> description: Claim Response Model
>
> type: object
>
> properties:
>
> claimId:
>
> type: string
>
> format: uuid
>
> description: Unique identifier for the claim
>
> description:
>
> type: string
>
> description: A short description of the claim
>
> status:
>
> type: string
>
> enum: \[\"PROCESSING\",\"REJECTED\",\"ACCEPTED\"\]
>
> claimUri:
>
> type: string
>
> description: Resource identifier for the claim
>
> example: \"https://api.exampleagency.govt.nz/claims/{claimId}\"
>
> errorModel:
>
> type: object
>
> properties:
>
> errors:
>
> type: array
>
> items:
>
> description: An array of error items containing error codes and
> descriptions.
>
> Note that the error descriptions will be normalised.
>
> properties:
>
> code:
>
> type: integer
>
> format: int32
>
> description: An error code - should be used in conjunction with the
> HTPP
>
> response code.
>
> description:
>
> type: string
>
> description: A short description of the error.
>
> \_links:
>
> type: array
>
> items:
>
> properties:
>
> rel:
>
> type: string
>
> description: The relationship to the request e.g. self which contains
> the
>
> resource that was requested or {object name}, a link to a
>
> resource that is related to the requested resource
>
> href:
>
> type: string
>
> description: A link to the related resource. In an error scenario this
> is
>
> likely to be something such as a link to a support portal.

**AsyncAPI 2.0**

To visualise paste content below into the AsyncAPI playground here
[[https://playground.asyncapi.io]{.underline}](https://playground.asyncapi.io)

> asyncapi: 2.0.0
>
> info:
>
> title: Claims Notifications
>
> version: 1.0.0
>
> description: This channel provides claim information and status
> notifications
>
> servers:
>
> production:
>
> url: broker.exampleagency.govt.nz
>
> protocol: amqps,secure-mqtt,https
>
> description: This is \"Example Agencies\" broker.
>
> security:
>
> \- oauth2: \[\]
>
> channels:
>
> claims/{claimId}:
>
> publish:
>
> message:
>
> \$ref: \'#/components/messages/claim\'
>
> parameters:
>
> claimId:
>
> description: Unique identifier for the claim
>
> schema:
>
> type: string
>
> format: uuid
>
> subscribe:
>
> message:
>
> \$ref: \'#/components/messages/claim\'
>
> components:
>
> messages:
>
> claim:
>
> payload:
>
> type: object
>
> properties:
>
> claimId:
>
> type: string
>
> format: uuid
>
> description: Unique identifier for the claim
>
> description:
>
> type: string
>
> description: A short description of the claim
>
> status:
>
> type: string
>
> enum: \[\"PROCESSING\",\"REJECTED\",\"ACCEPTED\"\]
>
> claimUri:
>
> type: string
>
> description: Resource identifier for the claim
>
> example: \"https://api.exampleagency.govt.nz/claims/{claimId}\"
>
> securitySchemes:
>
> user-password:
>
> type: userPassword
>
> oauth2:
>
> type: oauth2
>
> description: OAuth2 identity service for \"Example Agency\"
>
> flows:
>
> authorizationCode:
>
> authorizationUrl: https://api.exampleagency.govt.nz/oauth/authorize
>
> tokenUrl: https://api.exampleagency.govt.nz/oauth/token
>
> scopes:
>
> read:claims: Read details of claims

[]{#_heading=h.3hej1je .anchor}

# Appendix E - Standards for Developing APIs

Standards for Developing APIs

In addition to the security standards captured in Part-B the table below
captures (current) API and web standards that should be considered as
part of any API Strategy.

Refer to the [[Government digital
standards]{.underline}](https://www.digital.govt.nz/standards-and-guidance/technology-and-architecture/government-enterprise-architecture/government-digital-standards-catalogue/)
catalogue for recommended standards and their current state.

+---------------+------------------------------------------------------+
| Standard or   | Description                                          |
| Standards     |                                                      |
| Organisation  |                                                      |
+===============+======================================================+
| OpenAPI       | The OpenAPI Specification defines a standard,        |
|               | language-agnostic interface to RESTful APIs which    |
|               | allows both humans and computers to discover and     |
|               | understand the capabilities of the service without   |
|               | access to source code, documentation, or through     |
|               | network traffic inspection.                          |
+---------------+------------------------------------------------------+
| AsyncAPI      | AsyncAPI is an open source initiative that seeks to  |
|               | improve the current state of Event-Driven            |
|               | Architectures (EDA). Their long-term goal is to make |
|               | working with EDAs as easy as it is to work with REST |
|               | APIs.                                                |
+---------------+------------------------------------------------------+
| HTTP          | HTTP stands for Hyper Text Transfer Protocol.        |
|               | Communication between client computers and web       |
|               | servers is done by sending HTTP Requests and         |
|               | receiving HTTP Responses. In practice, most RESTful  |
|               | APIs use HTTP as a transport layer and rely on the   |
|               | use of HTTP verbs, like POST, GET, PUT and DELETE.   |
+---------------+------------------------------------------------------+
| OAuth2/OIDC   | The OAuth 2.0 Authorization Framework (OAuth2) is an |
|               | industry standard framework that enables third       |
|               | parties limited access to protected resources and is |
|               | commonly used authorisation approach for APIs. Open  |
|               | ID Connect (OIDC) is an identity layer on top of     |
|               | OAuth2 that allows consuming applications to request |
|               | information about authenticated sessions and end     |
|               | users.                                               |
+---------------+------------------------------------------------------+
| JSON/JSON     | JavaScript Object Notation (JSON) is an open         |
| Schema        | standard for a lightweight format for storing and    |
|               | transporting data. It is a \"self-describing\"       |
|               | notation and is easy for both humans and computers   |
|               | to understand.                                       |
+---------------+------------------------------------------------------+
| JWT/JW        | These are a set of open standards for securely       |
| S/JWE/JWK/JWA | transmitting information between systems using JSON. |
|               | They include the data structure a web token (JWT),   |
|               | how to sign a JWT (JWS), how to encrypt a JWT (JWE), |
|               | and some JSON cryptography practices (JWK and JWA)   |
+---------------+------------------------------------------------------+
| Fast          | [FHIR is a an industry standard for exchanging       |
| Healthcare    | healthcare information electronically. It was        |
| Int           | developed by the HL-7 standards                      |
| eroperability | organisation.]{.mark}                                |
| Resources     |                                                      |
| (FHIR)        |                                                      |
+---------------+------------------------------------------------------+
| Payments New  | The PNZ API Centre standards is an industry standard |
| Zealand (PNZ) | for Open Banking. The security profile is quite      |
| API Centre    | interesting in regards to capturing customer consent |
| Standards     | for third parties to act on their behalf.            |
+---------------+------------------------------------------------------+
| SOAP          | This standard is Deprecated for NZ Government - GEAG |
|               | has determined that the standard should not be used  |
|               | for new work, but may still be in use for existing   |
|               | APIs.                                                |
+---------------+------------------------------------------------------+
| Financial     | Another industry standard for the financial sector.  |
| Grade API     | It is an example of good security profile practices. |
| (FAPI)        |                                                      |
| Security      |                                                      |
| Profile       |                                                      |
+---------------+------------------------------------------------------+
| Pan European  | Peppol is a global standardised framework that       |
| Public        | enables businesses to exchange procurement documents |
| Procurement   | electronically. To do this, Peppol provides and      |
| Online        | maintains artefacts and specifications to make it    |
| (Peppol)      | possible for businesses using different systems to   |
|               | 'speak' to each other.                               |
|               |                                                      |
|               | The use of Peppol is governed by a multi-lateral     |
|               | agreement structure, owned and maintained by         |
|               | OpenPeppol.                                          |
+---------------+------------------------------------------------------+
| Internet      | The IETF is a large open international community     |
| Engineering   | concerned with the evolution of the Internet         |
| Task Force    | architecture and the smooth operation of the         |
| (IETF)        | Internet. Their mission is to make the Internet work |
|               | better by producing high quality, relevant technical |
|               | documents that influence the way people design, use, |
|               | and manage the Internet. Many of the standards       |
|               | listed above were developed through the IETF.        |
+---------------+------------------------------------------------------+
| Standards New | A business unit within the Ministry of Business,     |
| Zealand       | Innovation and Employment, which specialises in      |
|               | managing the development of standards. They also     |
|               | publish and sell NZ, joint Australia-NZ, and         |
|               | international standards.                             |
+---------------+------------------------------------------------------+
| Stats NZ:     | Information about the standards and classifications  |
| Standards and | Stats NZ use and maintain, news about reviews, and   |
| cl            | tools to help classify and code responses.           |
| assifications |                                                      |
+---------------+------------------------------------------------------+
| Health        | This organisation supports and promotes the          |
| Information   | development and adoption of fit-for-purpose health   |
| Standards     | information standards for the NZ health system.      |
| Organisation  |                                                      |
| (HISO)        |                                                      |
+---------------+------------------------------------------------------+
| Data Content  | There is a documented set of government data content |
| Requirements  | requirements -                                       |
|               | [[https://www.data.govt.nz/manage-data/d             |
|               | ata-content-standardisation/register-of-government-d |
|               | ata-content-requirements/]{.underline}](https://www. |
|               | data.govt.nz/manage-data/data-content-standardisatio |
|               | n/register-of-government-data-content-requirements/) |
+---------------+------------------------------------------------------+

[]{#_heading=h.4gjguf0 .anchor}Table 25: Standards for Developing APIs

[^1]: [https://tools.ietf.org/html/rfc6648]{.underline}

[^2]: [[https://www.hl7.org/fhir/patient.html]{.underline}](https://www.hl7.org/fhir/patient.html)

[^3]: [https://tools.ietf.org/html/rfc7159]{.underline}

[^4]: *See
    [[https://devportal.yaas.io/tools/apibestpractices/index.html#BatchProcessing]{.underline}](https://devportal.yaas.io/tools/apibestpractices/index.html#BatchProcessing)
    for best practice*

[^5]: *See
    [[https://restlet.com/http-status-codes-map]{.underline}](https://restlet.com/http-status-codes-map)
    for a map of HTTP Status Codes*

[^6]: *See
    [[https://www.owasp.org/index.php/Top_10_2007-Information_Leakage_and_Improper_Error_Handling]{.underline}](https://www.owasp.org/index.php/Top_10_2007-Information_Leakage_and_Improper_Error_Handling)*

[^7]: https://tools.ietf.org/html/rfc7234

[^8]: [https://tools.ietf.org/html/rfc6648]{.underline}
