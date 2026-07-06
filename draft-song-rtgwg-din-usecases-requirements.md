---
stand_alone: true
ipr: trust200902
title: "Distributed Inference Network (DIN) Problem Statement, Use Cases, and Requirements"
abbrev: "DIN: Problem, Use Cases, Requirements"
lang: en
category: info

docname: draft-song-rtgwg-din-usecases-requirements-02
submissiontype: IETF
number:
date: 2026
consensus: true
v: 3
workgroup: rtgwg
keyword:
 - DIN
 - AI Inference

author:
 - name: Song Jian
   organization: China Mobile
   email: songjianyjy@chinamobile.com
   country: China
 - name: Weiqiang Cheng
   org: China Mobile
   email: chengweiqiang@chinamobile.com
   country: China

normative:  # list the referenced RFC's   RFC9800

informative:

--- abstract

This document describes the problem statement, use cases, and requirements for a "Distributed Inference Network" (DIN) in the era of pervasive AI. As AI inference services become widely deployed and accessed by billions of users, applications and devices, traditional centralized cloud-based inference architectures face challenges in scalability, latency, security, and efficiency. DIN aims to address these challenges by leveraging distributed edge-cloud collaboration, intelligent scheduling, and enhanced network security to support low-latency, high-concurrency, and secure AI inference services.


--- middle

# Introduction

AI inference is rapidly evolving into a fundamental service accessed by billions of users, applications, IoT devices, and AI agents. 

The rapid advancement and widespread adoption of large AI models are introducing significant changes to internet usage patterns and service requirements. These changes present new challenges that existing network need to address to effectively support the growing demands of AI inference services.

First, internet usage patterns are shifting from primarily content access to increasingly include AI model access. 

Users and applications are interacting more frequently with AI models, generating distinct traffic patterns that differ from traditional web browsing or streaming. This shift requires networks to better support model inference as an important service type alongside conventional content delivery.

Second, the interaction modalities are diversifying from simple human-to-model conversations to include complex multi-modal interactions. 

As AI inference costs decrease dramatically, applications, IoT devices, and autonomous systems are increasingly integrating AI capabilities through API calls and embedded model access. This expansion creates unprecedented demands for high-concurrency processing and predictable low-latency responses, as these systems often require real-time inference for critical functions including autonomous operations, industrial control, and interactive services.

Third, AI inference workloads introduce distinct traffic characteristics that impact network design. 

Both north-south traffic between users and AI services, and east-west traffic among distributed AI components, are growing significantly. Moreover, the nature of AI inference communication, often organized around token generation and processing, introduces new considerations for traffic management, quality of service measurement, and resource optimization that complement traditional bit-oriented network metrics.

In addition, AI agents are autonomous, goal-driven entities that can perceive their environment, make decisions, and execute actions. AI agents communicate with each other and with models/tools, requiring not only inference but also coordination, state management, and dynamic discovery. This further stresses the network infrastructure and is considered within the scope of this document.

These developments collectively challenge current network infrastructures to adapt to the unique characteristics of AI inference workloads. Centralized approaches face limitations in supporting the distributed, latency-sensitive, and concurrent nature of modern AI services, particularly in scenarios requiring real-time performance, data privacy, and reliable service delivery.

This document outlines the problem statement, use cases, and functional requirements for a Distributed Inference Network (DIN) to enable scalable, efficient, and secure AI inference services that can address these emerging challenges.


# Conventions and Definitions
DIN:
: Distributed Inference Network

{::boilerplate bcp14-tagged}

# Problem Statement

The proliferation of AI inference services has exposed fundamental limitations in traditional centralized AI inference architectures. 

Centralized inference deployments face severe scalability challenges when handling concurrent requests from the rapidly expanding ecosystem of users, applications, IoT devices, and AI agents. Service providers have experienced recurrent outages and performance degradation during peak loads, with concurrent inference requests projected to grow from millions to billions. The fundamental constraint of concentrating computational resources in limited geographical locations creates inherent bottlenecks that lead to service disruptions and degraded user experience under massive concurrent access.

While human-to-model conversations may tolerate moderate network latency, the emergence of diverse interaction patterns including application-to-model, device-to-model, and machine-to-model communications imposes stringent low-latency requirements that centralized architectures cannot meet. 

Applications including industrial robots, autonomous systems, and real-time control platforms require low-latency responses that are fundamentally constrained by the unavoidable geographical dispersion between end devices and centralized inference facilities. This architectural limitation creates critical barriers for delay-sensitive operations across manufacturing, healthcare, transportation, and other domains where millisecond to sub-millisecond-level response times are essential.

