
# Introduction

The Strategy for a Digital Public Service is "a call to action for the
public service to operate in the digital world, in a more modern and
efficient way --- delivering the outcomes that Aotearoa New Zealand
needs."

It envisions a future where agencies prioritise the creation of open
Application Programming Interfaces (APIs) to enable reuse of data,
transactions and rules, which, in turn, creates an opportunity for
greater cooperation and interoperability between agencies, to
dramatically improve service design and delivery.

Agencies need focused guidance, approaches and techniques to help
increase their knowledge and skills around APIs. There is a wide range
in the level of knowledge and skill regarding API design and delivery
across Government agencies.

Hence, this document tries to offer a balance of guidance for those new
to APIs along with quick lookup standards, which should assist agencies
in achieving consistency and commonality in their API deliverables.

## Scope

This document aims to provide a set of high-level standards with design
and implementation guidance, along with low-level API best practices to
guide government agencies in their development of APIs.

-   **Part A -- API Concepts and Management 2021\
    **Looks at the business context for APIs within government and
    articulates the principles and considerations that could impact an
    agency when creating APIs. It looks at APIs in the context of their
    impact on the organisation as well as across government and public
    services through to commercial innovation. Version 1.0 published in
    2016 was called API Standard and Guidelines - Part A -- Business.

-   **Part B -- API Security 2021\
    **Part B (this document) contains the API Security reference
    architecture and technical details for implementing API Security.
    Version 1.0 published in 2016 was called API Standard and
    Guidelines - Part A -- Technical but has been split into a Part B -
    Security and Part C -- Development for this version 2.0.

-   **Part C -- Development\
    **Part C contains the technical details for API Development,
    including general API implementation standards for API developers &
    consuming application developers. Version 1.0 published in 2016 was
    called API Standard and Guidelines - Part A -- Technical but has
    been split into a Part B - Security and Part C -- Development for
    this version 2.0.

> The guidance in this document set is intended to apply to all API
> standards and protocols, however much of the guidance is oriented to
> REST APIs.
>
> Applicable technical standards are referenced throughout the document
> set and are intended to provide detailed guidance for developers of
> API standards.
>
> Examples presented in this document are purely illustrative examples,
> and do not represent recommended API design and/or data content
> requirements for the New Zealand Government.
>
> The document will use hypothetical or actual use cases with a
> government context to illustrate practical application of the concepts
> described.

## Target Audience

The target audience for this document is primarily solution designers
and API developers within, or contracted to, agencies and organisations
within the public service of New Zealand.

Additionally, compliance and assurance personnel may be interested, as
well, in terms of assessing alignment with the standards and guidelines.

# API Security

## Introduction

According to Gartner, by 2022, API abuses will be the most-frequent
attack vector for enterprise web application data breaches. As such,
securing RESTful APIs is fundamental to the success of any API Strategy
or implementation; any approach should include the following three key
areas:

a.  Domain of Consideration

b.  Domain of Control

c.  Identity[^1]-centric and Holistic View

### Domain of Consideration

Developing and securing RESTful APIs is more than just applying
standards; it is a framework and state of mind that has to be understood
and followed jointly by the business owners, IT architects and
developers. The API Security framework must be defined at the
organisation and business level and should always consider who, how and
what users and applications (both internal and external to an
organisation) will interact with the APIs. These considerations should
be defined at the beginning of any project and driven from a desired
business outcome e.g. provide real time information for the public about
the closest location and address of a GP.

![Diagram Description automatically
generated](media/image5.png){width="5.901388888888889in"
height="2.8930555555555557in"}

