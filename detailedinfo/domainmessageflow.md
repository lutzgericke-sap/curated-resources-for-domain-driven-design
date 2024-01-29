# Domain Message Flow

![Domain Message Flow](./images/Restaurant%20DDD%20Kata%20Example_DMF.png)

## What is Domain Message Flow?

One of the key aspects of designing systems that are loosely-coupled, meaning that they have minimal dependencies and interactions with each other, is to define clear and consistent boundaries and interfaces for each sub-system. These sub-systems are called bounded contexts, and they represent a specific part of the domain or business logic that the system is trying to model. Bounded contexts can be realized in different ways, such as microservices, which are small and independent services that communicate over a network, or modules, which are components within a larger and more monolithic system.

To understand how the bounded contexts interact with each other and with external actors and systems, it is useful to create a Domain Message Flow Diagram. This is a simple graphical representation that shows the flow of messages, such as commands, events, and queries, that are exchanged between the different elements of the system, for various scenarios or use cases. The scenarios should be chosen to cover the most important and common functionalities of the system, and to illustrate the end-to-end flow of messages from the initiation to the completion of a task. Ideally, the scenarios should include the happy path, which is the optimal and expected way a process shouldrun, as well as some alternative or exceptional paths, which are the possible deviations or errors that might occur.

The Domain Message Flow Diagram can help to identify and evaluate some of the design choices and trade-offs that are involved in creating loosely-coupled systems. For example, it can help to detect if there are any centralized services that act as a single point of failure, meaning that if they fail or become unavailable, the whole system or a large part of it will stop working. It can also help to measure the chattiness of the system, which is the amount and frequency of messages that are sent between the services. A high level of chattiness can indicate that the bounded contexts are not well-defined or aligned with the domain, and that they might need to be reevaluated or restructured. Additionally, it can help to identify which services are more critical or sensitive, and might need to be more robust, reliable, and resilient in order to handle failures or disruptions gracefully.

An important aspect of creating a Domain Message Flow Diagram is to reuse the events and commands that were previously modeled in the Event Storming, which is another technique for exploring and designing the domain. The events and commands represent the actions and reactions that occur in the system, and they should be consistent and coherent across the different diagrams and models. The Domain Message Flow Diagram should also consider which events or commands might be sent from or to an external system or an actor, such as a user, a device, or another application, and how they affect the flow of messages within the system.

## How to use it?

The first step in designing your software architecture is to identify the different bounded contexts that make up your system. A bounded context is a logical boundary that defines a specific domain or functionality within your system. By identifying the bounded contexts, you can separate the concerns and responsibilities of each part of your system and avoid unnecessary coupling and complexity.

Once you have identified the bounded contexts, you can start designing the message flows between them. A message flow is a sequence of messages that are exchanged between different bounded contexts to achieve a certain goal or scenario. To design the message flows, you need to follow these steps:

- First, create a list of the scenarios that you want to model. A scenario is a description of a user or system action and the expected outcome. For example, a scenario could be "A customer places an order and receives a confirmation email".
- Next, for each scenario, create a diagram that shows the message flow. A diagram is a visual representation of the message flow using symbols and lines. To create a diagram, you need to follow this process:
  1. Start with an actor, a context, or a system that initiates the message flow. An actor is a user or an external system that interacts with your system. A context is a bounded context that belongs to your system. A system is a collection of bounded contexts that form your system. For example, you could start with a customer actor, an reservation context, or a restaurant website.
  2. Create the message that they want to send. A message is a unit of information that is transmitted between different bounded contexts. A message can be a command, an event, or a query. A command is a message that tells another context to do something. An event is a message that informs another context about something that has happened. A query is a message that asks another context for some information. For example, you could create a "Order Food" command, an "Table Reserved" event, or a get "Today's Reservations" query.
  3. Add the recipient of the message and a line connecting the sender and the receiver. The recipient is another actor, context, or system that receives the message. The line is a symbol that shows the direction and the type of the message. A solid line indicates a synchronous message, which means that the sender waits for a response from the receiver. A dashed line indicates an asynchronous message, which means that the sender does not wait for a response from the receiver. For example, you could add an order context as the recipient of the place order command and a solid line between the customer actor and the order context.
  4. Place the message close to the line. The message should be written near the line that connects the sender and the receiver. The message should also be aligned with the direction of the line. For example, you could place the place order command above the solid line from the customer actor to the order context.
  5. Repeat steps **i - iv** until your scenario is complete. You should continue adding messages, recipients, and lines until you have covered all the steps and outcomes of your scenario. For example, you could add an order placed event from the order context to the customer actor, a send confirmation email command from the order context to an email context, and a confirmation email sent event from the email context to the order context.
- The message should contain 3 elements:
  - The name of the message. The name of the message should be a concise and descriptive phrase that summarizes the purpose and the content of the message. The name of the message should also follow a consistent naming convention. For example, you could use verbs for commands, past tense verbs for events, and nouns for queries. For example, place order, order placed, and get order status are good names for messages.
  - The order in which the message occurs in the flow being modelled. The order is the position and the sequence of the message in the message flow. The order indicates when and how the message is sent and received. The order can be expressed using numbers, letters, or symbols. For example, you could use numbers to indicate the chronological order of the messages, such as 1, 2, 3, etc. For example, the place order command could be the first message in the message flow, so it could have the order 1.

