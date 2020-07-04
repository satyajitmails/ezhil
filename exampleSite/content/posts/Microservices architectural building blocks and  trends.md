---
title: "Microservices architectural building blocks and  trends"
date: 2020-06-30T20:46:58+05:30
description: "Microservices architectural building blocks and  trends"
tags: [Primer, todo]
---

In the digital age technology based on sound software architecture is a primary foundation for a successful business. The most important value driver of software architecture is the ability to experiment with end users by introducing a new business idea into production quickly. 

Technology itself is not a silver bullet for problem-solving, but it provides different approaches for problem-solving. Microservices architecture is one such approach in technology for server-side service design. It has gained popularity due to successful adoption by large internet consumer companies like Amazon, Facebook, Netflix, Twitter, etc. by helping them solve certain problems. They operate on a massive scale and are consistently on the top of their game. A laser-sharp focus on innovation is supported by engineering practices like a short release cycle of features through automation of build-test-deploy pipeline. A/B testing, gamification, and other techniques are used to get quick customer feedback and pivot the feature releases accordingly. Microservices architecture acts as an enabler for the above and also helps in areas like on-demand scaling, effective resource allocation, an independent stream of development and deployment, choice of polyglot runtime environments, etc.
 
any excellent articles are detailing the promises of microservices architecture. This article is an attempt to provide a technical overview of core architectural building blocks for successful microservices architecture and the latest trends in that space. It is based on author’s and his industry peers' experience of developing microservices-based systems for more than the last half of the decade in both cloud native and cloud agnostic way. There is no single way or standard to develop a successful microservices architecture and every team’s mileage varies in terms of approach and execution. Microservices design patterns, storage, network design are the other critical aspects left out of this article due to lack of space.

Microservices architecture is a distributed server-side architecture based on loosely coupled services that are designed, developed, packaged, build, tested, deployed and scaled independently. The twelve-factor app is a methodology which nicely complements and helps to leverage the value of microservices architecture.

### 1. Service registration and discovery
   
Services need to find each other. They also have location transparency in a distributed architecture where services with short life cycles can reside in different containers/virtual machines/bare metals with continuously changing IP addresses. Service registration and discovery component allow services to register themselves by bootstrapping during start-up. They are found by other services and also find other services through the discovery server.

![GitHub Logo](/service_discovery.png)
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Service registration and discovery (source: nginx.com)

Hashicorp Consul, Netflix Eureka, Etcd are few of the examples of service registration and discovery servers.

### 2. Service to service communication

A service communicates with other services for the execution of a functionality. There are multiple ways in which service to service communication can happen.

![GitHub Logo](/Sync_vs_Async_messaging_Microsoft.png)
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Synchronous vs. asynchronous messaging (source: microsoft.com)

#### 2.1 Asynchronous mode using a message queue or polling
It has two types of approach; one is push based using a message queue and another is poll based using HTTP.A service communicating to other services through message queue keeps the services decoupled, keeps them asynchronous, can scale out as per load, provides message resiliency, etc. The downside to this approach is an extra message queue component to maintain. RabbitMQ, Kafka is leading open source message brokers and there are managed services options for message queues from public cloud providers like AWS, Azure, GCP, etc. 
A poll-based approach has the downside of wasting compute cycles while it is waiting for response.
#### 2.2. Synchronous mode of direct service to service communication
It is the simplest approach as it doesn't need any additional components. The downside is the heavy coupling and cascading effect of change between the services.
#### 2.3. Through a proxy or API gateway
 This approach is used when we want to expose services in a centralized and controlled manner. Services that are opened to the outside world to be used by external clients also use this pattern. The downside is another component to maintain. Kong, Zuul and cloud-based options like AWS API gateway, Google cloud apigee, Azure API management are used here.

 ![GitHub Logo](/custom_api_gateway_microsoft.png)
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;API gateway(source: Microsoft.com))

No matter which style of the communication we choose, we still need to deal with the resilience issues of distributed systems. We can use resilience handling techniques like request retries with exponential backoff, failure handling, circuit breaking, back pressure, bulkhead, isolation of faults to improve the resilience of the system.

There are components and libraries available which provide these features like spring cloud Netflix, Alibaba, etc. Recently there is a rise in using service mesh components for the same due to their non-intrusive approach of residing as a sidecar along with the microservices component versus being embedded inside the service codebase like the above-mentioned framework and libraries. Leading players in this space are Istio, Linkerd, Envoy.

### 3. Service configuration
Each service may use some configuration data like file paths, date and time formats, environment-specific values, etc. As the number of services increases; creating, storing, updating, deleting the configurations becomes nontrivial and time-consuming. A configuration server component helps in storing and managing these configurations.
    
Hashicorp Consul, Spring configuration server are few of the examples of configuration servers. We can also create our configuration servers by using a database.

### 4. Secrets management
Each service uses some infrastructure and application-level highly sensitive data like credentials, connection strings, API private keys, etc. which are not suitable to store in a version control system like git or a database. A secret manager component helps to store, managing those secrets. In some cases, it also helps in the creation of the secrets.

![GitHub Logo](/secrets_management.png)
(Lambda based microservice with secret manager provided DB credentials (source: aws.amazon.com)

Hashicorp Vault is a great open-source option for a secret manager.AWS Secrets Manager, AWS Parameter Store, Azure Key Vault, GCP Cloud KMS are software-based options for a secret manager. Hardware security modules (HSM) like GCP Cloud HSM, Azure Key Vault and AWS Cloud HSM is provided by cloud providers to strengthen secret management. 

### 5. Observability
Logs, metrics, traces are called the golden triad of service observability
which helps us to understand microservice execution behavior from end to end. An effective way to observe microservices' behavior is to also understand the whole systems' behavior, where we monitor the infrastructure and other components of the whole system along with the microservices. Application/cloud performance monitoring products like Dynatrace, Datadog, Newrelic, AppDynamics can be augmented with the above approaches to collect, monitor and analyze an end to end microservices system.

![GitHub Logo](/amazon_graph.jpeg)
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;Call graphs of microservices in several organizations




