# Basics: Microservices

Unfortunately, there is no generally agreed on definition of the term
"microservice". So this brochure will first explain the basic ideas
behind microservices.

## Independent Systems Architecture (ISA) Principles

[ISA](http://isa-principles.org) (Independent Systems Architecture)
is a collection of basic principles for microservices. It is based on
experiences collected with microservices in many different projects.

## Terms

In the principles the term *must* is used for principles that have to be strictly
adhered to.  *Should* describes principles that have many
advantages, but do not necessarily have to be complied with.

The ISA principles speak of a *system*. The IT landscape of a company
consists of many systems. Every system can work with a different
architecture and can therefore be implemented based on different
principles.

## Principles

1. The system must be divided into *modules* which offer
 *interfaces*. Access to other modules is only possible through these
 interfaces.  Modules must therefore not be directly dependent on the
 deployment details of another module, for example, the data models in the
 database.

2. Modules must be *separate processes, containers or virtual
 machines* to maximize independence.

3. The system must have two clearly separated levels of
architectural decisions:
   * The *macro architecture* includes decisions that affect all
   modules.
   * The *micro architecture* comprises those decisions that can be made
  differently for each module.

     All other principles from point 4 onwards are part of the
     macro architecture.

4. The choice of *integration options* must be limited and
standardized for the system. The integration can use synchronous or
asynchronous communication and / or it can take place at the frontend
level.

5. *Communication* must be limited to a set protocols like REST or
messaging implementations like Kafka. Also metadata, e.g. for
authentication, must be standardized.

6. Each module must have its *own independent continuous delivery
pipeline*. Tests are part of the continuous delivery pipeline.
Therefore, the tests of the modules must be independent.

7. *Operations* should be standardized. This includes configuration,
deployment, log analysis, tracing, monitoring and alarms. There may be
exceptions to the standard when a module has very specific
requirements.

8. *Standards* for operation, integration or communication should be
defined on the interface level. The protocol can be standardized as
REST, and data structures for the communication can be standardized.
But each module should be free to use a different REST library.

9. Modules must be *resilient*. They must not fail if other modules
are not available or communication problems occur. It must be possible
to stop a module and start it in a different environment (servers,
networks, configuration, etc.)  without losing data or other state.

## Reasons

ISA shows that microservices are a way of modularization (principle
1). So ideas like
[information hiding](https://en.wikipedia.org/wiki/Information_hiding)
or high
[cohesion](https://en.wikipedia.org/wiki/Cohesion_%28computer_science%29)
/ low coupling are also applicable to microservices. The difference to
traditional modules is the implementation as a separate container
(principle 2). This allows more freedom in the technical
implementation of the modules. However, the modules are still part of
a system, so in the end the freedom must be limited accordingly (principle 3).
Consequently, integration (principle 4) and communication (principle
5) have to be standardized because otherwise there will be no system but rather
separate isolated islands.

Independent deployment is an advantage of microservices and can only
be ensured if each microservice has its own continuous delivery
pipeline (principle 6).

Standardization (principle 7) facilitates operations, especially in the face of
a large number of microservices. But the standards must not restrict
the freedom of technology and therefore should only define the
interface (principle 8). A microservices system will maybe not use
many different technologies from the beginning, but you should keep
the opportunity open to be well prepared for further
development. In the long run, new technologies will appear on the
market, and it is advantageous if the system can use them.

A microservices system is a distributed system. That increases the
likelihood of failure of servers, the network or a
microservice. Therefore, resilience (principle 9) is essential. Also,
resilience allows microservices to be moved to a different
environment. That is an advantage if the system runs in a cluster.

Thus, the ISA principles provide a good basis for a
microservices system.

## Self-contained Systems

The ISA principles define important principles for microservices, but
they do not cover all decisions and features. For example,
organization, domain architecture and the question whether microservices should
contain a UI or not are not discussed.

Self-contained systems (SCSs) are an approach to microservices that
has already proven itself in many projects. All essential
information on SCSs can be found on the website
<http://scs-architecture.org/>. Here is an overview of the
most important characteristics:

- Each SCS is an *autonomous web application*. The code for 
  the web interface is included in the SCS. Thus, a user can use
  one SCS without relying on other SCSs.

- SCSs are not allowed to *share a UI*. After all, an SCS should be
  used via its own UI.

- An SCS can have an *optional API*. But the API is not strictly
  necessary, since the SCS already has a web interface for the
  user. For mobile clients or other SCSs, access via an API maybe
  useful.

- The SCS contains *data and logic*. A new feature typically requires
  changes to UI, logic, and data. All these changes can be done in
  a single SCS.

- For one SCS exactly *one team* is responsible. However, a team can
  be in charge of more than one SCS.

- To avoid tight coupling, SCSs should *not share business
code*. Only the sharing of common technical code is allowed. As a rough rule: Only
code that would be published as open source might be shared between
SCS.

- To further decouple the SCS, the SCS *should not share
infrastructure*, for example, no shared database should be used. For
cost reasons, compromises can be made.

- The *communication* between SCSs is *prioritized*:
  * Frontend integration has the highest priority.
  * This is followed by asynchronous communication
  * and finally, synchronous communication is also possible.

    The focus is on decoupling and resilience. The
    higher-priority types of communication help to achieve
    these goals.

As mentioned, the SCS idea has already proven itself in many projects. The
[links on the website](http://scs-architecture.org/links.html) give
an impression of some of these projects. The approach is only usable for web
applications, since every SCS has a web interface. However, the separation
into systems that implement part of the business logic and are developed by one
team, is also sensible for other types of systems.

## Conclusion & Outlook

ISA defines the principles all microservices systems should comply with while SCS
defines best practices that have been used successfully in many projects.

The following chapters describe technical recipes for the communication
between microservices in the order of priorities suggested by SCS: frontend
integration, asynchronous communication and finally, synchronous
communication.
