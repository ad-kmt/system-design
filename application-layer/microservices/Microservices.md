## What are microservices?
**Microservices** - also known as the microservice architecture - is an architectural style that structures an application as a collection of services that are:

- Independently deployable
- Loosely coupled

Services are typically organized around business capabilities.
Each service is often owned by a single, small team.

## Context for Microservices Architecture

Imagine! you are developing a complex business-critical enterprise application. You are designing a microservice architecture that structures the application as a set of independently deployable, loosely coupled, components, a.k.a. services. Each service consists of one or more subdomains and is owned by the team (or teams) that owns the subdomains.

#### Characteristics:

**Subdomain**: A subdomain is an implementable model of a slice of business functionality, a.k.a. business capability. It consists of business logic, which consists of business entities that implement business rules, and adapters, which communicate with the outside world. The subdomains implement the application’s behavior, which consists of a set of (system) operations.

**Team Organization**: Your engineering organization is organized into small, loosely coupled, cross-functional teams. A team is responsible for one or more subdomains.

**Independently deployable**: Each service typically has its own source code repository and its own deployment pipeline, which builds, tests and deploys the service.

**Delivery Performance**: You need to deliver changes rapidly, frequently and reliably in order for your business to thrive in today’s volatile, uncertain, complex and ambiguous world. (Measure this using DORA metric)

**DevOps**: Each team delivers software using DevOps practices . In particular, it practices continuous deployment. The team delivers a stream of small, frequent changes that are tested by an automated deployment pipeline and deployed into production.

**Operations**: Some system operations will be local (implemented by a single service), while others will be distributed across multiple services. A distributed operation is implemented using either synchronously using a protocol such as HTTP/REST or asynchronously using a message broker, such as Apache Kafka.

This is what a typical microservice architecture functions.

## The Problem
- How to organize the subdomains into one or more deployable/executable components.
- The key challenge when using microservices is designing a good service architecture.
- If you get it wrong you risk creating a distributed monolith, which will slow down software delivery.

## Solution
**Assemblage** is an architecture definition process for grouping subdomains/bounded contexts into services.

Assemblage uses the **dark energy and dark matter forces** to shape the service architecture.

Dark energy forces encourage decomposition into smaller services. Dark matter forces resist decomposition.

The balance between these forces shapes the service architecture.

The **microservices pattern language** is your guide when designing an architecture: service collaboration, testing, deployment, common crosscutting concerns and more. It’s a collection of patterns that help you make decisions when designing and evolving an architecture.

Find more about these here:

**Assamblage**
https://microservices.io/post/architecture/2023/02/09/assemblage-architecture-definition-process.html

**Dark energy and dark matter forces**
https://microservices.io/post/microservices/2021/11/30/dark-matter-dark-energy.html

**Microservices pattern language**
https://microservices.io/patterns/index.html


# Resources

https://microservices.io/index.html

https://microservices.io/patterns/microservices.html