Enterprise and industrial AI inference scenarios present unique security and compliance requirements. Centralized architectures introduce risks such as single points of failure (e.g., vulnerable to DDoS/APT attacks) and raise data sovereignty concerns when sensitive data must traverse long distances to centralized inference pools. Sectors including finance, healthcare, and public services often mandate localized processing to comply with regulations. However, distributed architectures also introduce their own security challenges: a larger attack surface, potential for model extraction or data leakage from intermediate nodes, and the need for trust among distributed components. The Distributed Inference Network (DIN) aims to address these by providing mechanisms for secure, verifiable inference within a trusted perimeter while enabling the benefits of distribution. 

The rise of AI agents adds new dimensions: agents may be created, migrated, or terminated dynamically, requiring the network to support agent identity, discovery, and stateful communication across distributed nodes. Current networks lack the necessary abstractions to handle agent-scale dynamics.



# Use Cases

## Enterprise Secure Inference Services
Enterprises in regulated sectors such as finance, healthcare, industrial and public services require strict data governance while leveraging advanced AI capabilities. In this use case, inference servers are deployed at enterprise headquarters or private cloud environments, with branch offices and field devices accessing these services through heterogeneous network paths including dedicated lines, VPNs, and public internet connections. 

The scenario encompasses various enterprise applications such as AIoT equipment inspection, intelligent manufacturing, and real-time monitoring systems that demand low-latency, high-reliability, and high-security inference services. Different network paths should provide appropriate levels of cryptographic assurance and quality of service while accommodating varying bandwidth and latency characteristics across the enterprise network topology. 

The primary challenge involves maintaining data sovereignty and security across diverse network access scenarios while ensuring consistent low-latency performance for delay-sensitive industrial applications.

## Edge-Cloud Collaborative Model Training
Small and medium enterprises often need to dynamically procure additional AI inference capacity while facing capital constraints for full-scale inference infrastructure deployment. This use case enables flexible resource allocation where businesses maintain core computational resources on-premises while dynamically procuring additional inference capacity from AI inference providers during demand peaks. 

The hybrid deployment model allows sensitive data to remain within enterprise boundaries while leveraging elastic cloud resources for computationally intensive operations. As enterprise business requirements fluctuate, the ability to seamlessly integrate local and cloud-based inference resources becomes crucial for maintaining service quality while controlling operational costs. 

The network should support efficient coordination between distributed computational nodes, ensuring stable performance during resource scaling operations and maintaining inference pipeline continuity despite variations in network conditions across different service providers.

## Dynamic Model Selection and Coordination
The transition from content access to model inference access necessitates intelligent model selection mechanisms that dynamically route requests to optimal computational resources. This use case addresses scenarios where applications should automatically select between different model sizes, specialized accelerators, and geographic locations based on real-time factors including network conditions, computational requirements, accuracy needs, and cost considerations. 

The inference infrastructure should support real-time assessment of available resources, intelligent traffic steering based on application characteristics, and graceful degradation during resource constraints. 

Key requirements include maintaining service continuity during model switching, optimizing the balance between response time and inference quality, and ensuring consistent user experience across varying operational conditions. This capability is particularly important for applications serving diverse user bases with fluctuating demand patterns and heterogeneous device capabilities.


## Adaptive Inference Resource Scheduling and Coordination
The evolution from content access to model inference necessitates intelligent resource coordination across different computational paradigms. This use case addresses scenarios where inference workloads require adaptive resource allocation strategies to balance performance, cost, and efficiency across distributed environments.

Large-small model collaboration represents a key approach for balancing inference accuracy and response latency. In this pattern, large models handle complex reasoning tasks while small models provide efficient specialized processing, requiring the network to deliver low-latency connectivity and dynamic traffic steering between distributed model instances. The network should ensure efficient synchronization and coherent data exchange to maintain service quality across the collaborative ecosystem.

Prefill-decode separation architecture provides an optimized framework for streaming inference tasks. This pattern distributes computational stages across specialized nodes, with prefilling and decoding phases executing on optimized resources. The network should provide high-bandwidth connections for intermediate data transfer and reliable transport mechanisms to maintain processing pipeline continuity, enabling scalable handling of concurrent sessions while meeting real-time latency requirements.