After you have created the diagrams for each scenario, you can review them and look for any gaps, inconsistencies, or errors. You can also compare them with the requirements and the expectations of the stakeholders. You can use the following questions to guide your review:

- Are the bounded contexts clearly defined and named?
- Are the messages clear, consistent, and complete?
- Are the message types appropriate for the purpose and the direction of the message?
- Are the message data minimal, sufficient, and structured?
- Are the message orders correct and logical?
- Are the message flows complete and coherent?
- Do the message flows cover all the scenarios and outcomes?
- Do the message flows meet the requirements and the expectations of the stakeholders?

If you find any issues or areas for improvement, you can revise your diagrams and update your message flows accordingly. You can also get feedback from other developers, architects, or domain experts to validate and refine your message flows. By doing this, you can ensure that your message flows are accurate, consistent, and comprehensive. With this iterative approach you can also verify if your EventStorming has been valid. You can take the newly gained insights to iterate on your EventStorming.

## Anti-Pattern

An anti-pattern is a common but ineffective or harmful solution to a problem, that has more negative consequences than positive ones. It is the opposite of a pattern, which is a good and proven solution to a problem. Anti-patterns can be found in various domains, such as software engineering, project management, and business processes. The following are anti-pattern we have identified and observed in several workshops. They are often indicators that the domain is not broken down into independent bounded contexts. By not addressing them you might inflict unwanted and unneeded dependencies into your application design.

### Synchronous Dependencies / Communication

The synchronous communication pattern is a one way of designing interactions between bounded contexts, which are sub-systems that represent a specific part of the domain. However, this pattern can also introduce some challenges and risks for the system, depending on the level and the nature of the communication. Synchronous communication pattern means that the sender and the receiver of a message must be online and ready at the same time, and that the sender must wait for a reply before continuing with other tasks. This can have different implications for the system, such as:

At the **process level**, synchronous communication can indicate that the bounded contexts are not well-defined or aligned with the domain. They might have too many dependencies or responsibilities, which can lead to tight coupling and low cohesion. This can make the system more difficult to maintain, test, and evolve. Moreover, synchronous communication can affect the reliability and the resilience of the system, as each message can be vulnerable to errors, failures, or disruptions in the communication channel or the message processing, which can cause the system to fail or behave unpredictably. This can also impact the user experience, as the clients can observe the errors or the delays in the system. Therefore, at the process level, synchronous communication should be avoided or replaced by a better solution, such as asynchronous communication, which is more suitable for loosely-coupled systems.

At the **technical level**, synchronous communication can increase the resource consumption and the complexity of the system, as each message can require a lot of data, processing, and coordination, especially when there are many requests happening simultaneously or when the messages are large or complex. This can reduce the performance and the scalability of the system, as each message can block the execution of other tasks or processes until a response is received, which can cause delays, bottlenecks, and congestion in the system. However, synchronous communication can also offer some benefits, such as simplicity, consistency, and immediacy, which can be useful for some scenarios or requirements. Therefore, at the technical level, synchronous communication can be used with caution and with appropriate mechanisms, such as HTTP feeds or transactional outbox, which can enable asynchronous design with synchronous means.
In conclusion, the synchronous communication pattern is not inherently bad, but it can have some drawbacks and limitations for the system, depending on how it is applied and what it is used for. Thus, it is important to differentiate between synchronous requests at a technical and at a process level, and to choose the best communication pattern for each situation and context.

### Star Fish Pattern

In software engineering, a **single point of failure** (SPOF) is a part of a system that, if it fails or becomes unavailable, causes the entire system or a large part of it to stop functioning. A single point of failure can compromise the **availability** and **reliability** of the system, which are two important attributes of software quality.

One way to identify a single point of failure in a system is to use the **star fish pattern**. The star fish pattern is a graphical representation of a system where a centralized component or module is connected to many other components or modules, forming a shape similar to a starfish. The centralized component or module acts as the **hub** or the **coordinator** of the system, while the other components or modules act as the **spokes** or the **workers** of the system.

The star fish pattern can be useful for some scenarios, such as when the system needs to have a consistent and centralized control or coordination mechanism, or when the system needs to have a simple and clear structure. However, the star fish pattern also has many drawbacks and risks, such as:

