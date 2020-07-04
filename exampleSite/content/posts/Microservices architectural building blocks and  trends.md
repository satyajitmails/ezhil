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

1. Service registration and discovery
Services need to find each other. They also have location transparency in a distributed architecture where services with short life cycles can reside in different containers/virtual machines/bare metals with continuously changing IP addresses. Service registration and discovery component allow services to register themselves by bootstrapping during start-up. They are found by other services and also find other services through the discovery server.

![GitHub Logo](/images/github.png)

Hashicorp Consul, Netflix Eureka, Etcd are few of the examples of service registration and discovery servers.
