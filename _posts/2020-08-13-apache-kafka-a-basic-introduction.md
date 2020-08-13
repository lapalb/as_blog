---
layout: post
title: "Apache Kafka : A Basic Introduction"
tags:
 -
---
Apache Kafka is messaging system developed by LinkedIn and donated to Apache Foundation. This is De-Facto messaging system used for Server Side development.
It uses Publisher Subscriber Design Pattern.

![Apache Kafka](https://kafka.apache.org/images/logo.png)

> Apache Kafka is an open-source distributed event streaming platform used by thousands of companies for high-performance data pipelines, 
streaming analytics, data integration, and mission-critical applications.

 
 #### What is Event Streaming
 Event streaming is the practice of capturing data in real-time from event sources like databases, sensors, mobile devices, cloud services, and software applications in the form of streams of events; storing these event streams durably for later retrieval; manipulating, processing, and reacting to the event streams in real-time as well as retrospectively; and routing the event streams to different destination technologies as needed.

 #### Capabilities of Kafka
 1. To Write(Publish) and Read(Subscribe)
 2. To Store Stream of Event durably.
 3. To Process Stream of Event as they occur

 #### Where Kafka Can be Deployed?
 1. Bare Metal Hypervisor like KVM or ESXi
 2. VMs
 3. On-Prem
 4. Cloud

 We can self manage kafka environment or get it managed by SP

 #### How Kafka Works:
 Kafka is a distributed System consisting of Servers and Clients which communicate via TCP/IP Stack.

 1. Servers: Kafka run as a cluster of multiple servers than can span over multiple DC and Cloud Region. Some of these server form storage layer called broker and other use Kafka Connect to import and export data

 2. Client: Allows you to write Distributed Application and MicroServices that read/write and process stream of data in parallel at scale in a fault tolerant system


 #### Main Concepts and Terminology

 1. Event: Also knowns by record or message. A testimony that something has happened in real world. An Event has key, Value, TimeStamp and Metadata.

 Producer and Subscriber are agnostic to each other. Events are organized and stored as topic(Kinda Folder). Multiple Producer and Subscriber can write on a Topic. We can have a config file per topic, where we can define how long we can store some Event

 Topics are partitioned, meaning a topic is spread over a number of "buckets" located on different Kafka brokers.

 To Ensure Fault Tolerant, we replicate the topic over multiple data centre across multiple region. A common production setting is a replication factor of 3


 ##### Kafka APIs
 1. Admin API:  to manage and inspect topics, brokers, and other Kafka objects.
 2. Producer API:  to publish (write) a stream of events to one or more Kafka topics.
 3. Consumer API: to consume (read) a stream of events to one or more kafka topics
 4. Connect API: to build and run reusable data import and export connector
 5. Kafka Stream API: To implement stream processing application and microservices