[]{#_Toc74234863 .anchor}Figure 11: API Security Considerations

### Domain of Control

The Domain of Control contains the components (defined further in this
document) that need to be developed, deployed and they need to work
together to provide API security to support:

-   Registered application developer access to the API

-   Authenticated and authorised consuming application access to the API
    or Events

-   Protected communication between the API, the Event Broker and the
    consuming application to ensure confidentiality and integrity

-   The ability for applications to act on behalf of a customer

### Identity Centric and Holistic View

The security of APIs should not just be seen as a bounded solution i.e.
only the components illustrated in security considerations above but
needs to be seen from a holistic perspective. It needs to incorporate
existing enterprise security frameworks where the management and
understanding of user identities is core. For example, securing an API
that is targeted for a mobile application is not just about applying an
OAuth profile, it should take into consideration how mobile devices and
applications are managed and secured and how the enterprise security
framework (e.g. authentication) can be leveraged.

![](media/image6.png){width="2.8206747594050743in"
height="2.4462674978127734in"}

[]{#_Toc74234864 .anchor}Figure 12: Identity Centric

People- (or User-) centric security frameworks are key to defining the
required access policies and controls for APIs. The management of
Identity (this includes users, device, servers and applications) should
be central to any API security framework.

## Definitions

This version of the API Guidelines expends its remit, its main focus is
still on REST but GraphQL, AsyncAPI and gRPC specifications are included
under the banner of APIs.

These additional types of API are covered in Section C (API Development)
but from a high-level perspective the definitions below apply to all
four API types.

For this standard the following definitions are used:

-   **Authentication** is the process of verifying the identity of a
    customer (or device) who presents identity credentials and
    authentication key(s);

-   **Authentication Authority --** is a system entity that provides
    authentication services to ensure only permitted customers (or
    devices) gain access

-   **Authorisation** is the process of verifying that a customer (or
    device) has the right to perform an action and what they are allowed
    to access;

-   **Availability** is the ability to minimise API downtime by
    implementing threat protection;

-   **Confidentiality** is the ability to ensure information that is
    sent between Users, Applications and Servers is only visible to
    those authorised to use it;

-   **Delegation** is when a user authorises another user (or device) to
    serve as his or her representative for a particular task;

-   **Delegated Authorisation** is a framework that defines how an owner
    of a set of resources can grant access (delegate) to a designated
    user or consuming application to perform actions on some of those
    resources on the owner's behalf, but without sharing their
    credentials;

-   **Federation** is the process that allows for the leverage and reuse
    of identity credentials to multiple Authentication Authorities for
    authentication and/or Single Sign On;

-   **Integrity** is the ability to ensure that information received has
    not been modified by a third party, also providing non-repudiation
    services;

-   **Provisioning** is the automated or manual service for aggregating
    and correlating identity data resulting in the creation of user (IT)
    accounts and the delivery of user meta data used by systems to
    define access policies and controls for services.

-   **Threat protection** is the service for protecting APIs (at the
    ingress and egress points of an organisation) from known threats
    (e.g. the OWASP top 10) by preventing misuse or loss of
    availability. Note: Threat protection should also be addressed at
    the OS hardening level and should be an integral part of the API
    software development;

-   **User Managed Access** has been developed to provide a user data
    delegation model which enables a resource owner to control the
    authorisation of data sharing and other protected-resource access
    made between online services on the owner's behalf or with the
    owner's authorisation by an autonomous requesting party;

-   **Consent Management** is the process that manages the collection of
    user data, ensuring that the required policies are applied, and the
    required consent has been obtained from the user, allowing the user
    to understand how the data is used and to be able to opt out if
    required. This is being driven by many global Privacy Laws.

-   **Zero Trust (ZT)** is the term for an evolving set of cybersecurity
    paradigms that move network defences from static, network-based
    perimeters to focus on users, assets, and resources. A zero-trust
    architecture (ZTA) uses zero-trust principles to plan enterprise
    infrastructure and workflows. Zero trust assumes there is no
    implicit trust granted to assets or user accounts based solely on
    their physical or network location

> ***Note***: A customer/user can be internal or external to a
> Government Agency.

## Risks 

[APIs are another channel into an organisation's resources and
information. Most organisations are accustomed to exposing a web
interface, with good control over what information is released via that
interface. APIs offer direct, machine to machine access to resources and
information, which makes it less obvious when information is incorrectly
exposed. It becomes increasingly important for internal business
stakeholders to decide what information and resources should be released
via this channel, and to whom.]{.mark}

[The security risks that APIs introduce will be similar to the
traditional risks experienced on any web channel (web sites and web
applications), except there is:]{.mark}

-   Increased attack surface due to more ways in, multiple services to
    potentially exploit 

-   Risk of inadvertently exposing back-end data, back-end architecture
    and back-end applications

-   Potential for greater consequences if your API is
    compromised/hijacked and serves up malicious payloads to consumers

-   Greater privacy concerns where APIs involve personally identifiable
    information

-   Risks of malware in uploaded files due to performance overhead or
    lack on inline scanning

-   Risk of malformed APIs that are developed with limited security
    validation and inappropriate security validation

-   Risk related to cloud and container-based systems where security
    best practices are not applied.

Risks posed by APIs include loss of integrity, confidentiality and
availability of data, for example:

-   Loopholes retrieving API resources may offer access to more
    information than was intended (especially if fields requested are
    built straight into a DB query)

-   Write operations offer a means of polluting data stores, feeding
    misinformation into a system

-   Write operations could be used to form a Denial of Service attack by
    overloading the server or data store

-   Use of wildcards in search fields can shut down APIs and back-end
    applications

-   Cross site scripting attacks made possible by consuming applications
    not checking user inputs

-   SQL injection into consuming applications which cause database
    damage at the API backend

-   Parameter attacks such as HTTP Parameter Pollution (HPP)

-   Man-in-the-middle attacks, modifying API requests or responses
    leading to data eavesdropping or misinformation insertion

-   Subverting authentication or authorisation mechanisms to spoof
    messages from legitimate consumers

-   Credential leakage or stealing authentication tokens to obtain
    information illicitly

-   System information leakage through API error messages revealing
    details about an API's construction or underlying system makeup

-   Broken Session IDs, Keys and authentication create exposure to
    unauthorized access through authentication factors that are not
    functioning because of poor security design or technology bugs.

-   Other broken resource identifiers, authentication and authorisation
    mechanisms, allowing attackers to exploit flaws to obtain access,
    either temporarily or permanently.

-   Exposing too much information through the use of generic resource
    APIs rather than specialising APIs for each specific circumstance

### Mitigation Approach

API risks need to be mitigated in a number of ways. There is no single
off-the-shelf security solution which can be dropped in to address all
aspects of API security. APIs need to be secure by design; security
needs to be built in from scratch and be considered within the context
of existing protection mechanisms.

The main areas that API Security covers are:

a.  Identity and Access Management (IdAM) to provide the following
    services:

    -   Authentication

    -   Authorisation and delegated authority

    -   Federation

b.  Confidentiality

c.  Integrity

d.  Availability and Threat Protection

e.  Logging, Alerting and Incident Management

This ensures that:

-   The consuming application is known and can only get access to API
    resources they are allowed to

-   Message content has not been tampered with between consumer and
    provider

-   Resources are reliably from the provider intended when the consuming
    application made the request

-   The API will be available when needed, and not brought down by
    attacks from malicious consuming applications

In order to address API security risks, a security framework is needed
which encapsulates all the aspects of security listed above.

### Zero Trust and Decoupled Environments

A Zero Trust Network Access model has been talked about for a number of
years. In the current environment it is now seen by many analysts as the
direction organisations need to take. This section highlights areas of
the model that can help mitigate risks related to APIs.

Zero Trust Architecture[^2] removed the concept of trusted internal and
untrusted external networks and focuses on the policy of "never trust
always verify".

The selection of cloud services has changed this security model to one
where all actors (employees, partners etc) require access controls no
matter where they are coming from or on.

Zero Trust is seen as an architecture that is critical for organisations
moving towards decoupled microservices and API architectures.

Microservices architectures are the backbone of many API services
offered by organisations and have embraced the concepts of identity and
how permissions are created and enforced between different services.

Every microservice requires an identity which can be confirmed, and the
required permissions and policies applied which should be based on
attributes and contextual access.

The following are some of the areas that need to be considered by an
organisation when planning their implementation of Zero Trust:

-   Apply Strong Identification and Authentication

-   Build a digital trust model that is dynamic, and trust is only valid
    for the current session

-   Constant evaluation

-   Always authenticate

-   Apply contextual authorisation (Attributes, Consent, Location, Time,
    behaviour etc)

-   Build in a Digital Risk capability that maps to a level of
    confidence and constantly re-evaluates

-   Leverage IAM capability from Identity proofing to Adaptive
    Authentication

-   Incorporate Endpoint security

-   Transaction Level verification and Continuous session validation

-   Ensure Data Security is applied with reference to Encryption and
    User privacy controls including consent management

-   Implement strong Auditing, Logging, Event reporting and Forensics
    providing insight and behavioural patterns

-   Smart Threat detection with Machine Learning

-   Inject Identity context into the API traffic (User, Application,
    Device etc)

-   Use JWT to provide secure and validated claims, which can also be
    encrypted

-   Apply Fine grained access at the egress point, allowing the
    Enforcement point to allow, block filter or modify the response

-   Identity Propagation to backend services to make decisions

-   JWTs limit chatter in microservice environments

-   All APIs should be secured and treated as if they are public APIs.

## Security Reference Architecture

> This section describes an API Security Reference Architecture and its
> component parts to inform the construction of an API security
> framework.
>
> It is important to note that REST, gRPC, GraphQL and AsyncAPI are
> different architectural models for building synchronous and
> asynchronous APIs that can leverage the Security Controls (e.g. OAuth
> 2.0 and OpenID Connect) defined in this document; but they all have
> their own intrinsic security models (e.g. throttling consideration in
> GraphQL) that are not covered in this document.

### Actors and Security Functional Capabilities

> Identity and Access Management defines the actors (users and devices)
> who interact with system components that manage and expose APIs.
> Figure 13 shows a typical model of API components (support stack) and
> actors. The actors and components are described in Table and Table 8.

![Diagram Description automatically
generated](media/image7.png){width="5.901388888888889in"
height="3.220138888888889in"}

[]{#_Toc74234865 .anchor}Figure 13: API Actors & Core Components

> The green areas highlight internal actors while the yellow areas
> highlight the external actors.
>
> The components defined remain valid no matter what API architecture
> (internal, cloud, hybrid) is implemented.

+-----------+----------------------------------------------------------+
| Actors    |                                                          |
| and       |                                                          |
| Devices   |                                                          |
+===========+==========================================================+
| External  | -   Customers - the public, other agencies and partners  |
| Users     |     who use consuming applications to access resources   |
|           |     via APIs.                                            |
|           |                                                          |
|           | -   External application developers who build software   |
|           |     to access resources via APIs                         |
+-----------+----------------------------------------------------------+
| Devices   | -   PC Browsers running web applications                 |
|           |                                                          |
|           | -   Mobile Devices running apps                          |
|           |                                                          |
|           | -   Servers running systems with server-to server        |
|           |     communications                                       |
+-----------+----------------------------------------------------------+
| Internal  | -   Internal API Developers who build APIs               |
| Users     |                                                          |
|           | -   Internal Application Developers who build software   |
|           |     which accesses resources via APIs                    |
|           |                                                          |
|           | -   Business Owners responsible for the API product(s)   |
|           |                                                          |
|           | -   Security responsible for ensuring the APIs are       |
|           |     secure                                               |
+-----------+----------------------------------------------------------+

[]{#_Toc74234992 .anchor}Table 8: Actors & Devices

> The core components of an API Security Framework (the development
> portal, manager and gateway) provide a grouping of functionality.
> These functions can be delivered with discrete applications, or
> bespoke code development, via COTS products or through leveraging
> existing devices that can be configured to provide these functions /
> services. Note: some of the functionality may overlap or be combined
> into one or more products depending on the vendor used.
>
> The following lists the functions of a mature API delivery and
> security framework for an agency that is working with the development
> community. Together, these functions provide full support for the
> application developer building and developing consuming applications
> that will use the API(s) exposed by the agency.
>
> Depending on the requirements of the agency, some of these functions
> might not be required e.g. if the agency API exposed is purely for
> public consumption and only allows consuming applications to read
> information, then only a solution for enforcing threat protection
> (i.e. Denial of Service) might be required, and this could be
> delivered using an existing service protection capability.

+-----------+----------------------------------------------------------+
| Core      |                                                          |
| C         |                                                          |
| omponents |                                                          |
+===========+==========================================================+
| API       | The API Portal often provides the following functions    |
| Portal    | for internal and external application developers:        |
|           |                                                          |
|           | -   Discovery of APIs                                    |
|           |                                                          |
|           | -   Analytics to monitor APIs                            |
|           |                                                          |
|           | -   Access to specifications and descriptions of APIs,   |
|           |     including SLAs                                       |
|           |                                                          |
|           | -   Social network capability to share and publish ideas |
|           |                                                          |
|           | Also supports the development, build and test of         |
|           | consuming applications.                                  |
+-----------+----------------------------------------------------------+
| API       | The API Manager functions cover:                         |
| Manager   |                                                          |
|           | -   Centralised API administration and governance for    |
|           |     API catalogues                                       |
|           |                                                          |
|           | -   Management of registration and on-boarding processes |
|           |     for communities of API developers                    |
|           |                                                          |
|           | -   Lifecycle Management of APIs                         |
|           |                                                          |
|           | -   Applying pre-defined security profiles               |
|           |                                                          |
|           | -   Security policy administration / definition          |
|           |                                                          |
|           | -   Policy evaluation                                    |
+-----------+----------------------------------------------------------+
| API       | The API Gateway capability can provide the following:    |
| Gateway   |                                                          |
|           | -   Act as the API proxy or the host acting as the       |
|           |     primary point of access for exposed APIs             |
|           |                                                          |
|           | -   Enforce threat protection, throttling and quota      |
|           |     management                                           |
|           |                                                          |
|           | -   Authorisation Services to control access to APIs     |
|           |                                                          |
|           | -   Authentication Services to ensure only permitted     |
|           |     users (internal/external) have access to the API     |
|           |                                                          |
|           | -   Security Policy enforcement                          |
|           |                                                          |
|           | -   Monitoring and analytics for business and security   |
|           |     analysts                                             |
+-----------+----------------------------------------------------------+
| Event     | The Event Broker (or \"broker\") is responsible for      |
| Broker    | receiving events (aka messages) from publishers          |
|           | (services) and delivering them to subscribers            |
|           | (services), that is, the consumers who have registered   |
|           | interest in events of that type.                         |
|           |                                                          |
|           | Brokers often store events until they are delivered,     |
|           | which is what makes event driven architectures very      |
|           | resilient to failures. Examples of brokers are RabbitMQ, |
|           | Apache Kafka and Solace.                                 |
|           |                                                          |
|           | With the emergence of an AsyncAPI standard, event driven |
|           | architectures are becoming more prevalent.               |
+-----------+----------------------------------------------------------+
| API       | OpenAPI (REST APIs) and AsyncAPI are API (message and    |
| Docu      | event-based APIs) documentation specifications in a      |
| mentation | machine-readable format                                  |
|           |                                                          |
|           | [[https://github.com/asyncapi/bind                       |
|           | ings]{.underline}](https://github.com/asyncapi/bindings) |
+-----------+----------------------------------------------------------+
| API       | Business owners and security specialists need to be able |
| M         | to monitor the use of APIs:                              |
| onitoring |                                                          |
| and       | -   Monitor uptake of API services                       |
| Analytics |                                                          |
|           | -   Define when to deprecate an old version              |
|           |                                                          |
|           | -   Profile usage for business                           |
|           |                                                          |
|           | -   Profile usage for security baselines                 |
|           |                                                          |
|           | -   Detect and respond to security events (SEIM)         |
|           |                                                          |
|           | This helps adapt to change in usage/demand.              |
+-----------+----------------------------------------------------------+
| C         | The credential stores are identity and key stores which  |
| redential | are used to securely store:                              |
| Stores    |                                                          |
|           | -   Internal and external user objects, and possibly     |
|           |     groups                                               |
|           |                                                          |
|           | -   API keys and secrets, certificates etc.              |
|           |                                                          |
|           | These stores are used by the API Gateway for             |
|           | authorisation and authentication services                |
+-----------+----------------------------------------------------------+

[]{#_Toc74234993 .anchor}Table 9: Core Components

> The model can also be split, with the API support stack duplicated --
> one set to support internal API usage and one set to support external
> use:

![Diagram Description automatically
generated](media/image8.png){width="5.901388888888889in"
height="3.670138888888889in"}

[]{#_Toc74234866 .anchor}Figure 14: Split API Support Stack

> Authentication, authorisation, confidentiality, integrity and
> availability can be applied across the components in the support
> stack, depending on component capabilities.
>
> The actual configuration and location of the API functional
> capabilities will vary depending on individual circumstances (e.g.
> some capabilities may be internal, some may be in the cloud, where API
> development is outsourced then 'internal' functional stack may belong
> to the outsourcer etc.). Also, some components might not be required
> or can be developed in house.

## Building Secure APIs

> Building in security starts from the ground up, so development of APIs
> needs to be done with awareness of the API security risks associated
> with the resources and information being exposed, and with appropriate
> mitigations in place for these API security risks.
>
> When developing an API is it advisable to carefully consider potential
> malicious use, especially:

-   PUTs and POSTs -- which change internal data and could be used to
    attack or misinform

-   DELETEs -- which could be used to remove the contents of an internal
    resource repository

> Standard secure coding practices are always recommended (see [[OWASP
> Security by Design
> Principles]{.underline}](https://wiki.owasp.org/index.php/Security_by_Design_Principles)),
> in line with New Zealand Information Security Manual (NZISM) guidance.
> But API development should take special note of the following:

-   Design Driven Development (refer to Part C)

-   [[OWASP Top
    Ten]{.underline}](https://owasp.org/www-project-top-ten/) -- A
    summary of the standard attacks and mitigations

-   [[REST Security Cheat
    Sheet]{.underline}](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html)
    -- REST-specific risks and how to prevent them, e.g. input
    validation

-   [[OWASP API Security
    Project]{.underline}](https://owasp.org/www-project-api-security/)
    -- Top 10 API-specific risks and how to prevent them

> The [[OWASP Cheat Sheet
> Series]{.underline}](https://cheatsheetseries.owasp.org/index.html)
> provides cheat sheets on a variety of security-related subjects. It is
> worth reviewing them to see if others may apply to your specific
> circumstances. Special note should be taken of the following where
> your API accepts input values as parameters:

-   [[OWASP Input Validation Cheat
    Sheet]{.underline}](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)
    -- A summary of input risks and mitigations

-   [[OWASP Cross Site Scripting Prevention Cheat
    Sheet]{.underline}](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
    -- how to escape inputs to prevent cross site scripting

-   [[OWASP SQL Injection Prevention Cheat
    Sheet]{.underline}](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
    -- ensuring database queries are built internally

-   [[OWASP Query Parameterization Cheat
    Sheet]{.underline}](https://cheatsheetseries.owasp.org/cheatsheets/Query_Parameterization_Cheat_Sheet.html)
    -- examples of SQL injection and stored procedure vulnerabilities

> It is also recommended that a security testing capability be
> incorporated into the development cycle which provides continuous,
> repeatable and automated tests to find security vulnerabilities in
> APIs and web applications during development and testing.

### API Security Design Principles 

> The following are key principles that should be applied when designing
> API security frameworks:

1.  Design with the objective that the API will eventually be accessible
    from the public internet, even if there are no plans to do so at the
    moment

2.  Security first -- build security into the API when they are being
    developed

3.  Use a common authentication and authorisation pattern, preferably
    based on existing security components: avoid creating a bespoke
    solution for each API

4.  Least Privilege - Access and authorisation should be assigned to API
    consumers based on the minimal amount of access they need to carry
    out the functions required, and strong authentication and
    authorization models are applied

5.  Maximise entropy (randomness) of security credentials by using API
    Keys rather than username and passwords for API authorisation, as
    API Keys provide an attack surface that is more challenging for
    potential attackers

6.  Balance performance with security with reference to key life times
    and encryption / decryption overheads

7.  Manage the exposure and lifetime of all APIs, and ensure all
    organisation APIs are covered by proactive scanning

8.  Validate the content of all incoming messages, ensuring
    communications are secured (i.e. encrypted) and apply threat
    protection policies (e.g. Injection and throttling).

# Usage Patterns

> Different API usage patterns require different authentication and
> authorisation models, below is a short definition of each of the
> different usage patterns.
>
> Note: The Security components defined in the following diagrams are
> located, for simplicity, in the "trusted" zone i.e. an area managed by
> an agency. It is possible that these components could reside in
> different zones which relate to varying levels of trust (e.g. a DMZ).

## Pattern 1: Internal Use only

> In this pattern an API is developed for internal use only by agency
> applications/systems.

![Diagram Description automatically
generated](media/image9.png){width="5.218267716535433in"
height="3.1584251968503936in"}

[]{#_Toc74234867 .anchor}Figure 15: Internal API Security

> We see there is the need to authenticate and authorise the internal
> use to the internal application and implement protection between the
> internal application and the API on the API Gateway.

## Pattern 2: Identifying an Application Developer 

> When an API is released for external use, the first interaction will
> be with App Developers who want to try the API out. This will normally
> be via the API Developer Portal.

![](media/image10.png){width="5.901388888888889in"
height="2.7555555555555555in"}

[]{#_Toc74234868 .anchor}Figure 16: Developer Authentication to API
Access

> The Application Developer needs to be authenticated to the API
> Developer Portal to register their new application and attain the
> relevant credentials which are used to secure interactions with the
> new application during development. The developer has to agree to the
> conditions of use and subsequent usage of the API can then be traced
> via the API keys (see Identify a Consuming Application below).

## Pattern 3: Anonymous Consuming Application

> This pattern applies when the API provider does not need to know which
> consuming applications are using their APIs.

![Diagram Description automatically
generated](media/image11.png){width="5.852033027121609in"
height="2.070719597550306in"}

[]{#_Toc74234869 .anchor}Figure 17: Unidentified Consuming Application

> The consuming application is unidentified (e.g. has no API Key) but
> can still use the API.

## Pattern 4: Identifying a Consuming Application

> This pattern applies when the API provider needs to know which
> consuming applications are using their APIs (for communication,
> logging and analytics purposes).

![](media/image12.png){width="5.901388888888889in"
height="2.0944444444444446in"}

[]{#_Toc74234870 .anchor}Figure 18: Consuming Application Identification

> The consuming application is authenticated (e.g. API Key, Client
> Secret etc.) to use the API, but this is only used as a means of
> identification or registration.

## Pattern 5: Authorising a System to System Interaction (B2B)

> The system to system model is where an API is being used to enable
> information sharing or integration with an external system e.g. a
> partner agency gaining access to supporting information.

![B2B](media/image13.png){width="5.895833333333333in"
height="2.28125in"}

[]{#_Toc74234871 .anchor}Figure 19: System to System Authorisation

> In this model the aim is to ensure that only the correct consuming
> system has access to the API, and that the API is protected from
> malicious use. Business to business (B2B) models often carry sensitive
> information, so the consuming system needs to be authenticated to the
> provider for authorised access, confidentiality and integrity.

## Pattern 6: Authorising a Consuming Application 

> Here the pattern covers the case where different external consuming
> applications may be granted different levels of access to resource(s).
> The application's access is not dependent on which customer is
> currently using the application, but on which application is using the
> API e.g. perhaps the developer for Application A pays a fee so
> Application A gets a different quality of service from the API than
> Application B.

![](media/image14.png){width="5.901388888888889in"
height="3.2777777777777777in"}

[]{#_Toc74234872 .anchor}Figure 20: Consuming Application Authorisation

> The consuming applications must be authenticated and authorised before
> accessing the API. This is normally enforced at the API gateway.

## Pattern 7: Authorising a Customer (Delegated Authority)

> In this pattern, external consuming applications may be granted
> different access to resource(s) depending on which customer is
> currently using the application e.g. learner authorises a mobile
> application to retrieve their own record of achievement.

![](media/image15.png){width="5.901388888888889in"
height="2.0381944444444446in"}

[]{#_Toc74234873 .anchor}Figure 21: Delegated Authority

> The customer authenticates to the device. The device and/or the
> application is already authorised to use the API. The customer logs in
> and authorises the device and/or application to access their
> information. E.g. an internet banking application.

## Pattern 8: Decoupled Flow - CIBA 

## (Client Initiated Backchannel Authentication)

> In the traditional flow the end user is redirected to an
> authentication page, in this pattern the authentication and consent
> process is delegated to an authentication device of the end user. This
> process is performed via a back channel with a request and response.
> This flow decouples the authentication device from the traditional
> flow.
>
> In this model the client can initiate the authentication, and consent,
> of an end-user via an out-of-band mechanism.

![Diagram Description automatically
generated](media/image16.png){width="5.901388888888889in"
height="2.5854166666666667in"}

[]{#_Toc74234874 .anchor}Figure 22: Decoupled Flow

## Quick Reference Table

The following table provides a quick reference to identify the most
appropriate authentication and authorisation model to use for the
patterns defined above. The models are explained in detail in subsequent
sections.

<table style="width:100%;">
<colgroup>
<col style="width: 6%" />
<col style="width: 6%" />
<col style="width: 6%" />
<col style="width: 6%" />
<col style="width: 2%" />
<col style="width: 2%" />
<col style="width: 6%" />
<col style="width: 6%" />
<col style="width: 6%" />
<col style="width: 6%" />
<col style="width: 3%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 6%" />
<col style="width: 4%" />
<col style="width: 3%" />
<col style="width: 4%" />
<col style="width: 6%" />
</colgroup>
<thead>
<tr class="header">
<th rowspan="3">OAuth 2.0 properties</th>
<th colspan="2"></th>
<th colspan="15">Vendor or Internally Developed API Gateway
Capability</th>
</tr>
<tr class="odd">
<th rowspan="2">Mutual TLS (Certificates)</th>
<th rowspan="2">API Keys</th>
<th colspan="11">OAuth 2.0 Grant Types</th>
<th colspan="3">OpenID Connect</th>
<th></th>
</tr>
<tr class="header">
<th>Client Credentials</th>
<th colspan="2">Resource Owner Password Credentials</th>
<th colspan="4">Authorisation Code</th>
<th colspan="3">Implicit</th>
<th>Client Initiated Backchannel Authentication (CIBA)</th>
<th colspan="3">Hybrid</th>
<th>API Gateway Proprietary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>OpenID Connect Scope</td>
<td>n/a</td>
<td>n/a</td>
<td>N</td>
<td>N</td>
<td>Y</td>
<td colspan="2">N</td>
<td colspan="2">Y</td>
<td>N</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
<td>n/a</td>
</tr>
<tr class="even">
<td>Response type</td>
<td>n/a</td>
<td>n/a</td>
<td>n/a</td>
<td>n/a</td>
<td>n/a</td>
<td colspan="2">Code</td>
<td colspan="2">code</td>
<td>Token</td>
<td>Id_token</td>
<td>Id_token token</td>
<td>n/a</td>
<td>Code id_token</td>
<td>Code Token</td>
<td>Code id_token token</td>
<td>n/a</td>
</tr>
<tr class="odd">
<td>PKCE</td>
<td>n/a</td>
<td>n/a</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
<td>N</td>
<td>Y</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>n/a</td>
</tr>
<tr class="even">
<td colspan="18"><strong>API Usage Patterns</strong></td>
</tr>
<tr class="odd">
<td>Pattern 1: Internal Use Only</td>
<td>✔</td>
<td></td>
<td></td>
<td>✔</td>
<td></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>✔</td>
</tr>
<tr class="even">
<td>Pattern 2: Identifying an Application Developer</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
</tr>
<tr class="odd">
<td>Pattern 3: Anonymous Consuming Application</td>
<td></td>
<td>✔</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Pattern 4: Identifying a Consuming Application</td>
<td></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>✔</td>
</tr>
<tr class="odd">
<td>Pattern 5: Authorising a System to System Interaction (B2B)</td>
<td>✔</td>
<td>✔</td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>✔</td>
</tr>
<tr class="even">
<td>Pattern 6: Authorising a Consuming Application</td>
<td></td>
<td>✔</td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>✔</td>
</tr>
<tr class="odd">
<td>Pattern 7: Authorising a Customer (Delegated Authority)</td>
<td></td>
<td>✔</td>
<td></td>
<td>✔</td>
<td></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td>🗶</td>
<td></td>
<td></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td>✔</td>
<td>✔</td>
<td>✔</td>
<td>✔</td>
</tr>
<tr class="even">
<td><p>Pattern 8:</p>
<p>Decoupled Flow (CIBA)</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><p>✔</p>
<p><strong>Recommended</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

[]{#_Toc74234994 .anchor}Table 10: Quick Reference Table

> The initial consideration for any API Security Framework should be to
> use the Authorisation Code Grant Type, the following points provide
> pointers for agencies when considering their requirements:

1.  It is good practice to use API Keys as the basis of all
    system-to-system authentication, such as consuming applications to
    API.

2.  For the Authorise Consuming Application usage pattern, the **Client
    Credentials Grant Type** is recommended but the **API Keys** model
    can be used instead.

3.  For the Customer Authorisation usage pattern

    -   the **Authorisation Code Grant Type** is recommended where the
        customer is the Resource Owner, the provider (agency) controls
        the Resource Server, but the Authorisation server is not owned
        by the provider or is elsewhere within the provider organisation

    -   Where there is a strong desire to not interrupt the customer's
        experience with the consuming application, use of **Client
        Initiated Backchannel Authentication** is appropriate.

    -   the **Resource Owner Password Credentials Grant Type** is
        appropriate where the customer is the Resource Owner, the
        provider (agency) controls the Resource Server, and the API
        Gateway is the OAuth 2.0 Authorisation Server

4.  Use of solely **API Keys** for Customer Authorisation is only
    appropriate as a last resort

5.  For the Internal Use Only usage pattern, **the Authorisation Code
    Grant Type** is recommended, where practical. Otherwise, it may be
    appropriate to leverage the provider agency's existing internal
    authentication and authorisation providers

6.  For the **Developer Authentication** usage pattern, it is
    appropriate to leverage (or build) the capabilities of the developer
    portal (e.g. username and password).

7.  The **Decoupled flow (CIBA)** supports out-of-band authentication
    and consent approval. It is recommended for organisations that want
    to enable push notification for web-based services and applications.

8.  The **Authorisation Code Grant Type** has been enhanced with
    **PKCE** (Proof of Key for Code Exchange) and addresses key security
    hacks. In OAuth 2.1 (draft) it is now recommended as a default
    option for **Authorisation Code Grant Type.**

# API Authentication & Authorisation Basics

> Before looking at the technical solutions to API authentication and
> authorisation, this section will provide an introduction that
> illustrates the situations where authentication and authorisation are
> appropriate.
>
> Authorisation and authentication are intrinsically linked inside the
> OAuth 2.0 framework which in itself is regarded as synonymous with
> securing APIs. OAuth 2.0 uses its own terminology which is worth
> becoming familiar with when adopting an OAuth 2.0 approach.
>
> As the OAuth 2.0 framework is a commonly accepted approach to the
> securing of modern APIs (large companies like Google, Microsoft and
> Twitter use it), this section also covers an introduction to OAuth
> 2.0.

## Authentication

**[Required]{.smallcaps}**

When securing APIs, authentication is required to identify the consumers
and/or consuming applications that want to access or consume an API.
Authentication enables the API provider to identify all consumers of an
API and to confirm that the consumer requesting access is who they say
they are. This doesn't automatically authorise them to access the APIs
or the underlying resources.

Providers should define a registration process for each category of
consumer, whether system or human.

The ability of knowing who is using an API cannot be overstated. This is
critical when it comes time to implement aspects of the API service
lifecycle, such as service deprecation, or notification of an outage. It
also enables the API provider to implement different service levels for
different consumers. E.g. commercial customers might have a higher
request limit per day than customers not paying for the service.

Making application developers register for use of the API also means
they must sign up to terms and conditions that define how they might use
the data they get from the API, and that they agree to ensure that their
consuming applications will behave in an acceptable and non-abusive
manner.

### Authentication Techniques

> The diagram below lists the authentication techniques that can be used
> to secure APIs and Appendix B - Authentication provides guidance on
> when to use them.

![](media/image19.png){width="5.905216535433071in"
height="3.9583333333333335in"}

[]{#_Toc74234875 .anchor}Figure 23: Authentication Options

> There is a second Security Token option that is built on SAML, but it
> is only recommended if SAML is already in place within a particular
> sector (For example Education), otherwise SAML is seen as a deprecated
> model for REST APIs.
>
> This document does not cover the SAML option but the following link
> detail how SAML is used as an authentication token in OAuth 2:
>
> [Security Assertion Mark-up Language (SAML) 2.0 Profile for OAuth 2.0
> Client Authentication and Authorization Grants]{.underline}

## OAuth 2.0 Basics[^3]

> OAuth 2.0 provides a more comprehensive and extensible approach to
> security than some of the basic authentication and authorisation
> mechanisms. Based on security tokens, it can be used for delegated
> authority such as enabling a mobile application to act on behalf of
> its user.
>
> The IT industry perceives the need for any production quality API
> security framework to be based on OAuth 2.0. In reality OAuth 2.0 is a
> delegated authorisation framework, but it provides the
> **[foundations]{.underline}** on which secure services can be built in
> order to provide the complete security solution.
>
> OAuth 2.0 requires some fundamental security components in order to
> work, and has its own terminology for describing these components and
> their roles:

![](media/image20.png){width="4.072275809273841in"
height="2.782584208223972in"}

[]{#_Toc74234876 .anchor}Figure 24: OAuth 2.0 Components

1.  **Resource Owner** -- the person who has the right to grant a third
    party (e.g. a consuming application) access to a protected resource
    (e.g. information about themselves). Quite often the resource owner
    is the customer.

2.  **Client (or Client Application)** -- A consuming application
    requesting access to a protected resource on behalf of a third party
    e.g. a mobile application on a user's (third party) smartphone or a
    web application accessed via a browser.

3.  **OAuth Server / Authorisation Server** provides a Security Token
    Server / Infrastructure for managing tokens. It is responsible for
    issuing:

    -   Authorisation (code) grant -- approval tokens driven by Resource
        Owner approval

    -   Access tokens used by the API to authorise access

    -   Refresh tokens which allow new access tokens to be requested by
        the client and re-issued within a specified timeframe

4.  **Authentication Server** -- This is not a component of OAuth 2.0,
    or defined by OAuth 2.0, but needs to be considered when defining a
    complete OAuth 2.0 framework. This could be a simple login
    capability or managed by an Identity Service Provider.

5.  **Resource Server** -- This hosts the protected resources (APIs &
    backend applications) which only allow authenticated and authorised
    clients by:

    -   Checking the access token in each incoming API request

    -   Validating the access token against the Authorisation Server and
        the permitted access rights

> OAuth 2.0 comes with four types of grant flows (how Client
> Applications can gain Access Tokens), each appropriate to different
> situations and solution requirements:

-   Client Credentials

-   Resource Owner Password Credentials

-   Authorisation Code

-   Implicit

> OAuth 2.0 is appropriate where there is a requirement for third party
> applications to access restricted resources. This should help mitigate
> the risks relating to:

-   Third party applications storing user credentials (username and
    password)

-   Resource servers having to support user stores and password
    authentication

-   Resource owners not being able to define granular access to
    resources, including duration

-   Revoking credentials that are compromised

> The following two sections (Resource Based Scopes (Scopes) and Proof
> Key for Code Exchange (PKCE)) are two additional concepts that should
> be clearly understood, and they provide additional security controls.
> Also, PKCE is seen as a security control that will be mandated in
> future versions of the OAuth 2 specification.

### Resource Based Scopes (Coarse Grained Access)

> Access and Refresh Tokens provide confirmation that the end-user has
> consented to delegate access rights to the client. Scopes, which are
> linked to the Access Token, provided an additional level of
> authorisation, each one defining a specific capability for example
> "read" document or "write" document.
>
> Scopes are approved by the end user and enforced by the backend API.
> The authorisation server validates the token, which contains the
> scopes that have been consented to, and validates the client is not
> exceeding its access rights.

### PKCE (Proof Key for Code Exchange)

> The Authorisation Code Grant Type is regarded as the recommended
> solution for most scenarios and is regarded as one of the most secure
> options especially or server-side applications, where the final access
> token required to call the Resource APIs is protected via an encrypted
> channel between the Authorisation Server and the Client Application
> (residing on a server)
>
> To obtain the access token the client application makes an
> authorisation request to the Authorisation Server and if the required
> information is provided and approved the Authorisation Server presents
> the Client application with a Code that is then used to request the
> access token over the secure back channel.
>
> The back-channel link is normally secured using MTLS, but the initial
> flow to obtain the code token is over TLS and in certain architectures
> can be intercepted in a Man in the Middle attack.
>
> Proof of Key for Code Exchange (PKCE) was developed specifically to
> address this, which is called the "Authorisation Code Interception
> Attack", and in particular for mobile phone scenarios where malicious
> application (with elevated rights) could also be installed on the same
> mobile device as the client application and obtains the code, and with
> this then obtain the access token.
>
> It works based on a random key (code verifier) that is generated, only
> known by the Client and is used to create another random key, based on
> a hashing method, which is called the code challenge.
>
> The challenge is sent (including the method) during the code flow and
> is stored by the authorization server.
>
> When the client requests the token with the code token, it also
> includes the original code verifier, which the authorisation server
> validates against the code challenge before the Access Token is
> returned to the client.

## Basic OAuth 2.0 Implementation Patterns

> There are three primary implementation patterns:

1.  Client Credential Grant Flow

2.  Authorisation Code Grant Flow

3.  Distributed Resource and Authorisation Servers

![A picture containing shape Description automatically
generated](media/image21.png){width="5.788888888888889in"
height="2.51875in"}

[]{#_Toc74234877 .anchor}Figure 25: OAuth 2.0 Implementation Models

> As can be seen above, in most models the Resource Server resides with
> the Authorisation Server. But OAuth 2.0 also supports a distributed
> model, if needed, where the Resource Server and Authorisation Server
> are separate.
>
> By adding an Authentication Server component into the API Security
> Framework, a number of additional implementation models can be
> considered. The models above have separate Authentication servers e.g.
> external Identity Service Providers, Google, RealMe etc. and internal
> Authorisation services.
>
> These Authentication Services could be housed on the same system as
> the Authorisation and Resource Server, and can, as would be expected,
> simplify the Security architecture.

![A picture containing diagram Description automatically
generated](media/image22.png){width="5.8078619860017495in"
height="2.527356736657918in"}

[]{#_Toc74234878 .anchor}Figure 26: OAuth 2.0 Models (co-location of
Authorisation & Authentication Services)

### Distributed Model - User Managed Access (UMA)

> The Distributed Models allows for multiple Resource Servers and
> Authorisation Servers and is addressed by the User Managed Access
> (UMA) model, which is driven by the Kantara initiative[^4] and
> currently has been productionised by a number of vendors[^5].
>
> UMA is a delegation access model allowing 3^rd^ Parties to have
> temporary access to resources that are approved (consented to) by the
> resource owner.
>
> The resource owner has the ability to provide predefined policies that
> define the relationship and access controls for all their resources
> across multiple Resource Servers of what can be accessed and by whom
> (i.e. minimise their interaction in the current OAuth approval
> process) and provides a central point of control
>
> A centralised UMA Authorisation Server then keeps track of all
> Resource Servers associated with a given Resource Owner.

![Diagram Description automatically
generated](media/image23.png){width="3.9213845144356956in"
height="4.4000513998250215in"}

[]{#_Toc74234879 .anchor}Figure 27: User Managed Access

> The Resource Owner establishes a token-based trust relationship
> between the Resource Server and the Authorisation Server.
>
> The Resource Owner also defines the access control policies which
> grant access to potential consumers. A client application, driven by
> the Requesting Party who is requesting access to resources owned by
> the Resource Owner, attempts to access a resource on a Resource Server
> but will be redirected to the UMA Authorisation Server.
>
> The client application has to obtain a client key, client secret and
> access token from the UMA Authorisation Server before trying to get to
> the required resource on the Resource Server. The Resource Server will
> validate the access token and the permitted level of access with the
> Authorisation Server before allowing the client application to consume
> its required resources.
>
> The UMA Authorisation Server offers two APIs to support these
> interactions:

-   Protection API -- used by Resource Servers for getting
    authorisation-request tokens and validating access tokens

-   Authorisation API -- used by the Client Application to obtain a
    token for accessing a specific resource

> OAuth 2.0 provides a consent model that is driven via a synchronous
> process, UMA provides enhance consent capability that is driven via
> asynchronous processes, that allows for:

1.  The sharing of information with parties and groups based on
    relationships

2.  Manage request from 3rd Parties

3.  Monitor Shares across sources

## OpenID Connect

### Basic Principles

> OpenID Connect is the recommended security profile for the use of
> OAuth 2.0 authentication security tokens when an API requires more
> secure authentication than offered solely by API keys e.g. when data
> is a two-way flow between the consuming application and the API.
>
> OpenID Connect is used to:

1.  Enhance the process and user experience during the onboarding
    process

2.  Provide an SSO capability

3.  Secure transfer of user data

4.  Enrich the user experience

5.  Provides a trust framework \[integrity\] for Service and Identity
    Providers to share consented user data

> During the authorisation token exchange process a level of
> authentication is required. The authentication process is limited to
> what authentication services the authorisation server can support. For
> example, the Resource Owner authorisation process is normally
> supported out of the box by the authorisation server, using username
> and password.
>
> These authentication services can be enhanced with authentication
> security tokens by implementing the OpenID Connect OAuth profile. For
> customers and internal users this can be achieved using a brokered or
> federated service.
>
> Federation in the context of API security provides the ability to
> re-use user identities in an SSO way by providing a trust relationship
> between the Identity Service Provider (Open ID Connect service) and
> the Authorisation Server. This establishment of trust between the
> Identity Provider and Authorisation Server is normally established
> using certificates and mutual authentication. All communication must
> be over TLS/MTLS to provide Confidentiality and Integrity controls.
>
> OpenID Connect runs on top of OAuth 2.0 and is a lightweight RESTful
> framework for identity service interaction, to provide authorisation
> services. It allows claims (or attributes) about a user to be shared
> in a secure manner from an identity provider to the client application
> with the explicit consent of the user.
>
> OpenID Connect uses all the flows, grant types and endpoint exposed by
> OAuth 2.0, and it add the following additional capabilities to provide
> access to the users claims / attributes:

1.  An ID Token

2.  A Userinfo endpoint

> The ID Token is a JSON Web Token (JWT) that contains authenticated
> user information (and attributes) that the authorisation (OAuth 2.0
> Server) / authentication server (OpenID Connect Server) provides to
> the client application.
>
> This token can then be used to enforce finer grained access controls
> by providing additional attributes that can be used by the
> authorisation server to apply these policies.
>
> The "new" JWT token has to be signed in order to address
> confidentiality and integrity requirements. There are also additional
> parameters (relates to code, session and access token hashes) defined
> that have been added to help address replay attacks.
>
> The Userinfo endpoint can be called with the required access token to
> also obtain the same claims/ attribute (e.g. first name) provided in
> the ID Token
>
> To address the risk of forged or stolen assertions, it is recommended
> that all communication is over TLS and tokens are at a minimum signed
> for authentication

### OpenID Connect Grant Flows

> OpenID Connect builds on the existing OAuth 2.0 grant flows, and once
> implemented it is enacted using a specific scope (openid) in the
> initial authorisation call that the client makes to the OpenID Connect
> service.
>
> There are a number of additional scopes that OpenID Connect introduces
> (e.g. profile) that detail specific attributes (e.g. name) that can be
> presented in the ID token. So, for example a Client might request the
> profile information, but it is the Identity Provider that details what
> this will provide (e.g. first and last name, phone and email address)
> and this has to be consented (via the OAuth 2 consent process) to by
> the user.
>
> The request call also includes a response type which allows the
> application developer to request identity information tokens and
> security tokens depending on what information they want back, the type
> of client (e.g. Server/ Client based). The link below provides an
> excellent summary of the response type possible with OpenID Connect.
>
> <https://darutk.medium.com/diagrams-of-all-the-openid-connect-flows-6968e3990660>
>
> The ID Token not only includes identity information it also includes
> additional technical claims which allows the Client application to
> verify that the ID Token is valid and came from the Identity Provider.
> It is highly recommended that a Client validates the ID token (e.g.
> signature, client ID and issuer). The ID token can also be encrypted
> to enhance the confidentiality and integrity of the information
> presented.
>
> OpenID Connect works with all the existing OAuth 2.0 grant types and
> adds additional security controls to the Authorisation Code grant
> flow, for the implicit flow in OAuth 2.0, which is seen as a less
> secure flow than the Authorisation flow and is now being discouraged,
> OpenID Connect provides a level of enhancement to the Implicit flow as
> the nonce and state are returned in a signed JWT, but this is really
> only recommended in login-only use cases.
>
> Finally there is the concept of a Hybrid flow
> (<https://openid.net/specs/openid-connect-core-1_0.html#HybridFlowSteps>)
> that uses the Authentication code flow as a base and (depending on
> what is required by the client and what is enabled by the
> Authorisation Server) it allows additional tokens (ID Tokens) to be
> issued during the flow. These are both used to provide secure identity
> information and also additional confidentiality and integrity controls
> relating to state, nonce values and hashes.
>
> A good example of where the Hybrid flow is being mandated is in the
> management of consent in the Open Banking Consumer Data Rights
> specifications. (https://cdr-register.github.io)

### OpenID Connect Patterns

> In the first OpenID Connect pattern detailed in Figure 28, the
> Authentication and Authorisation Servers are conceptually hosted on
> different physical servers (the OpenID Connect server can be internal
> or external to the organisation). The user connects to the web
> application and is redirected to the OpenID Connect server for
> authorisation.
>
> Once authorised, the user is redirected to the Web Application which
> in turn exchanges the ID Token for an access token.
>
> Note: It is the token flow and exchange that is key to understand in
> this model. The Web Application could be an Application/ API Server
> and the interface to the authorisation and authentication server
> managed by the API Gateway
>
> A trusted link is set up between the OpenID Connect Server and the
> OAuth Server (Authorisation Server) which also allows additional
> identity information to be provided in a JWT format via the userInfo
> endpoint. This is important as the token exchange can result in the
> loss of user data that is required to provide fine grained access.
>
> If the OpenID Connect server was external, it would be the API Gateway
> that would be responsible for the interface and token exchange
> process.

![](media/image24.png){width="5.901388888888889in"
height="3.4069444444444446in"}

[]{#_Toc74234880 .anchor}Figure 28: OpenID Connect - Distributed
Authorisation & Authentication Server

> The application has to exchange the ID Token for an Access Token in
> this pattern.
>
> In the second pattern (below) the OpenID Connect server is run on the
> same server as the OAuth Authorisation server, so the ID Token and the
> Access Token can be issued at the same time. In both models the OpenID
> Connect Server can use LDAP for its back-end User Store, to provide
> authorisation for internal users.

![](media/image25.png){width="5.901388888888889in"
height="3.0097222222222224in"}

[]{#_Toc74234881 .anchor}Figure 29: OpenID Connect & OAuth

> One other model is for an external OpenID Connect pattern, where the
> OpenID Connect server is an external Identity Provider (e.g. AoG
> service) and the API Gateway is responsible for managing the token
> exchange, potentially also housing the Authorisation Server.

### Heart Working Group

> The OpenID Foundation uses working groups
> ([[https://openid.net/wg/]{.underline}](https://openid.net/wg/) ) to
> focus on specific problems, technology or specific marketplace sectors
> like FAPI (Financial-Grade APIs) or the Health sector HEART Working
> group.
>
> HEART (Health Relationship Trust
> [[https://openid.net/wg/heart/]{.underline}](https://openid.net/wg/heart/)
> )defines a set of profiles that enables patients to control how, when,
> and with whom their clinical data is shared.
>
> It also defines the interoperable process for systems to exchange
> patient-authorized healthcare data consistent with open standards,
> specifically FHIR (Fast Healthcare Interoperability Resources), OAuth,
> OpenID Connect, and UMA (User-Managed Access).
>
> Two pertinent specifications are:
>
> **Health Relationship Trust Profile for User-Managed Access 2.0**
>
> [[https://openid.net/specs/openid-heart-uma2-1_0.html]{.underline}](https://openid.net/specs/openid-heart-uma2-1_0.html)
>
> **Health Relationship Trust Profile for Fast Healthcare
> Interoperability Resources (FHIR) UMA 2 Resources**
>
> [[https://openid.net/specs/openid-heart-fhir-uma2-1_0.html]{.underline}](https://openid.net/specs/openid-heart-fhir-uma2-1_0.html)

### CIBA Flow

> The OpenID Connect "Client Initiated Backchannel Authentication" flow
> is important because it adds three "decoupled" authorisation flows.
> Instead of using redirects through the browser, this model allows a
> user's mobile device to be decoupled from the flow, and the client
> application, and act as an authentication device on which the user
> authentication and the consent confirmations are performed.
>
> The important point here is the client application and authorisation
> application/service do not have to run on the same device (e.g.
> smartphone) or be linked.
>
> In the CIBA flow the initial authorisation call is made to the new
> (OAuth2) backchannel authentication endpoint,
>
> and the authorisation server then delegates the authentication and
> consent approval tasks to the authentication device (smartphone) of
> the user, who will accept or deny the request.
>
> The access token being sent to the client is managed by one of three
> flows:

1.  Poll -- The client polls the Authorisation Server until the
    authorisation server has received the approval from the
    authentication device.

2.  Ping -- The client waits until it is notified by the Authorisation
    Server and then it requests the token

3.  Push -- The Authorisation server, when it receives approval from the
    authentication device pushed the Access, ID Token and Refresh token
    to the client

## Authorisation

**[Required]{.smallcaps}**

> Authorisation is the act of performing access control on a resource.
> Authorisation doesn't just cover the enforcement of access controls,
> but also the definition of those controls. This includes the access
> rules and policies, which should define the required level of access
> agreeable to both provider and consuming application. The foundation
> of access control is a provider granting or denying a consuming
> application and/or consumer access to a resource to a certain level of
> granularity.
>
> In the Authentication section the concepts of OAuth were introduced,
> and a number of Authentication patterns were defined. This section
> focuses on Authorisation and provides additional patterns that work
> with OAuth or provides an alternative.

### Authorisation Techniques

> Authentication on its own does not necessarily provide permissions to
> access an API or application. It merely validates that you are who you
> say you are. If it is used for access control, it is an all or nothing
> control mechanism (e.g. administration account).
>
> Once a user is authenticated (e.g. using username and password), an
> authorisation process will grant (or deny) them the right to perform
> an action or access to information. Normally this authorisation
> process is applied using either a coarse grained or fine-grained
> access control process.
>
> The normal model is to provide coarse grained access at the API or API
> Gateway request point, and fine-grained control at the backend
> services, but this model is changing as backend systems become more
> modular (e.g. microservices) and less monolithic. This will result in
> a need for fine grained authorisation support at the request point.
>
> With this understanding, the two types of authorisation that will be
> considered are defined in Figure 32.
>
> This covers:

1.  Role- or Group-based authorisation - where membership in a role or
    group determines access rights for the consumer

2.  Policy- or Attribute-based authorisation - where characteristics of
    the consumer are evaluated to determine access rights for the
    consumer

![Diagram Description automatically
generated](media/image26.png){width="5.901388888888889in"
height="1.6458333333333333in"}

[]{#_Toc74234882 .anchor}Figure 30: Authorisation Techniques

> The API Gateway will provide this support either using OAuth 2.0 or
> its own proprietary capability.

### Roles Based Access Controls (RBAC)

> In many organisations Active Directory provides the authentication
> services for users. Active Directory groups are then used to provide
> authorisation. This is classed as Discretionary Access Control (DAC):
> access to systems is granted by applying Access Control Lists (ACLs)
> directly to the user, or to the groups in which users reside.
>
> Note: LDAP directories can also provide this service, and in many
> organisations are used to provide the same service AD delivers but for
> external users.
>
> Active Directory (or LDAP) Groups are synonymous with roles and can be
> used to provide coarse-grained authorisation for APIs.

#### Scopes (Limited Fine Grain Access) 

> Based on the services (APIs) that are exposed, additional access
> controls can be applied using scopes. For example, a data service
> might provide "read" and "write" scopes which could be granted to a
> user based on the AD groups they were in.
>
> When the "Authorisation code" token is passed to the Authorisation
> Server a scope parameter is included to define what scopes the client
> can use. Scopes can be used to limit the authorisation granted to the
> client by the resource owner. These scopes are defined by the client
> application developer. This is an important consideration as it can
> impact how the API service is defined e.g. single service with
> multiple scopes or multiple services with single scopes. The developer
> has to ensure that the minimum privileges are granted to client
> applications to carry out the tasks (exposed by the Client Application
> and APIs) the user wishes the application to complete.
>
> Scopes provide a level of coarse/fine grained access and represent
> specific access rights e.g. the ability to read a document or write a
> new document (or both) is limited by the Access Token.
>
> Scopes can be used alone to define coarse/fine grained access, but
> these scopes need to be defined and built into the Client application
> / API being built. Consideration is needed to understand (for example)
> if:

-   a single scope protects the service

-   scopes are defined to protect fine-grained business functionality

-   services should be divided into many smaller services with one scope
    each

> Once the token is issued to a client application, the access rights
> bound by the scope are encapsulated in the Access Token for the length
> of its validation period.
>
> A client application may invite a user to authorise the application to
> act on behalf of the user. Using NZBN as an example, the client
> application (an accounting application for example) may invite a user
> to authorise the client application to update primary business data on
> the user's behalf. The application may ask "Do you want \[client
> application\] to be able to update your business information on the
> NZBN Directory?". Assuming the user grants the client application this
> privilege, the authorisation token returned by the API will have a
> scope that enables update access. This scope is represented by an
> identifier. For example, the NZBN update scope looks like this:
>
> https://api.nzbn.govt.nz/auth/pbd.readwrite
>
> whereas a read-only scope would be:
>
> https://api.nzbn.govt.nz/auth/pbd.core.readonly

### Attribute Based Access Controls

> Attribute-based access control (ABAC) defines an access control
> process whereby access is granted based on policies that are built
> using attributes e.g. a policy might state that access to a specified
> resource is only permitted for users who are in Sales or Marketing,
> who are managers, during office hours only. ABAC provides fine grain
> authorisation services.
>
> The really important control that ABAC provides is the ability to
> provide context when applying access controls, e.g. access decisions
> can be based on the IP address of the device, the operating system of
> the client and the last known transactions of a client.
>
> The recognised standard for ABAC is XACML, which is an XML
> based-language.

### API Gateway

> API Gateways have been mentioned previously in the context of API
> protection. Most API Gateways on the market provide support for OAuth
> 2.0 and can also provide Authorisation (and Authentication) Services
> via a direct connection to:

1.  An Identity Store containing groups

2.  An Identity Access Management system

3.  A Policy server

![](media/image27.png){width="5.450234033245844in"
height="2.6030697725284337in"}

[]{#_Toc74234883 .anchor}Figure 31: API Gateway for Authorisation

# Security Controls 

> This section looks at additional controls that should be considered
> and implemented when protecting APIs. The four areas that should be
> considered are:

1.  Confidentiality

2.  Integrity

3.  Availability

4.  Threat Protection

5.  Logging and Auditing

> Depending on the classification of the information that is presented
> in the APIs and the Risk Framework applied different access controls
> will need to be applied.
>
> Appendix F provides move detail in reference to the security controls
> that can be applied.

## Confidentiality and Integrity

> Confidentiality and integrity cover the handling of request and
> response data, both in transit and at rest. The aim is to protect the
> payload content from unauthorised access, manipulation or faking. An
> API request needs to be received intact by the API, with validation as
> to the source of the request. Untampered API responses need to be
> received by the consuming application, with confirmation that they are
> legitimately from the API.

## Availability and Threat Protection

> Availability in this context covers threat protection to minimise API
> downtime, looks at how threats against exposed APIs can be mitigated
> using basic design principles and how to apply protection against
> specific risks and threats.
>
> Availability also covers scaling to meet demand and ensuring the
> hosting environments are stable etc. These levels of availability are
> addressed across the hardware and software stacks that support the
> delivery of APIs. There are no specific standards for availability,
> but availability is normally addressed under business continuity and
> disaster recovery standards. These standards recommend a risk
> assessment approach to define the availability requirements. Further
> information on business continuity and risks can be found at Standards
> New Zealand website[^6].
>
> For cloud services, the New Zealand Government ICT website provides an
> assessment tool that includes a risk assessment tool which covers
> availability, business continuity and disaster recovery related
> questions[^7].
>
> As mentioned in section 1.1.3, there are various types of risk which
> impact APIs. This includes threats to availability as well as
> confidentiality and integrity. Many threats can be mitigated through
> good secure coding practices, using OWASP guidelines, as indicated in
> section 1.2.2.
>
> Where the resources being exposed by an API are sensitive i.e. not
> public data, it is advisable to perform:

-   Threat assessment -- early on in the API development lifecycle

-   Penetration test -- once an API is developed and published
    (testable)

> There are also automated vulnerability testing tools which can be used
> to give an indication of vulnerabilities in web application designs.

## Logging and Alerting

> Traditional logging, alerting and incident management practices also
> apply to APIs, along with additional considerations such as:

-   correlating API requests with specific back-end system activity and
    the resulting API responses to support end-to-end tracing

-   identifying specific API requests from consumers to help resolve API
    consumer problems

-   detecting events that may indicate a malicious attempt to access an
    API

# API Security Use Case

> The illustrative example below demonstrates a sequence of information
> exchange events and highlight where security controls are implemented.

## High Level View

> This sequence diagram shows the high-level interaction of the actors
> and participant service providers.

![Diagram Description automatically
generated](media/image28.png){width="5.901388888888889in"
height="4.313194444444444in"}

[]{#_Toc74234884 .anchor}Figure 32: API Security Use Case High Level
View

## Detailed Level View

> This sequence diagram shows the detailed interaction of the actors and
> participant service providers.

![Graphical user interface Description automatically generated with low
confidence](media/image29.png){width="6.379630358705162in"
height="5.029082458442694in"}

[]{#_Toc74234885 .anchor}Figure 33: API Security Use Case Detailed Level
View

1.  Glossary of terms

> Below is a list of common terms. Terms in the Description column
> highlighted in bold are described elsewhere in the Glossary.

  -----------------------------------------------------------------------
  Term                 Description
  -------------------- --------------------------------------------------
  Analytics            Analytics in the context of this document is the
                       capturing and reporting of API usage.

  Consumers            Customers, API Consuming Applications and
                       Application Developers who use the API.

  Consuming            This is any application (on any device) that
  Application          consumes an API.

  Context              Context in this document generally refers to
                       request context. For example, a JWT Token may
                       contain information about the customer initiating
                       an API request.

  Customers            People (or organisations) that use the Consuming
                       Applications to access the API resources the API
                       Provider is offering.

  Discovery            The ability for Application Developers to find
                       resources and associated APIs to use in their
                       Consuming Applications

  API                  Application Programming Interface - a piece of
                       software, which provides a way for other disparate
                       pieces of software (applications, systems) to talk
                       to one another.

  API Catalogue        The API delivery component that lists the APIs
                       offered, along with their Interface Specifications
                       and guidance on how to gain access and use the
                       APIs.

  API Developer        The organisation (or person) who creates the API
                       and maintains the Interface Specification for the
                       API.

  API Developer Portal The API delivery component that allows API
                       Providers to engage with, onboard, educate and
                       manage Application Developers whether inside or
                       outside the organisation. These management
                       activities will generally include registration,
                       documentation, analytics etc.

  API Gateway          The API delivery component that allows API
                       Providers to offer APIs to the outside world. This
                       component (physical or virtual) hosts the APIs
                       ready for Consumers to access. It provides an API
                       Provider with the ability to control who has
                       access to their APIs by enforcing policies for
                       access control. Some API gateways also offer
                       additional capabilities.

  API Manager          The API delivery component that allows API
                       Providers to control an API's visibility and
                       behaviour. It is usually exposed as a UI/console
                       to internal staff only, as it is seen as an
                       administration component. It offers a variety of
                       capabilities, including API registration and
                       catalogue administration.

  API Provider         Organisation who provides the API to expose a
                       resource (information or functionality) for
                       Consumers.

  Application          The software behind the API which provides the
                       business logic for the resource.

  Application          Software developer or organisation who builds
  Developer            Consuming Applications that use the API. An
                       application developer can be internal to your
                       agency, developers that work with trusted
                       partners, developers from other agencies or
                       developers from the private sector.

  Interface            Provides technical information to the API
  Specification        Developer community about the API. It includes
                       information about how the API works, any access
                       control features and any error conditions.

  Product Manager      The product manager is usually a technical role.
                       They understand an agency\'s API landscape and are
                       owners of API management platforms.

  Product Owners       The product ownership function usually resides in
                       a business area rather than technology. The role
                       of the product owner is to understand the product
                       that the agency is trying to deliver and be able
                       to make decisions on the representation of the
                       product in an API.

  Publish              The act of releasing the interface specification
                       and associated API to a location accessible by
                       Application Developers

  Resource             The information or functionality exposed by the
                       API.

  State                State defines the point in time record of an
                       in-flight transaction. Some systems maintain *user
                       state* for a period of time to enable a
                       transaction to be continued from the point of last
                       recorded state. APIs are usually, but not always,
                       considered stateless.
  -----------------------------------------------------------------------

[]{#_Toc74234995 .anchor}Table 6: Glossary of Terms

# Glossary of acronyms

  -----------------------------------------------------------------------
  Term                               Definition
  ---------------------------------- ------------------------------------
  AD                                 Active Directory

  API                                Application Programming Interface

  ASCII                              American Standard Code for
                                     Information Interchange

  CA                                 Certificate Authority

  CDN                                Content Delivery Network

  DHE                                Diffie-Hellman Ephemeral

  DMZ                                Demilitarized Zone

  DoS                                Denial of Service

  ECDHE                              Elliptic Curve DHE

  HATEOAS                            Hypermedia As The Engine Of
                                     Application State

  HPP                                HTTP Parameter Pollution

  HTTP                               HyperText Transfer Protocol

  IETF                               Internet Engineering Task Force

  JSON                               JavaScript Object Notation

  JWA                                JSON Web Algorithms

  JWE                                JSON Web Encryption

  JWK                                JSON Web Key

  JWS                                JSON Web Signature

  JWT                                JSON Web Token

  LDAP                               Lightweight Directory Access
                                     Protocol

  MAC                                Message Authentication Code

  OWASP                              Open Web Application Security
                                     Project

  PBD                                Primary Business Data

  RAML                               Rest API Modelling Language

  REST                               Representative State Transfer

  RFC                                Request for Comments (IETF)

  RO                                 Resource Owner

  RS                                 Resource Server

  SAML                               Security Assertion Markup Language

  SCIM                               System for Cross-domain Identity
                                     Management

  SEO                                Search Engine Optimization

  SLA                                Service Level Agreement

  SOAP                               Simple Object Access Protocol

  SPML                               Service Provisioning Markup Language

  SQL                                Structured Query Language

  SSO                                Single Sign On

  STS                                Security Token Service

  TBC                                To Be Completed

  TBD                                To Be Done

  TLS                                Transport Layer Security (superseded
                                     SSL)

  URL                                Uniform Resource Locator

  URI                                Uniform Resource Identifier

  WSDL                               Web Service Definition Language

  XSD                                XML Schema Definition

  WADL                               Web API Description Language

  XACML                              eXtensible Access Control Markup
                                     Language

  XML                                eXtensible Markup Language

  YAML                               YAML Ain\'t Markup Language
  -----------------------------------------------------------------------

[]{#_Toc74234996 .anchor}Table 7: Glossary of acronyms

#  Further Reading

+-----------------------------------+-----------------------------------+
| OWASP REST Security               | [[https://www.owasp.org/index.php |
|                                   | /REST_Security_Cheat_Sheet]{.unde |
|                                   | rline}](https://www.owasp.org/ind |
|                                   | ex.php/REST_Security_Cheat_Sheet) |
+-----------------------------------+-----------------------------------+
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
| Using HTTP Methods for RESTful    | <https://www.restapitutor         |
| Services                          | ial.com/lessons/httpmethods.html> |
+-----------------------------------+-----------------------------------+
| Reserved JavaScript Keywords      | <https://www.                     |
|                                   | w3schools.com/js/js_reserved.asp> |
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

[]{#_Toc74234997 .anchor}Table 11: Further reading

# Appendix A - Standards for Securing RESTful APIs 

## Standards for Securing RESTful APIs

> The table below captures (current) security standards that should be
> part of any API Security Strategy, ordered by type. The provisioning
> standards are included to complete the Identity and Access Standards
> table. This enables it to be used by architects to select the most
> appropriate option.

+-----------------+----------------------------------------------------+
| Provisioning    | Provides the framework for managing the            |
|                 | provisioning of user and their access to APIs e.g. |
|                 | the process for internal or external developers    |
|                 | gaining access to API development and publishing   |
|                 | services                                           |
+-----------------+----------------------------------------------------+
| SPML            | Service Provisioning Markup Language is an XML     |
|                 | based framework for facilitating the exchange of   |
|                 | provisioning information (creates, updates and     |
|                 | deletes) on user objects (e.g. an LDAP Directory). |
|                 | This is normally implemented to provide Just in    |
|                 | Time (Real Time) provisioning.                     |
|                 |                                                    |
|                 | Although now regarded by most as a legacy          |
|                 | standard, it is still supported by most vendors    |
|                 | and used by niche service vendors.                 |
+-----------------+----------------------------------------------------+
| SCIM            | System for Cross-domain Identity Management. This  |
|                 | is a RESTful API-based framework for Just in Time  |
|                 | provisioning and, like SPML, moves away from       |
|                 | batch- and delta-based provisioning processes. It  |
|                 | uses a RESTful API to manage the provisioning of   |
|                 | users.                                             |
|                 |                                                    |
|                 | As SCIM is a REST API framework it should be       |
|                 | secured using OAuth.                               |
+-----------------+----------------------------------------------------+
| Federation /    | Provides authentication and Single Sign On         |
| Authentication  | services to customers and secure transportation of |
|                 | authentication and authorisation information.      |
+-----------------+----------------------------------------------------+
| SAML            | Security Assertion Markup Language (SAML) is an    |
|                 | XML-based, open-standard data format for           |
|                 | exchanging authentication and authorisation data   |
|                 | between parties; in particular, between an         |
|                 | identity provider and a service provider.          |
|                 |                                                    |
|                 | SAML is seen as complex but is regarded as a       |
|                 | high-level security framework.                     |
|                 |                                                    |
|                 | As it is based on XML, SAML can have high payload  |
|                 | overheads and thus can result in performance       |
|                 | issues in the mobile application space.            |
|                 |                                                    |
|                 | It is still widely used but its uptake is          |
|                 | declining. It is included in this standard to      |
|                 | support existing New Zealand SAML instances (e.g.  |
|                 | education, RealMe).                                |
+-----------------+----------------------------------------------------+
| OpenID Connect  | OpenID Connect is an interoperability              |
|                 | authentication protocol based on the OAuth 2.0     |
|                 | framework.                                         |
|                 |                                                    |
|                 | This is a relatively recent federation protocol    |
|                 | that provides lightweight federation services. It, |
|                 | like SAML, provides SSO services and allows the    |
|                 | secure exchange of user authentication data, but   |
|                 | it is not as feature rich as SAML.                 |
|                 |                                                    |
|                 | As it is based on REST/JSON, it is perceived as    |
|                 | the Federation service of choice for mobile        |
|                 | services.                                          |
+-----------------+----------------------------------------------------+
| Claims          | Claims are the contents of tokens and are pieces   |
|                 | of information asserted about a subject. For       |
|                 | example, an ID Token can contain a claim called    |
|                 | mobile which asserts the subjects mobile phone     |
|                 | number.                                            |
+-----------------+----------------------------------------------------+
| CIBA            | Client Initiated Backchannel Authentication and it |
|                 | is a decoupled grant flow that allows the end user |
|                 | to use their mobile device to authenticate and     |
|                 | approve transactions.                              |
+-----------------+----------------------------------------------------+
| Delegated       | Provides a framework for delegating the specified  |
| Authorisation   | access rights to a 3^rd^ party.                    |
+-----------------+----------------------------------------------------+
| OAuth 1.0a      | OAuth 1.0a is derived from the original OAuth 1.0  |
|                 | specification (RFC 5849) which provides a method   |
|                 | for client applications to access resources on     |
|                 | behalf of a resource owner. It is an               |
|                 | authentication framework around the exchange of    |
|                 | signed tokens. It has now been made obsolete by    |
|                 | OAuth 2.0.                                         |
+-----------------+----------------------------------------------------+
| OAuth 2.0       | OAuth 2.0 is an open standard for a delegated      |
|                 | authorisation framework. It is not backward        |
|                 | compatible with OAuth 1.0, but is modelled on the  |
|                 | framework with the objective of providing greater  |
|                 | flexibility and defines specific credential        |
|                 | (grant) flows.                                     |
|                 |                                                    |
|                 | It is also based on token exchange, with the       |
|                 | primary difference being that the tokens are       |
|                 | secured by mandating TLS on all communication      |
|                 | connections (RFC 6749), where the OAuth 1 tokens   |
|                 | are digitally signed.                              |
+-----------------+----------------------------------------------------+
| OAuth 2.1       | [[https://tools.ietf.or                            |
|                 | g/html/draft-ietf-oauth-v2-1-00]{.underline}](http |
|                 | s://tools.ietf.org/html/draft-ietf-oauth-v2-1-00). |
|                 | This is an update to OAuth 2.0                     |
+-----------------+----------------------------------------------------+
| PKCE            | Proof of Key Code Exchange provides enhanced       |
|                 | security for the Authorisation code flow.          |
+-----------------+----------------------------------------------------+
| Authorisation   | Provides a framework for controlling access to     |
| Standards       | resources.                                         |
+-----------------+----------------------------------------------------+
| XACML           | The eXtensible Access Control Markup Language      |
|                 | standard is XML based and defines a fine-grained   |
|                 | attribute-based access control policy language.    |
|                 |                                                    |
|                 | It provides an architectural model and policy      |
|                 | terminology that can be used to separate out the   |
|                 | functions of any authorisation framework.          |
|                 |                                                    |
|                 | As it is based on XML it is sometimes perceived as |
|                 | a legacy standard, but, from a RESTful API         |
|                 | perspective, it provides a fine-grained            |
|                 | attribute-based authorisation framework. (RFC      |
|                 | 7061)                                              |
+-----------------+----------------------------------------------------+
| UMA             | User-Managed Access is an OAuth-based access       |
|                 | management protocol standard.                      |
|                 |                                                    |
|                 | It builds on OAuth 2.0 to provide additional       |
|                 | delegated authorisation capabilities.              |
|                 |                                                    |
|                 | Its key focus, for RESTful APIs, is to enable an   |
|                 | individual (Resource Owner) to manage and define a |
|                 | set of access control policies that can be managed |
|                 | by an Authorisation Server, which controls access  |
|                 | to a set of APIs.                                  |
+-----------------+----------------------------------------------------+
| ALFA            | Abbreviated Language for Authorisation defines     |
|                 | fine-grained authorisation rules in a JSON-like    |
|                 | policy language.                                   |
|                 |                                                    |
|                 | This language helps remove one of the greatest     |
|                 | barriers for implementing XACML, which is          |
|                 | complexity in writing of the access control        |
|                 | policies.                                          |
+-----------------+----------------------------------------------------+
| Two             | This is a method of confirming a user's claimed    |
| (Multi)-factor  | identity (authentication) by using two or more     |
| Authentication  | pieces of evidence, relating to something they     |
|                 | know, something they have and something they are.  |
+-----------------+----------------------------------------------------+
| U2F / FIDO      | Universal 2^nd^ Factor is an open authentication   |
|                 | standard that can be incorporated into an API      |
|                 | security framework                                 |
+-----------------+----------------------------------------------------+
| TOTP / HOTP     | Time-based and HMAC-based One-Time Password. These |
|                 | can be used in any of the authentication processes |
|                 | that are part of the process of gaining access to  |
|                 | APIs. The requirements for these would be based on |
|                 | business requirements and risk analysis of the     |
|                 | information or service being exposed by the API.   |
|                 |                                                    |
|                 | These could be used to add a second authentication |
|                 | factor to any existing or proposed authorisation   |
|                 | mechanisms.                                        |
+-----------------+----------------------------------------------------+
| JSON Security   | This is a set of standards that provide security   |
| Standards       | around the exchange of tokens, based on JSON.      |
+-----------------+----------------------------------------------------+
| JWT             | A JSON Web Token is designed to be compact and     |
|                 | provides trusted information that is used in the   |
|                 | authentication process.                            |
|                 |                                                    |
|                 | Used in API security to pass identity information, |
|                 | specifically by OpenID Connect.                    |
+-----------------+----------------------------------------------------+
| JWE             | JSON Web Encryption standard provides integrity    |
|                 | validation and can be used with or without digital |
|                 | signatures.                                        |
+-----------------+----------------------------------------------------+
| JWS             | JSON Web Signature is a standard for signing JSON, |
|                 | thus providing a level of authority (where it has  |
|                 | come from) and integrity, by proving the JWT       |
|                 | hasn't been changed in transit.                    |
+-----------------+----------------------------------------------------+
| JWA             | JSON Web Algorithm defines the algorithms used for |
|                 | encrypting the JWT.                                |
+-----------------+----------------------------------------------------+
| JWK             | JSON Web Keys represent the cryptographic key used |
|                 | for encrypting JWT. The algorithms for these are   |
|                 | defined in JWA.                                    |
+-----------------+----------------------------------------------------+
| Industry        |                                                    |
| Standards       |                                                    |
+-----------------+----------------------------------------------------+
| FAPI            | Financial Grade APIs is an OpenID workgroup that   |
|                 | now defines a set of specifications that that are  |
|                 | enforces in specific legislation e.g. Open Banking |
|                 | (NZ) and Customer Data Rights (Australia)          |
+-----------------+----------------------------------------------------+
| FHIR            | Fast Healthcare Interoperability Resources is a    |
|                 | standard describing data formats and elements and  |
|                 | an application programming interface for           |
|                 | exchanging electronic health records.              |
+-----------------+----------------------------------------------------+
| PNZ             | Payments New Zealand is a government body that is  |
|                 | driving the Open Banking initiative in New Zealand |
+-----------------+----------------------------------------------------+
| NZ Trust        | This is the framework that is driving NZ future    |
| Framework       | Digital Identity direction.                        |
|                 | https://www.digital.govt.nz/dig                    |
|                 | ital-government/programmes-and-projects/digital-id |
|                 | entity-programme/digital-identity-trust-framework/ |
+-----------------+----------------------------------------------------+

[]{#_Toc74234998 .anchor}Table 12: API Security Standards

# Appendix B - Authentication

## Anonymous Authentication

**[Not Recommended]{.smallcaps}**

This is where the customer and the application they are using can gain
access to backend API services without needing to authenticate in any
way.

![](media/image30.png){width="5.2846303587051615in"
height="1.3276870078740157in"}

[]{#_Toc74234886 .anchor}Figure 34: Anonymous Authentication Model

This approach can be used when the risk associated with the API is
negligible e.g. an API offering publicly available information. It can
be used for internal APIs if the agency's security policy allows.

The downside of this model is that it makes it difficult to gather
effective analytics, and therefore to understand the implications of
proposed changes to, and deprecation of, an API.

Although it is not recommended to use this pattern it sometimes has to
be included to support the scenario where a web application is making
calls, on the home or login page, to a back-end application server which
stores the pages and the related JavaScripts. In this case it is the API
Gateway that provides the security, along with the due diligence
required to ensure these pages and associated JavaScripts do not contain
information that should be secured.

The Anonymous authentication model should be protected against typical
API vulnerabilities and threats, as listed on the OWASP (Open Web
Application Security Project) web site. Typically, these relate to:

1.  Throttling to prevent Denial of Service attacks

2.  Message analysis to block HTTP attacks parameter attacks such as
    cross-site scripting, SQL injection, command injection and cross
    site request forgery

Note: If this approach is used, it might be appropriate to restrict
access to the API based on other information (e.g. based on IP address).
This capability can be applied using an API Gateway, or existing
capabilities (e.g. firewalls, load balancers etc) may be able to provide
this level of protection

## Username and Password Authentication (Direct Authentication) 

**[Not Recommended]{.smallcaps}**

In the Direct Authentication model, the user is authenticated via an
identity store using username and password (or hash) credentials over
secure communications.

Username and Password Authentication is suitable for development
purposes, during training or the initial stages of development because
it reduces the barrier to accessing the API. It could also be used for
internal APIs, if the agency's security policy allows, and may be
suitable for customers if the identity risk[^8] associated with the API
is low.

Internal users would likely use an internal LDAP directory (e.g. Active
Directory) whilst external users (e.g. customers) would require a
separate identity store. The API Gateway could provide the
authentication services and, for external facing APIs, also threat
protection services.

API security is provided by the Application (Web) Server acting as a
trusted subsystem with TLS links to the backend API Server. The
Application/Web Server invokes the backend and provides the required
user ID information, which can be in the form of a session token.

![](media/image31.png){width="5.901388888888889in"
height="3.703472222222222in"}

[]{#_Toc74234887 .anchor}Figure 35: HTTP Basic / Digest Authentication
Model

This model can be easy to implement but has many limitations:

1.  An identity store (e.g. LDAP) is required along with a full
    registration process for all user types (e.g. applications and
    application developers)

2.  Cannot leverage a federated authentication model, so no single sign
    on (SSO), requiring re-presentation of username and password at
    every step

3.  Passwords would be in clear text. If direct authentication is used,
    TLS would be required to secure all communications

4.  Open to brute force attacks

5.  Passwords have low entropy, have to be reset and managed, and are
    difficult to revoke at a granular level

This model can be used for testing and development purposes but is **Not
Recommended** for production APIs; API Keys are preferred. Refer to the
NZ Evidence of Identity Standard for guidance on customer
authentication. If considering using this model for internal users,
preference would be a Single Sign-On solution using Kerberos.

## API Keys Authentication

**[Recommended]{.smallcaps}**

API Keys are a digital authentication mechanism, with the API key taking
the form of a long string of generated characters. API keys are usually
unique and can be assigned to an application, developer, or user. The
usual practice is for an application developer to obtain a key for their
application from the API provider and utilise the key within their
application. To obtain an API key, the developer must undergo a
registration process with the API Provider. The steps involved in the
registration process are dependent on the level of risk associated with
the API.

![](media/image32.png){width="5.901388888888889in"
height="2.6152777777777776in"}

[]{#_Toc74234888 .anchor}Figure 36: API Key Authentication

At run time, the consuming application automatically passes the API Key
to the API every time it requests an API resource. The API Gateway
validates the API Key against the API Key Store (which can be part of
the API Gateway functionality or provided by another secure device)
before allowing the consuming application access to the requested API
(or set of APIs) and backend resources.

This model is similar to the Username and Password model, but it is the
API Gateway which can be responsible for creating, managing the API key
and API secret and storing a copy in the API key store for validation,
rather than redirecting to an identity store for policy validation and
approval.

Username and password authorisation models can have high administration
and response time overheads (relating to cryptographic functions). API
keys are not linked to users and require no cryptographic functions.
Like usernames and passwords, they come in pairs and are defined below:

-   API Key - public unique identifier -- a 40+ random character string
    to authenticate the consuming application to the API

-   API Secret -- private unique identifier- only known by the API
    Gateway and used to validate the API key. The API secret in this
    model is not passed over the network.

API Keys should be used wherever system to system authentication is
needed (especially with a production level API). They are suitable for
simple public APIs which do not need more complex authentication models.
API Keys should be used in preference to username and passwords because:

-   More secure - greater entropy than passwords -- random long string
    of characters

-   Speed -- API keys do not involve any hashing process, i.e. the
    hashing process required for passwords

However, the risk is that anyone with a copy of the API key can use it
as though they were the legitimate consuming application. Hence all
communications should be over TLS, to protect the key in transit. The
onus is on the application developer to properly protect their copy of
the API key. If the API key is embedded into the consuming application,
it can be decompiled and extracted. If stored in plain text files they
can be stolen and re-used for malicious purposes.

Note: API Keys are recommended as they provide a level of security to
public APIs that can help protect sites from screen scraping or provide
the required information to throttle, or possibly bill, access to data.
Organisations need to carry out a risk analysis of the possible threats
against the classification of the data that could be obtained and from
this decide if API Keys are required.

## Certificates (Mutual) Authentication

Use this model when the API requires stronger authentication[^9] than
offered solely by API Keys, and the overhead of certificate management
is warranted.

In Certificate (Mutual) Authentication, internal and external parties
are authenticated with each other. Both the consuming application and
the API provider hold a digital certificate. The digital certificate can
be trusted because it was issued by a mutually trusted Certificate
Authority (CA). When the consuming application makes a request to the
API, the server hosting the API presents its certificate to the
consuming app. The app verifies the server's certificate then sends its
own certificate to the server. The server verifies the client
certificate and mutual trust is achieved, allowing the consuming
application to use the API.

![](media/image33.png){width="5.901388888888889in"
height="2.4750185914260716in"}

[]{#_Toc74234889 .anchor}Figure 37: Certificate Authentication

This is **Not Recommended** for customer authentication as there would
be a high overhead in terms of certificate management.

This is **Recommended** for consuming application to server (gateway) or
API to back-end communications (if needed).

Refer to the NZ Information Security Manual for guidance.

## Developer Authentication

> Developer authentication will normally take place at the API Portal
> when gaining access to APIs.
>
> The API Portal will offer an authentication solution for developers to
> provide a username and password (possible two factor) login process
> (See Figure 33) and a user store. Further details for this are not
> provided in this document, but a vendor API Portal will normally
> provide their own authentication solution and user store, or it can
> integrate with an existing identity and access management system.

![Graphical user interface, text, application Description automatically
generated](media/image34.png){width="5.173513779527559in"
height="3.5267311898512688in"}

[]{#_Toc74234890 .anchor}Figure 38: API Portal Login Page

> Once the developer has logged into the API Portal they can browse and
> discover the APIs available. API Portals normally require the
> consuming application developer to:

1.  Provide contact details e.g. email address

2.  Register the application they are developing

> The API Portal should provide registration services for the client
> application to use:

1.  API keys for basic authentication services and API monitoring

2.  OAuth services and the management of Client ID and a Client Secrets
    (for applications)

3.  Additional production authentication and authorisation service e.g.
    basic, certificate etc.

## Multi Factor Authentication (MFA)

> An application could use multi-factor authentication (MFA) to enhance
> other authentication techniques to mitigate identity risks. For
> example, by requesting a fingerprint from the customer in addition to
> their username and password (or API key).
>
> Often smartphone capabilities can be leveraged to provide this
> additional factor, but other options are available, like smart cards
> or hardware tokens.

# Appendix C - OAuth 2.0

OAuth 2.0 is a Token-based authorisation framework and is defined and
implemented using Grant Flow type patterns. These define the different
types of interaction a client application can perform to gain an "access
token" and thus access to the protected resource.

There are four grant type flows supported by the OAuth 2.0:

1.  Authorisation Code

2.  Implicit

3.  Resource Owner Password Credentials

4.  Client Credentials

## Grant Types 

> The following table explains which grant flow type to use for which
> situation:

+----------------------------------------+-----------------------------+
| Description                            | Recommendations             |
+========================================+=============================+
| **Authorisation Code**                 |                             |
+----------------------------------------+-----------------------------+
| Use for Internal Users or where the    | **Recommended**             |
| Customer is the Resource Owner, your   |                             |
| agency controls the Resource Server,   | The most secure OAuth flow. |
| but the Authorisation server is not    |                             |
| owned by the agency or is elsewhere    | Use for public facing APIs  |
| within the organisation.               | for Customer Authorisation  |
|                                        | patterns.                   |
| -   The Authorisation Server provides  |                             |
|     the Authorisation Code (grant) to  | Use for Internal Use Only   |
|     the client application once the    | pattern.                    |
|     Resource Owner has approved the    |                             |
|     request                            | Use the state attribute to  |
|                                        | link request and response.  |
| -   The client application then uses   |                             |
|     this to request the access token   | It is now recommended to    |
|                                        | include PKCE in this flow.  |
| -   The Authorisation Server validates |                             |
|     the client application using the   |                             |
|     Client ID and Client Secret. The   |                             |
|     client application has to store    |                             |
|     these credentials securely         |                             |
|                                        |                             |
| -   The client application             |                             |
|     authenticates to the Authorisation |                             |
|     Server via its TLS certificate and |                             |
|     call-back URL                      |                             |
|                                        |                             |
| Useful if the API requires a customer  |                             |
| of a client application to authorise   |                             |
| access to a protected resource         |                             |
| provided by the API.                   |                             |
+----------------------------------------+-----------------------------+
| **Implicit**                           |                             |
+----------------------------------------+-----------------------------+
| Used when the client application       | **Not Recommended**         |
| resides on a device (e.g. smartphone)  |                             |
| and cannot secure the credentials.     | The least secure grant      |
|                                        | type.                       |
| Only the "Access token" is transmitted |                             |
| from the Authorisation Server to the   | If used it should ONLY be   |
| client.                                | for information that is     |
|                                        | public and ONLY for GETs.   |
+----------------------------------------+-----------------------------+
| **Resource Owner Password              |                             |
| Credentials**                          |                             |
+----------------------------------------+-----------------------------+
| The Resource Owner's username and      | **Not Recommended**         |
| password are used once as the          |                             |
| Authorisation grant to obtain an       | Use for Customer            |
| Access Token. The credentials are then | Authorisation pattern if    |
| discarded.                             | Authorisation Code grant    |
|                                        | flow can't be used.         |
|                                        |                             |
|                                        | Use for Internal Use Only   |
|                                        | pattern to secure Internal  |
|                                        | APIs that use Active        |
|                                        | Directory Groups / Kerberos |
|                                        | for authorisation and       |
|                                        | authentication if           |
|                                        | Authorisation Code grant    |
|                                        | flow is not available.      |
+----------------------------------------+-----------------------------+
| **Client Credentials**                 |                             |
+----------------------------------------+-----------------------------+
| The client application is able to      | **Recommended**             |
| obtain access to the protected         |                             |
| resource on its own behalf.            | Use:                        |
|                                        |                             |
|                                        | -   For the Authorise       |
|                                        |     Consuming Application   |
|                                        |     pattern from device to  |
|                                        |     API                     |
|                                        |                             |
|                                        | -   Also use for Server to  |
|                                        |     Server (B2B), using     |
|                                        |     signed tokens           |
|                                        |                             |
|                                        | -   when the Customer using |
|                                        |     the client, application |
|                                        |     is also the Resource    |
|                                        |     Owner                   |
+----------------------------------------+-----------------------------+

[]{#_Toc74234999 .anchor}Table 13: OAuth 2.0 Grant Types

This table compiles the different grant types and provides
recommendations for agencies implementing an API Security Framework.
Recommendations are based on maximising the level of security for the
APIs being exposed.

OAuth 2.0 introduced different grant types to provide organisations with
the flexibility to support a variety of client application models. These
specific models are not device driven i.e. there is no specific device
(e.g. mobile) mapping to grant type; it is the level of risk an agency
is prepared to support that needs to be defined to clarify which grant
type should be selected.

For the application developer, the difference is in the infrastructure
they need to provide e.g. the "Authorisation Code" model requires a
managed server on which the client application runs.

The "Authorisation Code" is the most frequently used model and as it is
regarded as the most secure model it is covered in more depth later in
this document. The Implicit grant is the least secure and to quote from
the OAuth RFC:

> *"Implicit grants improve the responsiveness and efficiency of some
> clients (such as a client implemented as an in-browser application),
> since it reduces the number of round trips required to obtain an
> access token. However, this convenience should be weighed against the
> security implications of using implicit grants"*

These OAuth 2.0 Grant flow types replace the two-legged and three-legged
patterns used in OAuth 1.0.

There is now an RFC that has been defined that provides a Device
Authorization Grant flow (grant_type) that has been developed to address
"browser less" devices e.g. smart TVs, printers etc. and uses another
device to connect to the authorisation server to approve the request via
a polling process.

# Appendix D - OAuth 2.0 and OpenID Connect Tokens & Credentials

Access tokens are becoming a standard form of access control without the
need for passing credentials. Anyone with an access token (bearer token)
is permitted access to the resource being controlled, which makes tokens
a target for stealing or copying. Hence it is important to keep the
lifetime of tokens as short as realistically possible, depending on the
type of resource being exposed and business risk appetite.

The OAuth framework (RFC 6749 and 6750) relies heavily on TLS for the
security of the bearer token. The following RFCs offer additional
integrity and confidentiality capability that can be applied to the
bearer token (access token):

-   JSON Web Token (JWT) Profile for OAuth 2.0 Client Authentication and
    Authorization Grants (RFC 7523)

-   Proof-of-Possession Key Semantics for JSON Web Tokens (JWTs) (RFC
    7800)

There are two types of tokens, Opaque and JWTs. Both the access and
refresh token can be presented in either form.

The Opaque Tokens are produced by, and stored in, the Authentication
Server. Each one has a specific task in the OAuth 2.0 framework.

The JWT tokens are produced and signed by the Authorisation Server but
are not stored there. They are stored by the Client Application and when
used are verified by the signature.

The table below provides a list of the main tokens and credentials that
are used to provide authentication and authorisation services in the
OAuth 2.0 framework.

+-------------------------------------+--------------------------------+
| Description                         | Recommendation                 |
+=====================================+================================+
| > **Access Tokens (Opaque)**        |                                |
+-------------------------------------+--------------------------------+
| Also called bearer tokens. No       | -   It is **Required** that    |
| additional identity checks are      |     the token be protected     |
| carried out once this has been      |     both in transit (TLS) and  |
| issued.                             |     in storage (encryption)    |
|                                     |                                |
| Used by the client application to   | -   The "Authorisation Request |
| access protected resources on the   |     Header Field" format is    |
| provider, and it can be signed.     |     **Required** to only be    |
|                                     |     used to transmit tokens    |
| It is a random character string     |                                |
| that also contains "scope"          | -   It is **Recommended** that |
| information to allow additional     |     the lifetime of this token |
| access policies to be applied e.g.  |     be set to 60 mins          |
| duration of access.                 |                                |
|                                     | -   It is **Recommended** that |
| It is granted by the Resource Owner |     scopes be used for coarse- |
| via the Authorisation Grant Token   |     and fine-grained access    |
| Flow and enforced by Authorisation  |                                |
| and Resource Servers.               | -   Form-Encoded Body          |
|                                     |     Parameter is **Not         |
|                                     |     Recommended** for          |
|                                     |     transmission               |
|                                     |                                |
|                                     | -   URI Query Parameter is     |
|                                     |     **Not Recommended** for    |
|                                     |     transmission               |
+-------------------------------------+--------------------------------+
| > **Refresh Token (Opaque)**        |                                |
+-------------------------------------+--------------------------------+
| Used to obtain new Access tokens    | -   It is **Required** that    |
| when the old one expires or is      |     the token be protected     |
| invalid.                            |     both in transit (TLS) and  |
|                                     |     in storage (encryption)    |
|                                     |                                |
|                                     | -   It is **Recommended** that |
|                                     |     the lifetime of this token |
|                                     |     be set to 24 hours         |
+-------------------------------------+--------------------------------+
| > **Opaque Tokens vs JWTs**         |                                |
+-------------------------------------+--------------------------------+
| Access and Refresh Tokens can be    | -   It is **Recommended** that |
| delivered as an Opaque string or as |     organisations investigate  |
| a JWT that is signed, and if        |     both options and           |
| required can be encrypted. Possible |     understand the differences |
| pros and cons of the JWT are:       |     between the two and        |
|                                     |     defined how one over the   |
| 1.  JWTs are self-contained as all  |     other can provide          |
|     the information required is     |     additional security        |
|     within the token                |     controls or limits         |
|                                     |     complexity.                |
| 2.  JWTs provide signing services   |                                |
|     to allow the verification of    | -   It can be noted that there |
|     the token                       |     is a move towards the JWT  |
|                                     |     token as it can be used in |
| 3.  JWT are harder to revoke        |     the microservice space as  |
|                                     |     the claims information are |
|                                     |     contained inside.          |
+-------------------------------------+--------------------------------+
| > **Authorisation Code**            |                                |
+-------------------------------------+--------------------------------+
| The Authentication Server sends the | It is **Recommended** that the |
| Authorisation Code to the Client    | lifetime of this token be set  |
| after being granted consent by the  | to 24 hours                    |
| Resource Owner.                     |                                |
|                                     |                                |
| Used to authenticate the client.    |                                |
+-------------------------------------+--------------------------------+
| > **API Key**                       |                                |
+-------------------------------------+--------------------------------+
| A 40+ random character string used  | **Required** when implementing |
| in some scenarios to authenticate   | an authorisation solution that |
| the client application to the API.  | uses API Keys. This is         |
|                                     | normally presented as an       |
|                                     | option in the developer API    |
|                                     | Portal.                        |
+-------------------------------------+--------------------------------+
| > **Client ID**                     |                                |
+-------------------------------------+--------------------------------+
| When registering an OAuth Client    | **Required** when implementing |
| application with the API Portal, a  | an OAuth 2.0 model that        |
| Client ID is issued.                | supports "Authorisation Code"  |
|                                     | flow                           |
| Used when interacting with the      |                                |
| Resource Server.                    |                                |
+-------------------------------------+--------------------------------+
| > **Client Secret**                 |                                |
+-------------------------------------+--------------------------------+
| Also provided when the OAuth Client | **Required** when implementing |
| application is registered. This is  | an OAuth 2.0 model that        |
| used with the Client ID when        | supports "Authorisation Code"  |
| exchanging an authorisation code    | flow                           |
| for an access token                 |                                |
+-------------------------------------+--------------------------------+
| **ID Token**                        |                                |
+-------------------------------------+--------------------------------+
| ID Tokens are JWTs that can be used | It is **Recommended** that     |
| to:                                 | there are incorporated into    |
|                                     | any OAuth 2.0 / OpenID Connect |
| 1.  Authenticate a user             | environments as they provide   |
|                                     | additional security controls   |
| 2.  Collect information about a     | that allow a higher level of   |
|     user and send it in a           | communication trust between    |
|     verifiable format that can be   | the Relying Party the Identity |
|     trusted by the relying party    | Provider and the service being |
|                                     | protected.                     |
| 3.  Provide information in the      |                                |
|     token that can be used to       | Using ID tokens to provided    |
|     customise the Client            | verified claims is also        |
|     application or to provide       | **Recommended** to provide     |
|     claims for an access policy     | finer grained access to        |
|                                     | services                       |
| 4.  Provide a set of hashed claims  |                                |
|     that can be used to verify that |                                |
|     the ID Token and related Access |                                |
|     / Refresh Tokens can be from    |                                |
|     the Service Provider.           |                                |
+-------------------------------------+--------------------------------+
| **MTLS**                            |                                |
+-------------------------------------+--------------------------------+
| MTLS allows a higher level of trust | When the relying party (who    |
| between different parties when      | owns the Client, application   |
| exchanging credentials.             | is communicating with the      |
|                                     | OpenID (Identity) Provider for |
|                                     | exchanging credentials it is   |
|                                     | **Recommended** that it is     |
|                                     | carried out over MTLS          |
|                                     |                                |
|                                     | It is also **Recommended**     |
|                                     | that organisations should      |
|                                     | implement a                    |
|                                     | proof-of-possession /          |
|                                     | holder-of-key capability that  |
|                                     | ties the MTLS certificate to   |
|                                     | the Access Token when handling |
|                                     | confidential / restricted      |
|                                     | information                    |
+-------------------------------------+--------------------------------+
| **JWT (private_key_JWT)**           |                                |
+-------------------------------------+--------------------------------+
| OAuth 2.0 Clients Applications can  | It is **Recommended** that     |
| use Client IDs. and Client secrets  | organisations implement this   |
| to authenticate to the services     | form of client authentication  |
| (e.g. token generation, user        | when protecting confidential   |
| information and access revoke).     | (and above) information        |
|                                     |                                |
| In RFC 7523 the concept of using    |                                |
| JWTs for Client Authentication.     |                                |
| This provides additional controls   |                                |
| over the standard Client ID and     |                                |
| Secret, and it mandates that the    |                                |
| JWT is signed and verified, that it |                                |
| contains the required claims which  |                                |
| are validated, and ones (e.g. jti   |                                |
| -- JWT ID) that are used to ensure  |                                |
| the JWT is not used twice.          |                                |
+-------------------------------------+--------------------------------+

[]{#_Toc74235000 .anchor}Table 14: OAuth 2.0 Tokens & Credentials

## OAuth Scenario (Authorisation Code Grant Flow)

> This is a hypothetical scenario to demonstrate a key OAuth pattern
> using the Authorisation Code grant flow. In this scenario IRD has
> developed a set of APIs that can be used by professional accounting
> firms to offer additional services to their customers.
>
> The assumption here is that IRD have an API Gateway, that offers:

1.  API Developer Portal

2.  OAuth Authorisation Server

3.  Resource Server, exposing the APIs that can be called

4.  That IRD are securing an API called "View IRD Return" with an
    Authorisation Code Grant Type

### Stage 1 -- Develop the Application (3^rd^ Party)

> The third party (in this case MyAccountantWebsite.com) develops a
> client application that will be exposed to their customers when they
> login to their website. It will allow customers of MyAccountantWebSite
> to authorise and set up delegated access for the MyAccountantWebSite
> application to view their IRD returns, but without the customer having
> to provide their IRD username and password to MyAccountantWebsite.
>
> The application will use the APIs exposed by IRD and is developed on
> an MyAccountantWebsite.com Application (Web) Server that can securely
> store security credentials.

### Stage 2 -- Register the (Client) Application

The developer needs to register as a user of the IRD API Portal. IRD
needs to verify that this person is allowed to register as a user. (This
process is outside the scope of this document and will vary depending on
the sensitivity of the APIs exposed.)

The authentication of the developer can be via:

-   IRD's internal client login services

-   An external Identity Service provided (OpenID Connect or SAML based,
    or Social Network Identity provider)

Once the developer has been approved and has been granted login
credentials (username and password) they log onto the IRD API Portal and
register their client application; this is carried out over a TLS secure
link. The following information is provided:

-   The name of the application (by the Developer)

-   Return URL (by the Developer)

-   Client ID (by IRD) -- stored securely

-   Client Secret (by IRD) -- stored securely

The developer completes development of the client application on
MyAccountantWebsite. The next steps detail how the MyAccountantWebsite
customer uses the application.

Note: the values of the Client ID and Secret are represented as simple
strings below. In reality these are long, randomly generated strings.

![](media/image35.png){width="4.982496719160105in"
height="2.8442082239720037in"}

[]{#_Toc74234891 .anchor}Figure 39: Stage 2 Client Registration

### Stage 3 --Customer Sets New Service and Authorises Access

The Customer logs into MyAccountantWebsite from their browser and clicks
on the IRD button (View IRD) which should allow the user access to
information presented by the "View IRD Return" API (see Figure 21: Stage
3 Client Registration below). As there is no current "Access Token"
stored for the client application to use, the user is redirected to the
IRD Authorisation Server "Authorisation End Point" with the following
information:

1.  IRD URL A (Authorisation endpoint URL)

2.  Return URL (where the authorisation code will be sent)

3.  Client ID = ABC (random long string that is used to identify the
    client application)

4.  Scope = READ (defined by the application as to what the application
    can do)

5.  State = xyz123 (random long string that is used to mitigate man in
    the middle attacks)

![](media/image36.png){width="5.428406605424322in"
height="3.4807469378827647in"}

[]{#_Toc74234892 .anchor}Figure 40: Stage 3 Client Registration

### Stage 4 -- Authentication and Approval by the Resource Owner

As the client application doesn't have an access token for this
customer, or a session set up with IRD, the customer is redirected to
the IRD login page. The customer then logs into IRD and will be
presented with a request to accept the scopes (in this case READ) for
MyAccountantWebsite access.

![](media/image37.png){width="4.901414041994751in"
height="3.4508311461067365in"}

[]{#_Toc74234893 .anchor}Figure 41: Stage 4 Client Registration

### Stage 5 -- Provide an Authentication Code

With the customer's acceptance of the scope, the Authorisation server
sends an Authorisation code to the client application (with the same
state parameter for the client to validate).

![](media/image38.png){width="5.0919477252843395in"
height="3.2650054680664917in"}

[]{#_Toc74234894 .anchor}Figure 42: Stage 5 Client Registration

### Stage 6 --Authorisation Code is Sent to Token Endpoint 

To gain access to API resources, the client application sends the
Authorisation Code to the Token endpoint (T on the diagram below) on the
Authorisation Server, along with the Client ID and Client Secret it
received when the client application was registered. This is used for
authentication of the client application to the authorisation server.
Note: The communication must be over TLS.

![](media/image39.png){width="5.603139763779527in"
height="3.5927887139107613in"}

[]{#_Toc74234895 .anchor}Figure 43: Stage 6 Client Registration

### Stage 7 -- The Access Token It Provides

The Authorisation Server provides an Access token back to the client
application, along with a refresh token (for later use) and an expiry
time for the Access token.

![](media/image40.png){width="5.1486132983377075in"
height="3.2715780839895015in"}

[]{#_Toc74234896 .anchor}Figure 44: Stage 7 Client Registration

### Stage 8 -- The Client Application uses the Access Token to Access the Resource 

The Client Application presents the Access Token to the Resource Server
at IRD, which is verified by the Authorisation Server and the requested
data is returned from the IRD back end system via the View IRD Return
API to the MyAccountantWebsite client application.

![](media/image41.png){width="5.901388888888889in"
height="3.7840277777777778in"}

[]{#_Toc74234897 .anchor}Figure 45: Stage 8 Client Registration

This completes the OAuth scenario, as the client application has
retrieved, and can use, the resource data returned from the API.

[]{#_Toc74234793 .anchor}

# Appendix E - Authorisation 

## ABAC Implementation

To implement Attribute Based Access Control, the current models defined
use XACML.

XACML (developed by OASIS), provides a reference architecture, a request
/ response protocol and a policy language.

It is a highly distributed and loosely coupled architecture. It provides
very useful generic definitions of the required components (services)
which can be used to define any access control model.

It uses the following services to define the reference architecture:

1.  Policy Enforcement Point (PEP) -- where the request to the resource
    is intercepted and policy applied (based on the decision made by the
    Policy Decision Point)

2.  Policy Decision Point (PDP) -- This is the policy server to which
    the PEP sends the request for evaluation as to whether a user should
    or should not have access to a resource. The PDP has access to
    policy and can match the credentials and request against policy to
    make a permit/deny decision. It can also enforce policy related
    obligations e.g. enhanced logging, notification and alerts, or
    re-routing to request additional authorisation process.

3.  Policy Administration Point (PAP) -- The interface where the
    policies are developed and defined

4.  Policy Information Point (PIP) -- Used to gather additional
    information about a user from Identity stores or databases to
    provide additional attributes that are required by the PDP to
    validate the policy and apply the required outcome.

The links and flows between these services are detailed in the diagram
below:![Diagram Description automatically
generated](media/image42.png){width="4.643859361329834in"
height="2.6410640857392824in"}

[]{#_Toc74234898 .anchor}Figure 46: XACML Reference Architecture

XACML is generally perceived as being difficult to write policies in,
but this is being addressed in two ways:

1.  OASIS is developing a Request/Response Interface based on JSON and
    HTTP for XACML 3.0, Version 1.0

2.  There is a JSON-based language called ALFA (Abbreviated Language for
    Authorization) which can be used to build XACML policies

For XACML to support fine grained access for APIs requires a model such
as is illustrated in the diagram below (based on the scenario in section
1.5.6).

![Diagram Description automatically
generated](media/image43.png){width="5.835207786526684in"
height="1.831314523184602in"}

[]{#_Toc74234899 .anchor}Figure 47: ABAC Support for APIs

> It follows these steps:

1.  The access token is obtained during the request and exchange process

2.  The access token is presented during the resource request to the
    PEP, which also exposes the resource

3.  The access request is passed to the Authorisation Server

4.  The Authorisation Server verifies the access token and passes a
    XACML request to the PDP. This is where additional fine-grained
    access can be applied.

5.  The PDP authorises the PEP to allow access to the back-end service

# Appendix F - Security Controls

This section captures a number of key controls that should be applied.
It is recommended that organisations should the relevant RFC (or active
draft documents) that relate to securing APIs. For example:

[[https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics-18.txt]{.underline}](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics-18.txt)

## Communications Security (Confidentiality)

**[Required]{.smallcaps}**

All communications to or from an API must be over TLS 1.3 or higher.
Other versions of TLS and SSL should be disabled. This provides a
recognised level of confidentiality that covers all communications
between all components.

The consuming application must validate the TLS certificate chain when
making requests to protected resources, including checking the
Certificate Revocation List (CRL).

## State (Integrity)

State is also a parameter that can be used during the authorisation
grant stage to provide a level of security to address possible
man-in-the-middle attacks. The state parameter is a string of random
letters and numbers that is sent to the Authorisation Server by the
client when requesting an authorisation code. It is sent back to the
client with the Authorisation Code and should be verified by the client
application to confirm the authenticity of the response i.e. it came
from the authorisation server to which the request was sent.

Note: State is used to provide a level of integrity when using the
standard format of bearer tokens. The confidence in the level of
integrity can be increased if JWT tokens are used for bearer tokens.

## Content Encryption (Confidentiality)

If content needs only to be visible to specific consumer endpoints, use
encryption. However, if content only needs to be guaranteed untampered
and/or from a specific source (e.g. provider) then use content signing.
Content encryption enables all or part of a JSON payload to be readable
only by the target consumer(s). This is useful where the content being
carried by the API is sensitive, and the API request or response
transits multiple stopping points. Whilst TLS protects the payload in
transit, it only applies to each point to point connection between
components (e.g. mobile app to API gateway). If transit components are
not totally under the provider's control, it can be worthwhile
performing body encryption. E.g. it may be sensible to encrypt credit
card details passed between consumer and provider backend systems.

It is also worth considering how much protection the information needs
whilst at rest (e.g. information received from consuming applications,
caches) and whether some content should be stored encrypted.

Encryption is only worthwhile implementing when data sensitivity or data
protection requirements drive it, as encryption is computationally
intensive. It also makes it more difficult for protection mechanisms,
such as API gateways, to validate and transform API content. When only
the integrity of the content passed needs to be ensured, consider using
Content Signing (section 1.7.4) instead.

There are many existing ways of encrypting message content, built into
code libraries and development tools. It is Required that any content
encryption adheres to the standard algorithms laid out in NZISM (HMAC
Algorithms).

## Content Signing (Integrity)

Content signing is used to assure content integrity and proof of
authorship. It can apply to the whole body of the JSON message or
specific elements of that content e.g. credit card details. There are
many approaches to content signing and the most appropriate approach is
requirements dependent. Standard signing algorithms exist within coding
libraries, and JWT has a body which can contain verifiable (signed) JSON
fields. API Gateways can also be configured to sign content objects in
transit, if provided with an appropriate private key.

Signing has less of a computational overhead than encryption, but can
still affect performance, so it is advisable that it be used only when
and where needed.

For APIs, this is a developing area: there are standards currently under
development to address content signing:

-   Message Authentication Code - OAuth 2.0 Message Authentication Code
    (MAC) Tokens (draft)

-   Proof of Possession - OAuth 2.0 Proof-of-Possession (PoP) Security
    Architecture (draft)

It is **Recommended** that where Bearer Tokens are used, they should be
signed using JSON Web Tokens (JWT) as defined in:

-   JSON Web Token (JWT) RFC 7519

-   JSON Web Signature (JWS) RFC 7515

-   JSON Web Token (JWT) Profile for OAuth 2.0 Client Authentication and
    Authorization Grants RFC 7523

## Non-Repudiation (Integrity)

Non-repudiation covers the means to ensure that a consumer cannot deny
making a request and, similarly, a provider cannot claim they did not
send a response. To aid non-repudiation for APIs, it is important to
ensure credentials are not shared between consumers and to perform
comprehensive logging of API request/responses.

Digital signatures are useful for not just guaranteeing authenticity and
integrity, but also supporting non-repudiation.

## Availability and Threat Protection

Below is a table of risk types and some recommended approaches to help
mitigation these threats:

+---------------------------------+------------------------------------+
| Threat                          | Mitigation (OWASP)                 |
+=================================+====================================+
| Exposure of inappropriate API   | Protect and Limit (whitelist) the  |
| methods to access services      | HTTP Methods (GET, PUT etc)        |
|                                 | exposed                            |
|                                 |                                    |
|                                 | Validate Method(s) for session     |
|                                 | token / API key.                   |
+---------------------------------+------------------------------------+
| Denial of Service attacks       | Throttle access to all exposed     |
|                                 | APIs. Monitor use to indicate      |
|                                 | possible DoS attacks               |
+---------------------------------+------------------------------------+
| Malicious Input, Injection      | Validate input: Secure parsing and |
| attacks and Fuzzing             | strong typing                      |
|                                 |                                    |
|                                 | Validate incoming content-type     |
|                                 | application/json                   |
|                                 |                                    |
|                                 | Validate JSON content              |
|                                 |                                    |
|                                 | Validate XML (schema and format)   |
|                                 |                                    |
|                                 | Scan attachments                   |
|                                 |                                    |
|                                 | Produce valid HTTP Return Code     |
|                                 |                                    |
|                                 | Validate response type             |
+---------------------------------+------------------------------------+
| Cross-Site Request Forgery      | Use tokens with state and nonce    |
|                                 | parameters                         |
+---------------------------------+------------------------------------+
| Cross-Site Scripting Attacks    | Validate Input                     |
+---------------------------------+------------------------------------+

[]{#_Toc74235001 .anchor}Table 15: Risks & Mitigations

## Token Threat Mitigation

Securing OAuth flows relies on the exchange of tokens between consuming
applications and API backend servers. There is always the threat of
these tokens being obtained illicitly, losing confidentiality and
integrity of message content or the integrity of the sender of the
token. This risk also applies to the transferring of API keys.

The table below captures the main Token threats and possible mitigation
strategies:

+---------------------------------+------------------------------------+
| Threat                          | Mitigation                         |
+=================================+====================================+
| Token Manufacture or            | Digital signing of tokens (e.g.    |
| modification (fake tokens and   | JWS with JWT) or attaching a       |
| man in the middle attacks)      | Message Authentication Code (MAC)  |
+---------------------------------+------------------------------------+
| Token disclosure -- man in the  | Communication Security             |
| middle attack.                  |                                    |
|                                 | Use TLS 1.3 with a cipher suite    |
| The Access Token is passed in   | that includes DHE or ECDHE         |
| clear text with no hashing,     |                                    |
| signing or encryption.          | The client application must        |
|                                 | validate:                          |
|                                 |                                    |
|                                 | -   The TLS certificate chain      |
|                                 |                                    |
|                                 | -   Check the certificate          |
|                                 |     revocation list\*              |
|                                 |                                    |
|                                 | \*Stored locally in a file or LDAP |
|                                 | server[^10]                        |
+---------------------------------+------------------------------------+
| Token Redirects.                | Using the "audience" header        |
|                                 | (defined currently in a draft RFC) |
| Ensure the Authentication and   | the client application, resource   |
| Resource Servers are "paired",  | server and authorisation server    |
| and the access token can only   | can help\* ensure that the token   |
| be used in this between the     | can only be used on the resource   |
| specified servers               | servers requested by the client    |
|                                 | and recognised by the              |
|                                 | authorisation server.              |
|                                 |                                    |
|                                 | Also addressed with "state"        |
|                                 | parameter in the header            |
|                                 |                                    |
|                                 | > \* Signing of tokens is also     |
|                                 | > applicable to address token      |
|                                 | > redirects                        |
+---------------------------------+------------------------------------+
| Token replay -- where the       | Limit lifetime of the token (e.g.  |
| threat actor copies an existing | 10 minutes) -- turning it into a   |
| token (e.g. refresh token or    | short-lived issue                  |
| authorisation code) and reuses  |                                    |
| it on their own request         | Use signed requests along with     |
|                                 | nonce and timestamps               |
|                                 |                                    |
|                                 | Validate TLS certificate chain     |
|                                 | when accessing Resource Server     |
+---------------------------------+------------------------------------+

[]{#_Toc74235002 .anchor}Table 16: Token Threat Mitigation

API Gateway capabilities can protect against many typical API
vulnerabilities and threats. Typically, these relate to:

-   Throttling to prevent Denial of Service attacks

-   Message analysis to block HTTP attacks; parameter attacks such as
    cross-site scripting, SQL injection, command injection and cross
    site request forgery

-   Controlling egress of information via the API, aligned to set access
    permissions/policies

As well as providing (if required) access control to API functionality.

[]{#_Toc74234803 .anchor}

# Appendix G - IETF NFC Relating to OAuth 2.0

+-----------------------------------+-----------------------------------+
| RFC number and Title              | High Level Description            |
+===================================+===================================+
| RFC 6749                          | The core OAuth 2.0 RFC defining   |
|                                   | the authorisation framework.      |
| The OAuth 2.0 Authorization       |                                   |
| Framework                         |                                   |
+-----------------------------------+-----------------------------------+
| RFC 6750                          | How to use bearer tokens in HTTP  |
|                                   | requests to access OAuth 2.0      |
| The OAuth 2.0 Authorisation       | protected resources. Any party in |
| Framework: Bearer Token Usage     | possession of a bearer token (a   |
|                                   | \"bearer\") can use it to get     |
|                                   | access to the associated          |
|                                   | resources (without demonstrating  |
|                                   | possession of a cryptographic     |
|                                   | key). To prevent misuse, bearer   |
|                                   | tokens need to be protected from  |
|                                   | disclosure in storage and in      |
|                                   | transport.                        |
|                                   |                                   |
|                                   | Note: RFC 8996 deprecates TLS 1.0 |
|                                   | and 1.1 and recommends 1.2 or     |
|                                   | ideally 1.3 in OAuth 2.0          |
|                                   | implementations)                  |
+-----------------------------------+-----------------------------------+
| RFC 6819                          | Security considerations for OAuth |
|                                   | beyond those in the OAuth 2.0     |
| OAuth 2.0 Threat Model and        | specification, based on a         |
| Security Considerations           | comprehensive threat model for    |
|                                   | the OAuth 2.0 protocol.           |
+-----------------------------------+-----------------------------------+
| RFC 7009                          | This profile defines a revocation |
|                                   | endpoint on the authorisation     |
| Token Revocation                  | server to enable clients          |
|                                   | (consuming applications) to       |
|                                   | revoke their own access or        |
|                                   | refresh tokens. This is essential |
|                                   | should a token get into the wrong |
|                                   | hands and be used for malicious   |
|                                   | purposes. Before allowing a       |
|                                   | client to revoke an access token  |
|                                   | and/or associated refresh tokens, |
|                                   | the authorisation server first    |
|                                   | validates the client's            |
|                                   | credentials.                      |
+-----------------------------------+-----------------------------------+
| RFC 7519                          | URL-safe means of representing    |
|                                   | claims to be transferred between  |
| JSON Web Token (JWT)              | two parties. The claims in a JWT  |
|                                   | are encoded as a JSON object that |
|                                   | is used as the payload of a JSON  |
|                                   | Web Signature (JWS) structure or  |
|                                   | as the plaintext of a JSON Web    |
|                                   | Encryption (JWE) structure,       |
|                                   | enabling the claims to be         |
|                                   | digitally signed or integrity     |
|                                   | protected with a Message          |
|                                   | Authentication Code (MAC) and/or  |
|                                   | encryption.                       |
+-----------------------------------+-----------------------------------+
| RFC 8725                          | This document updates RFC 7519 to |
|                                   | provide actionable guidance       |
| JSON Web Token Best Current       | leading to secure implementation  |
| Practices                         | and deployment of JWTs.           |
+-----------------------------------+-----------------------------------+
|                                   |                                   |
+-----------------------------------+-----------------------------------+
| RF7521                            | Common framework for OAuth 2.0 to |
|                                   | interact with other identity      |
| Assertion Framework for OAuth 2.0 | systems using an assertion and to |
| Client Authentication and         | provide alternative client        |
| Authorisation Grants              | authentication mechanisms.        |
+-----------------------------------+-----------------------------------+
| RFC 7522                          | The use of a Security Assertion   |
|                                   | Markup Language (SAML) 2.0 Bearer |
| Security Assertion Markup         | Assertion as a means for          |
| Language (SAML) 2.0 Profile for   | requesting an OAuth 2.0 access    |
| OAuth 2.0 Client Authentication   | token as well as for client       |
| and Authorization Grants          | authentication.                   |
+-----------------------------------+-----------------------------------+
| RFC 7523                          | Use of a JSON Web Token (JWT)     |
|                                   | Bearer Token as a means for       |
| JSON Web Token (JWT) Profile for  | requesting an OAuth 2.0 access    |
| OAuth 2.0 Client Authentication   | token as well as for client       |
| and Authorization Grants          | authentication.                   |
+-----------------------------------+-----------------------------------+
| RFC 7591                          | Mechanisms for dynamically        |
|                                   | registering OAuth 2.0 clients     |
| OAuth 2.0 Dynamic Client          | with authorisation servers.       |
| Registration Protocol             |                                   |
+-----------------------------------+-----------------------------------+
| RFC 7592                          | Methods for the management of     |
|                                   | OAuth 2.0 dynamic client          |
| OAuth 2.0 Dynamic Client          | registrations for use cases in    |
| Registration Management Protocol  | which the properties of a         |
|                                   | registered client may need to be  |
|                                   | changed during the lifetime of    |
|                                   | the client.                       |
+-----------------------------------+-----------------------------------+
| RFC 7662                          | Method for a protected resource   |
|                                   | to query an OAuth 2.0             |
| OAuth 2.0 Token Introspection     | authorisation server to determine |
|                                   | the active state of an OAuth 2.0  |
|                                   | token and to determine            |
|                                   | meta-information about this       |
|                                   | token. Provides authorisation     |
|                                   | context of the token from the     |
|                                   | authorisation server to the       |
|                                   | protected resource.               |
+-----------------------------------+-----------------------------------+
| RFC 7800                          | How to declare in a JSON Web      |
|                                   | Token (JWT) that the presenter of |
| Proof-of-Possession Key Semantics | the JWT possesses a particular    |
| for JSON Web Tokens (JWTs)        | proof-of-possession key and how   |
|                                   | the recipient can                 |
|                                   | cryptographically confirm proof   |
|                                   | of possession of the key by the   |
|                                   | presenter.                        |
+-----------------------------------+-----------------------------------+
| RFC 7636                          | OAuth 2.0 public clients          |
|                                   | utilising the Authorisation Code  |
| Proof Key for Code Exchange by    | Grant are susceptible to the      |
| OAuth Public Clients              | authorisation code interception   |
|                                   | attack. This specification        |
|                                   | describes the attack as well as a |
|                                   | technique to mitigate against the |
|                                   | threat through the use of Proof   |
|                                   | Key for Code Exchange.            |
+-----------------------------------+-----------------------------------+
| RFC 8176                          | Establishing a registry for       |
|                                   | Authentication methods for        |
| Authentication Method Reference   | example:                          |
| Values                            |                                   |
|                                   | -   Retina Scan                   |
|                                   |                                   |
|                                   | -   Facial Recognition            |
|                                   |                                   |
|                                   | -   Fingerprints                  |
|                                   |                                   |
|                                   | -   Geolocation information       |
|                                   |                                   |
|                                   | -   Proof of possession of a      |
|                                   |     hardware key                  |
|                                   |                                   |
|                                   | -   Knowledge based               |
|                                   |     authentication                |
|                                   |                                   |
|                                   | -   Multi-channel authentication  |
|                                   |                                   |
|                                   | -   Multi-factor authentication   |
|                                   |                                   |
|                                   | -   One-time password             |
|                                   |                                   |
|                                   | -   Personal Identification       |
|                                   |     Number                        |
|                                   |                                   |
|                                   | -   Password based                |
|                                   |                                   |
|                                   | -   Risk Based                    |
|                                   |                                   |
|                                   | -   SMS confirmation messages     |
|                                   |                                   |
|                                   | -   Proof of possession of a      |
|                                   |     software key                  |
|                                   |                                   |
|                                   | -   Confirm by telephone          |
|                                   |                                   |
|                                   | -   User presence test            |
|                                   |                                   |
|                                   | -   Voice biometrics              |
|                                   |                                   |
|                                   | -   Windows integration           |
+-----------------------------------+-----------------------------------+
| RFC 8252                          | This RFC recommends external      |
|                                   | user-agents like in-app browser   |
| OAuth 2.0 for Native Apps         | tabs as the only secure and       |
|                                   | usable choice for OAuth, rather   |
|                                   | than embedded user-agents.        |
+-----------------------------------+-----------------------------------+
| RFC 8414                          | This defines how an OAuth 2.0     |
|                                   | Client can interact with an       |
| OAuth 2.0 Authorization Server    | authorisation server by providing |
| Discovery Metadata                | a discovery endpoint that         |
|                                   | provides the endpoints and        |
|                                   | authorisation server capability.  |
+-----------------------------------+-----------------------------------+
| RFC 8628                          | The OAuth 2.0 device              |
|                                   | authorisation grant is designed   |
| OAuth 2.0 Device Authorization    | for Internet-connected devices    |
| Grant                             | that either lack a browser to     |
|                                   | perform a user-agent-based        |
|                                   | authorisation or are input        |
|                                   | constrained to the extent that    |
|                                   | requiring the user to input text  |
|                                   | in order to authenticate during   |
|                                   | the authorisation flow is         |
|                                   | impractical. It enables OAuth     |
|                                   | clients on such devices (like     |
|                                   | smart TVs, media consoles,        |
|                                   | digital picture frames, and       |
|                                   | printers) to obtain user          |
|                                   | authorisation to access protected |
|                                   | resources by using a user agent   |
|                                   | on a separate device.             |
+-----------------------------------+-----------------------------------+
| RFC 8693                          | Defines a protocol for a          |
|                                   | lightweight HTTP and JSON based   |
| OAuth 2.0 Token Exchange          | Security Token Service (STS) --   |
|                                   | covering requests of tokens from  |
|                                   | an Authorisation Server.          |
+-----------------------------------+-----------------------------------+
| RFC 8705                          | This document describes OAuth     |
|                                   | client authentication and         |
| OAuth 2.0 Mutual-TLS Client       | certificate-bound access and      |
| Authentication and                | refresh tokens using mutual       |
| Certificate-Bound Access Tokens   | Transport Layer Security (TLS)    |
|                                   | authentication with X.509         |
|                                   | certificates.                     |
|                                   |                                   |
|                                   | OAuth clients are provided a      |
|                                   | mechanism for authentication to   |
|                                   | the authorisation server using    |
|                                   | mutual TLS.                       |
|                                   |                                   |
|                                   | OAuth authorisation servers are   |
|                                   | provided a mechanism for binding  |
|                                   | access tokens to a client\'s      |
|                                   | mutual-TLS certificate, and OAuth |
|                                   | protected resources are provided  |
|                                   | a method for ensuring that such   |
|                                   | an access token presented to it   |
|                                   | was issued to the client          |
|                                   | presenting the token              |
+-----------------------------------+-----------------------------------+
| RFC 8707                          | This document specifies an        |
|                                   | extension to the OAuth 2.0        |
| Resource Indicators for OAuth 2.0 | Authorisation Framework defining  |
|                                   | request parameters that enable a  |
|                                   | client to explicitly signal to an |
|                                   | authorisation server about the    |
|                                   | identity of the protected         |
|                                   | resource(s) to which it is        |
|                                   | requesting access.                |
+-----------------------------------+-----------------------------------+
| RFC 6755                          | This document establishes an IETF |
|                                   | URN Sub-namespace for use with    |
| An IETF URN Sub-Namespace for     | OAuth-related specifications.     |
| OAuth                             |                                   |
+-----------------------------------+-----------------------------------+

[]{#_Toc74235003 .anchor}Table 17: IETF NFC Relating to OAuth 2.0

# Appendix H - RFCs in Development

The following are RFCs which are pertinent to this standard but are
currently under development:

+---------------------------------+------------------------------------+
| Description                     | High Level view                    |
+=================================+====================================+
| OAuth 2.0 JWT Secured           | This document introduces the       |
| Authorization Request           | ability to send request parameters |
|                                 | in a JSON Web Token (JWT) instead, |
|                                 | which allows the request to be     |
|                                 | signed with JSON Web Signature     |
|                                 | (JWS) and encrypted with JSON Web  |
|                                 | Encryption (JWE) so that the       |
|                                 | integrity, source authentication   |
|                                 | and confidentiality property of    |
|                                 | the Authorization Request is       |
|                                 | attained.                          |
+---------------------------------+------------------------------------+
| JWT Response for OAuth Token    | The introspection response, as     |
| Introspection                   | specified in OAuth 2.0 Token is a  |
|                                 | plain JSON object. This            |
|                                 | specification extends the token    |
|                                 | introspection endpoint with the    |
|                                 | capability to return responses as  |
|                                 | JWTs.                              |
+---------------------------------+------------------------------------+
| JSON Web Token (JWT) Profile    | This specification defines a       |
| for OAuth 2.0 Access Tokens     | profile for issuing OAuth 2.0      |
|                                 | access tokens in JSON web token    |
|                                 | (JWT) format. Authorisation        |
|                                 | servers and resource servers from  |
|                                 | different vendors can leverage     |
|                                 | this profile to issue and consume  |
|                                 | access tokens in an interoperable  |
|                                 | manner.                            |
+---------------------------------+------------------------------------+
| The OAuth 2.1 Authorization     | This is an in-progress update to   |
| Framework                       | version 2.0, Key points to note    |
|                                 | are:                               |
|                                 |                                    |
|                                 | 1.  PKCE is required for all OAuth |
|                                 |     clients using the              |
|                                 |     authorization code flow        |
|                                 |                                    |
|                                 | 2.  Redirect URIs must be compared |
|                                 |     using exact string matching    |
|                                 |                                    |
|                                 | 3.  The following grants are       |
|                                 |     omitted:                       |
|                                 |                                    |
|                                 |     a.  The Implicit grant         |
|                                 |                                    |
|                                 |     b.  The Resource Owner         |
|                                 |         Password Credentials       |
|                                 |                                    |
|                                 | 4.  Bearer token usage omits the   |
|                                 |     use of bearer tokens in the    |
|                                 |     query string of URIs           |
|                                 |                                    |
|                                 | 5.  Refresh tokens for public      |
|                                 |     clients must either be         |
|                                 |     sender-constrained or one-time |
|                                 |     use                            |
+---------------------------------+------------------------------------+
| OAuth 2.0 Security Best Current | This document describes best       |
| Practice                        | current security practice for      |
|                                 | OAuth 2.0. It updates and extends  |
|                                 | the OAuth 2.0 Security Threat      |
|                                 | Model to incorporate practical     |
|                                 | experiences gathered since OAuth   |
|                                 | 2.0 was published and covers new   |
|                                 | threats relevant due to the        |
|                                 | broader application of OAuth 2.0.  |
+---------------------------------+------------------------------------+
| OAuth 2.0 Rich Authorization    | This document specifies a new      |
| Requests                        | parameter                          |
|                                 | \"authorization_details\" that is  |
|                                 | used to carry fine grained         |
|                                 | authorisation data in the OAuth    |
|                                 | authorisation request.             |
+---------------------------------+------------------------------------+
| OAuth 2.0 Pushed Authorization  | Pushed authorization requests      |
| Requests                        | (PAR)enable OAuth Clients to push  |
|                                 | the payload of an authorisation    |
|                                 | request directly to the            |
|                                 | authorisation server in exchange   |
|                                 | for a request URI value, which is  |
|                                 | used as reference to the           |
|                                 | authorisation request payload data |
|                                 | in a subsequent call to the        |
|                                 | authorisation endpoint via the     |
|                                 | user-agent.                        |
+---------------------------------+------------------------------------+
| OAuth 2.0 Authorization Server  | This specifies a new parameter     |
| Issuer Identifier in            | \"iss\" that is used to explicitly |
| Authorization Response          | include the issuer identifier of   |
|                                 | the authorisation server in the    |
|                                 | authorisation response of an OAuth |
|                                 | authorisation flow. If implemented |
|                                 | correctly, the \"iss\" parameter   |
|                                 | serves as an effective             |
|                                 | countermeasure to \"mix-up         |
|                                 | attacks\" which are aimed to steal |
|                                 | an authorisation code or access    |
|                                 | token by tricking the client into  |
|                                 | sending the authorisation code or  |
|                                 | access token to the attacker       |
|                                 | instead of the honest              |
|                                 | authorisation or resource server.  |
+---------------------------------+------------------------------------+
| OAuth 2.0 Demonstrating         | This specification describes a     |
| Proof-of-Possession at the      | mechanism for sender-constraining  |
| Application Layer               | OAuth 2.0 tokens via a             |
|                                 | proof-of-possession mechanism on   |
|                                 | the application level and enables  |
|                                 | a client to demonstrate            |
|                                 | proof-of-possession of a           |
|                                 | public/private key pair by         |
|                                 | including a \"DPoP\" header (JWT)  |
|                                 | in an HTTP request, that enables   |
|                                 | the authorisation server to bind   |
|                                 | issued tokens to the public part   |
|                                 | of a client\'s key pair.           |
|                                 |                                    |
|                                 | This mechanism allows for the      |
|                                 | detection of replay attacks with   |
|                                 | access and refresh tokens.         |
+---------------------------------+------------------------------------+
| OAuth 2.0 for Browser-Based     | This specification describes the   |
| Apps                            | current best practices for         |
|                                 | implementing OAuth 2.0             |
|                                 | authorization flows in             |
|                                 | applications executing in a        |
|                                 | browser.                           |
|                                 |                                    |
|                                 | An application that is dynamically |
|                                 | downloaded and executed in a web   |
|                                 | browser, usually written in        |
|                                 | JavaScript. Also, sometimes        |
|                                 | referred to as a \"single-page     |
|                                 | application\", or \"SPA\".         |
|                                 |                                    |
|                                 | One of the key recommendations is  |
|                                 | the use of PKCE.                   |
+---------------------------------+------------------------------------+

[]{#_Toc74235004 .anchor}Table 18: RFCs in Development

[^1]: Identity relates to how a person (or thing) is represented and how
    this is used to access services or information. See
    https://www.digital.govt.nz/digital-government/programmes-and-projects/digital-identity-programme/what-is-digital-identity/

[^2]: [[https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf]{.underline}](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf)

[^3]: For more details, see Appendix C - OAuth 2

[^4]: [[https://kantarainitiative.org/confluence/display/uma/Home]{.underline}](https://kantarainitiative.org/confluence/display/uma/Home)

[^5]: [[https://www.gluu.org/]{.underline}](https://www.gluu.org/) and
    [[https://forgerock.org]{.underline}](https://forgerock.org) and
    [[https://wso2.com]{.underline}](https://wso2.com) and
    [[https://www.keycloak.org]{.underline}](https://www.keycloak.org)

[^6]: [[https://www.standards.govt.nz]{.underline}](https://www.standards.govt.nz)

[^7]: [https://www.ict.govt.nz/guidance-and-resources/information-management/requirements-for-cloud-computing/vendor-answer-sets/]{.underline}

[^8]: The NZ Evidence of Identity Standard defines levels of identity
    risk.

[^9]: Refer to the New Zealand Government Security Classification System
    and the New Zealand Information Security Manual for information
    about when stronger authentication techniques may be necessary.

[^10]: The process for obtaining this information is out of scope for
    this document
