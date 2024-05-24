# Layered Architecture in System Design

## What is Layered Architecture?

The layered architecture style is one of the most common architectural styles in software development. The idea behind Layered Architecture is that modules or components with similar functionalities are organized into horizontal layers. Each layer performs a specific role within the application, promoting the concept of separation of concerns.

### Key Concepts
- **Layers**: Each layer is a collection of modules that provide a consistent set of services.
- **Separation of Concerns**: Layers abstract the view of the system as a whole while providing enough detail to understand the roles and responsibilities of individual layers and the relationship between them.

### Common Layers
- **Presentation Layer**: Contains classes responsible for presenting the UI/visualization to the end-user and handling browser communication logic. This is the only layer that customers interact with.
- **Business/Logic Layer**: Contains all the logic required by the application to meet its functional requirements, including data aggregation, computation, and query requests.
- **Data/Physical + Persistence Layer**: Where retrievable information is stored, consisting of both logical and physical aspects. The logical schema specifies the conceptual model of data, while the physical schema implements this model into a physical database platform.

![](https://www.oreilly.com/api/v2/epubs/9781491971437/files/assets/sapr_0101.png)

![](https://herbertograca.com/wp-content/uploads/2017/07/2010s-layered-architecture.png?w=1100)

## How Does Layered Architecture Work?

### Communication and Constraints
- **Connectors**: The connector between each layer can be a function call, a query request, a data object, or any connector that conveys a request or information.
- **Topological Constraints**: Connectors only interact with two layers, usually with no skipping of layers allowed. Communication is usually between one user and one interface/system. Data flows both ways (user to system, and back).

### Open vs. Closed Layers
- **Closed Layers**: Each layer is reliant on one or more levels below it but independent of the ones above it. Requests must go through each closed layer, promoting isolation and making the code easier to alter, develop, and comprehend.
- **Open Layers**: Layers can bypass other layers (layer bridging), increasing flexibility but also complexity. It can prevent excessive traffic on individual levels but requires careful management to avoid maintainability issues.

## Why Use Layered Architecture?

### Advantages
- **Simplifies Structure**: Divides the application into distinct layers, each with a specific function, reducing complexity.
- **Hides Complexity**: Allows focus on more complex tasks or issues by isolating complexity.
- **Reduces Dependencies**: Minimizes dependencies between layers, simplifying the application’s structure.
- **Improves Testability**: Partitioning the application into layers and leveraging interfaces for inter-layer interaction allows isolation of layers for testing.
- **Increases Reusability**: Layers can be reused across multiple applications.
- **Enhances Scalability**: More hardware can be added to each layer.
- **Boosts Availability**: Multiple computers per tier increase uptime and availability.
- **Improves Security**: Firewalls can be installed between layers.

### Disadvantages
- **Interdependence**: Changes in one layer can require changes in multiple layers, reducing flexibility.
- **Increased Code Complexity**: More code is required to provide interfaces and communication logic between layers.
- **Potential for Inefficiencies**: Requests going through multiple layers can result in inefficiencies.
- **Performance and Cost**: Deploying multiple layers on different tiers requires additional performance and monetary costs.

## Applicable Problems
- Software that requires separate layers of processing and security.
- Data-driven software, CRUD applications.

## Resilience to Change
- **Separation of Concerns**: Each layer has a specific function, making updating individual layers easier and allowing teams to separate workloads.

## Negative Behaviors
- **Tightly Coupled Components**: Layered software can result in tightly coupled components and monolithic applications.
- **Security Issues**: Bypassing layers can compromise security. The Business Layer typically acts as an integrity check.
- **Complicated Communication**: If not properly designed and managed, communication between layers can become complicated.

## Supported Non-Functional Properties (NFPs)
- **Easy to Implement/Test**: Each layer has a specific function, making it easy to implement and test.
- **Flexibility**: Can be abstracted into layers, leading to many practical applications.
- **Security**: Security can be implemented at every layer.

## Inhibited Non-Functional Properties (NFPs)
- **Low Scalability**: Highly coupled software groups make it hard to scale and update.
- **Low Performance**: Data must travel through every layer, slowing down performance.


## Topics for Deeper Understanding
- Detailed design patterns for layered architecture
- Best practices for implementing layered architecture
- Case studies on layered architecture in real-world applications
