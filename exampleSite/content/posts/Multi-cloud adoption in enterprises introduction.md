---
title: "Multi-cloud adoption in enterprises:An introduction"
date: 2020-08-24T16:05:58+05:30
description: "This posts talks about multi cloud adoption in enterprises"
tags: [multicloud,cloud,aws,azure,gcp,distributed computing]
---

# Introduction
Cloud computing is mainstream now and it is the major driver for digital transformation in enterprises. The number of enterprises using or planning to use multiple clouds is growing. Primarily they use private cloud due to its security advantages and public cloud for innovation. There is a lot more to it when organisations choose the type of cloud which is the focus of this article. In the beginning phase of the cloud journey enterprises started adopting hybrid cloud which is a combination of on-premise and public cloud. Now it has been extended to multi-cloud which is hybrid cloud + N, N is one or more cloud providers. For example, an enterprise started using the AWS cloud along with its on-premise data centre and later extended to use the Azure cloud as well. Some of the enterprises also use multiple public clouds without an on-prem data centre.

![GitHub Logo](/service_discovery.png)
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Service registration and discovery (source: nginx.com)

To be replaced by the image from Rightscale

As per the RightScale State of the cloud report, 2019 around 84% of the enterprises surveyed use multiple clouds.

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

### 1.Benefits
The following are the benefits organisations are considering while looking into a multi-cloud adoption strategy.
#### 1.1. Reduced Vendor Lock-in
As more and more business-critical workloads are moving to cloud, enterprises are reluctant to get into single vendor lock-in. Spreading out the work amongst cloud providers are seen as a hedging strategy against vendor lock-in.
#### 1.2 Best of Breed innovation
Different cloud providers can provide the best of breed solutions on different technologies as per the strength of innovations. So, users have choices to pick the right tool for the job.
#### 1.3 Price Negotiation
Enterprises have better negotiation power on the pricing of cloud contracts as they are not overly reliant on any single cloud provider.
#### 1.4 Geo-Presence
There might be a need to run different workloads in different regions for data sovereignty reasons. They may also want to run workloads in the nearest data centres to minimize latency.
#### 1.5 QoS and SLA consideration
Organisations can choose a cloud provider’s offering out of multiple cloud providers based on their Service Level Agreement (SLA) and Quality of Service (QoS).
#### 1.6 Workload segregation
Segregating dev/test and production workloads. Development and testing workloads can run in on-prem and the production workloads might be running in a public cloud to take advantage of latency on a local colocation region, disaster recovery, scalability, etc.
#### 1.7 Improved disaster recovery
Multi-cloud disaster recovery is another area that has proved its mettle. Here one copy of the application runs on one cloud provider while its identical copy is ready with another provider to take over if the first copy fails due to some reason. Multi-cloud disaster recovery works well as we have seen the failures of relying on a single cloud provider over the years.
This applies to organisations when unscheduled downtime would severely disrupt their business.

### 2. Disadvantages
#### 2.1. Managing costs and loss of discounts
A single cloud provider always has discounts on the bulk usage of its offerings. The discounts are often directly proportional to the usage. In a multi-cloud approach, the usage spreads across cloud providers and thins down which results in bringing down the discounts.
#### 2.2. Security
Security can never be let upon in the hands of the cloud providers. Cloud provider’s responsibility is to provide all the best tools, processes and strategies for the security of the applications, but security is always the enterprise’s responsibility. They need to incorporate Zero-trust security including least privilege access. With multiple cloud providers the scope and complexity of maintaining security increases due to an increased attack surface area for hackers.
#### 2.3. Multi-cloud management
When enterprise workloads are spread across different clouds, they need some visibility to the usage and cost control. Multi-cloud management tools are available which can help the enterprises to get insights into their cloud usage and spending patterns.

The holy grail of cloud and that of multi-cloud is cost management. As of now, organisations are struggling with cloud cost controls and cloud sprawl. Cloud sprawl is running excess workloads in the cloud without the company’s knowledge. What organisations ultimately wants to achieve with a multi-cloud approach is cloud arbitrage. We are in the early days of cloud arbitrage which is dynamically shifting workloads across clouds to leverage relative price and performance advantages. As organisations use more cloud arbitrage it will result in higher QoS levels from cloud providers as a competitive differentiator which will ultimately benefit the organisations.

## Conclusion:

>"Some relevent quote"