The network infrastructure should support dynamic workload distribution, intelligent traffic steering, and efficient synchronization across distributed nodes. This comprehensive approach ensures optimal user experience while maximizing resource utilization efficiency across the inference ecosystem.


## Privacy-Preserving Split Inference
Sectors with stringent data privacy regulations, such as healthcare, finance, and government, require robust mechanisms to protect sensitive information while leveraging the power of large AI models. In this use case, data sovereignty is paramount: raw data such as patient records, financial transactions, or classified documents cannot leave the organization's premises. However, these organizations often lack the elastic computing resources needed to run large-scale foundation models on-premises.

A layered split inference architecture addresses this challenge by partitioning the model across the edge and cloud. The embedding layer and the last few layers are deployed on-premises, while intermediate layers are hosted in the cloud. The user's prompt is processed locally, and intermediate activations (hidden variables) are transmitted to the cloud for further computation. The final token generation occurs on-premises, ensuring that raw data never leaves the secure perimeter. This approach not only satisfies data sovereignty and compliance requirements but also enhances model security, as only partial model layers are exposed to the cloud, preventing full model reconstruction. Furthermore, it allows organizations to scale their inference capacity elastically by leveraging cloud resources during demand peaks, overcoming the physical constraints of on-premises infrastructure.

The network connecting the on-premises and cloud nodes must provide deterministic low-latency and high-bandwidth connectivity for transmitting hidden variables, as delays directly impact the user experience in clinical, financial, or governmental settings. Robust security mechanisms are essential to protect these intermediate representations from eavesdropping and tampering during transmission.


## AI Agent Inference Services
AI agents are autonomous software entities that combine AI inference with decision-making and inter-agent communication. They can be deployed in various forms, including software agents running on user devices (e.g., smartphones, PCs), or embedded agents in IoT devices and robots. These agents interact not only with each other in multi-agent systems, but also with various tools, APIs, existing applications, web services, and software through function calling or other mechanisms. Additionally, human-agent interaction remains essential, particularly when agents require human confirmation for critical decisions. This diverse interaction landscape spans a wide range of applications, including personal scheduling, smart home automation, industrial process control, and real-time monitoring.

Unlike human-AI conversations, which may tolerate moderate latency, the communication between agents and tools or between agents themselves often demands extremely low latency to ensure timely execution of tasks. The network should therefore provide deterministic, low-latency connectivity for these machine-to-machine interactions, while also supporting dynamic agent discovery, seamless migration of agents across locations (e.g., from a mobile device to edge), and efficient coordination among distributed agents with reliable and secure interactions. Furthermore, as agents may be ephemeral or long-lived, the network needs to handle rapid creation and termination of agent sessions without impacting ongoing services.


## Heterogeneous Agent Interworking Gateway

The growing deployment of AI agents in various environments, from smart homes and enterprises to industrial IoT, has created a significant interoperability challenge. Devices and agents from different vendors often operate on proprietary protocols and lack standard communication interfaces, hindering seamless collaboration. While initiatives such as OpenClaw or Hermes exist to address this, they often require high performance hardware and complex configuration, limiting their widespread adoption.

In this use case, a gateway or edge node functions as a local broker for heterogeneous AI agents. This gateway provides a unified interface for agents from different vendors to register, discover, and communicate with each other and with external services. For instance, in a smart home, a user could issue a single command to the gateway to orchestrate actions across lighting, security, and entertainment systems from multiple brands. In an enterprise, such a gateway could coordinate various AI-powered monitoring and response agents.

This gateway should be deployed at the network edge (e.g., residential gateway, BRAS, enterprise edge) to minimize latency for inter-agent communication and to keep sensitive data local. The gateway should be simple to set up, configure, and maintain, particularly for non-technical users. It should not require the purchase of specialized high performance gateway hardware or the installation of complex gateway software. The onboarding process for new agents should be intuitive and require minimal user intervention, ensuring broad accessibility and ease of deployment in home and small-office environments. By providing vendor-agnostic discovery and messaging standards, the gateway enables a plug-and-play ecosystem for AI agents, fostering innovation and improving user experience.


# Requirements

## Scalability and Elasticity Requirements

Distributed Inference Network should support seamless scaling to accommodate billions of concurrent inference sessions while maintaining consistent performance levels. The network should provide mechanisms for dynamic discovery and integration of new inference nodes, with automatic load distribution across available resources. Elastic scaling should respond to diurnal patterns and sudden demand spikes without service disruption. As AI agents can be created, migrated, or terminated dynamically, the network should support rapid provisioning and release of network resources associated with agent lifecycles.