- **Reduced availability and reliability**: If the hub or the coordinator of the system fails or becomes unavailable, the entire system or a large part of it will stop working. This can compromise the business continuity, productivity, and security of the system³. For example, if a database server is the hub of a system, and it crashes or goes offline, the system will not be able to access or store any data, rendering the system useless or unreliable.
- **Increased complexity and risk**: If the hub or the coordinator of the system is responsible for managing or coordinating many other components or processes, it can increase the complexity and the risk of the system. This can make the system more difficult to maintain, test, and modify, and more prone to errors and failures⁵. For example, if a web server is the hub of a system, and it handles many requests from different clients, it can become overloaded or overwhelmed, leading to performance degradation or system failure.
- **Decreased scalability and performance**: If the hub or the coordinator of the system is a bottleneck or a constraint for the system, it can decrease the scalability and the performance of the system. This can affect the efficiency, responsiveness, and quality of the system⁵. For example, if a message broker is the hub of a system, and it has a limited capacity or throughput, it can limit the scalability and the performance of the system, preventing it from handling more load or traffic.
- **Decreased flexibility and adaptability**: If the hub or the coordinator of the system imposes strict requirements or limitations on the system, it can decrease the flexibility and the adaptability of the system. This can prevent the system from evolving or changing according to the needs of the domain. For example, if a configuration server is the hub of a system, and it has a rigid or inflexible configuration schema, it can restrict the flexibility and the adaptability of the system, hindering its innovation or improvement.

Therefore, the star fish pattern is a synonym of a single point of failure, and it should be avoided or mitigated whenever possible. Some possible ways to avoid or mitigate the star fish pattern are:

- **Distributing or decentralizing the system**: Instead of having a single hub or coordinator, the system can have multiple hubs or coordinators, or no hubs or coordinators at all. This can increase the availability and reliability of the system, as well as the scalability and performance of the system, by eliminating or reducing the single point of failure. For example, instead of having a single database server, the system can have multiple database servers, or use a peer-to-peer or a distributed database system.
- **Isolating or modularizing the system**: Instead of having a single system or a monolithic system, the system can be divided into smaller and independent systems or modules, each with its own hub or coordinator, or no hub or coordinator at all. This can increase the complexity and risk of the system, as well as the flexibility and adaptability of the system, by separating or encapsulating the different concerns or functionalities of the system. For example, instead of having a single web server, the system can have multiple web servers, or use a microservice or a serverless architecture.

## Resources

1. **[Anti-pattern - Wikipedia](https://en.wikipedia.org/wiki/Anti-pattern):** Wikipedia's page on anti-patterns, providing an overview of common design patterns that may lead to counterproductive outcomes.

2. **[What Is an Anti-pattern? | Baeldung on Computer Science](https://www.baeldung.com/cs/anti-patterns):** Baeldung's article explaining anti-patterns in computer science, highlighting common pitfalls and mistakes in software design.

3. **[Virtual Domain-Driven Design - A community of practise](https://virtualddd.com/learning-ddd/ddd-crew-domain-message-flow-modelling/):** A resource from Virtual Domain-Driven Design focusing on domain message flow modeling within the DDD community.

4. **[Best Practice - An Introduction To Domain-Driven Design](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design):** Microsoft's article introducing best practices in Domain-Driven Design (DDD), emphasizing key concepts and approaches.

5. **[Domain Message Flow Modelling - GitHub](https://github.com/ddd-crew/domain-message-flow-modelling):** GitHub repository for domain message flow modeling, providing practical resources and examples.

6. **[Synchronous vs. Asynchronous Communication | The TechSmith Blog](https://www.techsmith.com/blog/synchronous-vs-asynchronous-communication/):** The TechSmith Blog's comparison of synchronous and asynchronous communication, exploring the advantages and disadvantages of each approach.

7. **[Synchronous vs Asynchronous Communication in Distributed Systems](https://gheorghina.github.io/microservices/reliability/sync/async/2023/02/09/sync-async-communication.html):** An article discussing synchronous and asynchronous communication in distributed systems, focusing on reliability aspects.

8. **[Practical Microservices Development Patterns: Sync vs. Async](https://dzone.com/articles/practical-microservices-development-patterns-sync):** DZone's article on practical microservices development patterns, particularly comparing synchronous and asynchronous communication.

9. **[Synchronous Communication: Pros, Cons, Trends and Tools | Chanty](https://www.chanty.com/blog/synchronous-communication/):** Chanty's exploration of synchronous communication, outlining its pros, cons, current trends, and relevant tools.

10. **[Centralized, Decentralized and Distributed Systems - GeeksforGeeks](https://www.geeksforgeeks.org/comparison-centralized-decentralized-and-distributed-systems/):** GeeksforGeeks' comparison of centralized, decentralized, and distributed systems, providing insights into their characteristics.

11. **[Single point of failure - Wikipedia](https://en.wikipedia.org/wiki/Single_point_of_failure):** Wikipedia's page on single points of failure, explaining the concept and its implications in system design.

12. **[What is a Single Point of Failure? Definition & FAQs - Avi Networks](https://avinetworks.com/glossary/single-point-of-failure/):** Avi Networks' definition and FAQs on single points of failure, offering insights into their nature and how to address them.

13. **[Centralized Points of Failure | weteachblockchain.org](https://weteachblockchain.org/courses/blockchain-security/3/centralized-points-of-failure/):** A resource discussing centralized points of failure in the context of blockchain security.

14. **[How to avoid a Single Point of Failure (SPOF) in Distributed Systems?](https://ipwithease.com/how-to-avoid-spof-in-distributed-systems/):** Practical tips on avoiding single points of failure in distributed systems, emphasizing resilience and redundancy.