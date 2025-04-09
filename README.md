
# Event-Driven Architecture in .NET

## Table of Contents
1. [What is Event-Driven Architecture?](#what-is-event-driven-architecture)
2. [When and Why Use Event-Driven Architecture](#when-and-why-use-event-driven-architecture)
3. [Advantages and Disadvantages](#advantages-and-disadvantages)
4. [Use Cases](#use-cases)
    - [To Decouple Components](#to-decouple-components)
    - [To Perform Async Tasks](#to-perform-async-tasks)
    - [To Keep Track of State Changes (Audit Log)](#to-keep-track-of-state-changes-audit-log)
5. [Listeners vs Subscribers](#listeners-vs-subscribers)
6. [Event Patterns](#event-patterns)
    - [Event Notification](#event-notification)
    - [Event-Carried State Transfer](#event-carried-state-transfer)
    - [Event Sourcing](#event-sourcing)
7. [Advanced Concepts](#advanced-concepts)
    - [Transaction Log](#transaction-log)
    - [Deletions](#deletions)
    - [Snapshots](#snapshots)
    - [Projections](#projections)
    - [External Updates](#external-updates)
    - [External Queries](#external-queries)
    - [Code Changes](#code-changes)
8. [Conclusion](#conclusion)
9. [Resources](#resources)

## What is Event-Driven Architecture?

Event-Driven Architecture (EDA) is a software design pattern where components communicate through the generation and consumption of events. These events signal that something has happened in the system and trigger asynchronous communication between decoupled services.

## When and Why Use Event-Driven Architecture

- When decoupling of services is essential.
- For systems requiring high scalability and real-time data flow.
- When tasks can be performed asynchronously.
- To ensure an immutable audit trail via event sourcing.

## Advantages and Disadvantages

### Advantages
- High scalability and resilience.
- Loose coupling between services.
- Natural fit for microservices and distributed systems.
- Enables real-time processing.

### Disadvantages
- Higher complexity in debugging and tracing.
- Requires robust monitoring and infrastructure.
- Harder to test and simulate.
- Risk of spaghetti code if overused.

## Use Cases

### To Decouple Components
Instead of direct service calls, components emit events. Other services listen and react to those events, promoting modularity and autonomy.

### To Perform Async Tasks
Offload long-running tasks (e.g., sending emails) into background workers via events and queues (e.g., Azure Service Bus, RabbitMQ).

### To Keep Track of State Changes (Audit Log)
Log all changes as events rather than mutating state. Useful in finance, healthcare, and systems with regulatory compliance.

## Listeners vs Subscribers

- **Listeners**: React to a single event with focused logic.
- **Subscribers**: React to multiple events with logic grouped by concern (e.g., transactional state).

## Event Patterns

### Event Notification

**Minimal Data**: Notify other components something happened.

#### Advantages
- Decoupled interaction.
- Asynchronous processing.

#### Disadvantages
- Lack of context can limit usefulness.
- Still needs another data query.

### Event-Carried State Transfer

**Full Entity Data**: Events carry full updated data.

#### Advantages
- Improves resilience and performance.
- Local reads without dependency.

#### Disadvantages
- Potential data duplication.
- Increased message size.

### Event Sourcing

Store only state changes as events in an event stream.

#### Transaction Log
Every state change is recorded as an event.

#### Deletions
Handled through reversal events.

#### Snapshots
Periodically save the state to speed up loading.

#### Projections
Compute and store materialized views of the current or historical state.

### Pros and Cons

**Pros**:
- Complete history, traceability.
- Retroactive analysis.
- Debugging and business analytics.

**Cons**:
- Complex code evolution.
- External systems interaction risk.
- Storage overhead.

## External Updates
Triggering real services from replayed events must be avoided.

## External Queries
Events dependent on remote systems must store query responses locally to preserve determinism.

## Code Changes
Business logic changes require strategies like versioned event handlers or strategy patterns.

## Conclusion

Event-Driven Architecture in .NET allows building scalable, decoupled, and resilient systems. While powerful, it introduces complexity requiring discipline and strong architectural practices.

## Resources

### GitHub Repositories
- https://github.com/dotnet-architecture/eShopOnContainers
- https://github.com/BrighterCommand/Brighter
- https://github.com/ThreeMammals/Ocelot

### Blogs & Articles
- [Microsoft EDA Guide](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven)
- [Martin Fowler on EDA](https://martinfowler.com/articles/201701-event-driven.html)
- [Herberto Graça’s Blog](https://www.herbertograca.com)

### Tutorials
- [Pluralsight - Event-Driven Architecture in .NET](https://www.pluralsight.com/)
- [Dev.to Series on EDA](https://dev.to/tags/eventdriven)
- [Event Store Docs](https://eventstore.com/docs/)