## Performance and Determinism Requirements

AI inference workloads require consistent and predictable network performance to ensure reliable service delivery. The network should provide strict Service Level Agreement (SLA) guarantees for latency, jitter, and packet loss to support various distributed inference scenarios. Bandwidth provisioning should accommodate bursty traffic patterns characteristic of model parameter exchanges and intermediate data synchronization, with performance isolation between different inference workloads.

In distributed inference scenarios where model layers are partitioned across on-premises and cloud nodes, the network should provide low-latency and high-bandwidth connectivity to ensure timely transmission of intermediate activations. Additionally, for scenarios involving communication between distributed agents or between agents and tools, the network should enable low-latency communication channels that prefer local processing at the edge to minimize round-trip delays.

## Security and Privacy Requirements

Comprehensive security mechanisms should protect AI models, parameters, and data throughout their transmission across network links. Cryptographic protection should be applied at appropriate layers (e.g., network, transport, or application) depending on the deployment scenario, with key management and authentication integrated. Privacy-preserving techniques should prevent leakage of sensitive information through intermediate representations while supporting efficient distributed inference.

When model partitioning is used to keep raw data on-premises, security mechanisms MUST protect intermediate computational results exchanged between edge and cloud nodes from eavesdropping and tampering. Gateways that coordinate communication between heterogeneous agents should enforce access control policies to ensure that only authenticated and authorized agents can join the network and access services. The network should also provide mechanisms to support agent identity verification and policy enforcement at the edge.

## Identification and Scheduling Requirements

The network should support fine-grained identification of inference workloads to enable appropriate resource allocation and path selection. Application-aware networking capabilities should allow inference requests to be steered to optimal endpoints based on current load, network conditions, and computational requirements. These identifiers, such as agent ID, workflow ID, or job ID, are typically defined by the application. Similar to DNS maps URL to IP address, the network may need to map application layer name or id to network-layer addresses or labels, and to enable efficient resource routing and orchestration. The network should also support agent registration, discovery, and stateful handover across distributed nodes. Both centralized and distributed scheduling approaches should be supported to accommodate different deployment scenarios and organizational preferences.

## Management and Observability Requirements

The network should provide comprehensive telemetry for performance monitoring, fault detection, and capacity planning. Metrics should include inference-specific measurements such as token latency, throughput, and computational efficiency in addition to traditional network performance indicators. Management interfaces should support automated optimization and troubleshooting across the combined compute-network infrastructure. The management system should also support the lifecycle management of AI agents, including registration, de-registration, health monitoring, and graceful shutdown, to adapt to the dynamic nature of agent-based applications.


## Authentication, Authorization, and Accounting (AAA) for Distributed Inference and Agents
The distributed nature of DIN, particularly the proliferation of AI agents and diverse inference workloads, introduces a critical need for robust Authentication, Authorization, and Accounting (AAA) mechanisms. This requirement is analogous to the role of AAA in residential broadband networks, where subscribers are authenticated, authorized based on their subscription, and subject to per-session accounting and traffic policies. However, traditional AAA operates at the level of the subscriber and does not authenticate individual applications or agents running within that subscriber's network, nor does it provide granular authorization for AI inference services.

In the context of DIN, the network should support agent-level AAA. Each agent or inference workload should have a unique identity that is cryptographically verified before it can access network resources or inference services. This enables granular access control, usage accounting and billing, and enhanced security and trust. The AAA framework should be implemented via a trust anchor at the edge (e.g., residential gateway, enterprise edge) that authenticates agents using credentials (e.g., certificates, API keys) and communicates with a central AAA server that authorizes service access. The network should provide interfaces for agents to present their credentials and for the edge node to enforce policies based on the AAA outcome. The system should also support the management of agent identities throughout their lifecycle, including provisioning, suspension, and revocation.


# Security Considerations

This document highlights security as a fundamental requirement for DIN. The distributed nature of inference workloads creates new attack vectors including model extraction, data reconstruction from intermediate outputs, and adversarial manipulation of inference results. Security mechanisms should operate at multiple layers while maintaining the performance characteristics necessary for efficient inference.

Compared to centralized architectures, distributed inference increases the attack surface but also enables localized processing that can reduce data exposure. The DIN should provide mechanisms to establish trust among nodes, such as attestation and secure key distribution.


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The authors would like to thank the contributors from China Mobile Research Institute for their valuable inputs and discussions. 

