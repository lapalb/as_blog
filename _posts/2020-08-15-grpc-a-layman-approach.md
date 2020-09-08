---
layout: post
title: "gRPC: A layman's approach"
date: 2020-08-15 10:45:54 +0530
categories: Tech
 -
---

### What is gRPC
1. Open Source RPC System
2. developed by Google in 2015
3. Use HTTP/2 for Transport and Protobuf as interface description language.
4. Provides features such as authentication, **bidirectional** streaming and flow control, blocking or nonblocking bindings, and cancellation and timeouts.
5. generates cross-platform client and server bindings for many languages

<img src="https://grpc.io/img/landing-2.svg">
### Where we use gRPC
1. connecting services in microservices style architecture
2. Connecting mobile devices and browser client to Backend Service
3. gRPC user protobuf, contrary to JSON. Hence follows strict specification

The client and server can talk to each other in variety of environment

### Working with protbuf
Protobuf is data language which is used to serialize structured data(Object, Array). It is faster than JSON and XML.

1. Create .proto file
2. Define the structure for the data you want to serialize
```protobuf
message Person {
  string name = "Akanksha";
  int32 id = 1;
  bool is_mcu_fan = false;
}
```
3. Use the protocol buffer compiler `protoc` to generate data access classes in  preferred language(s) from your proto definition.These provide simple accessors for each field, like `name()` and `set_name()`, as well as methods to serialize/parse the whole structure to/from raw bytes.

### Core concepts, architecture and lifecycle
 gRPC is based around the idea of defining a service, specifying the methods that can be called remotely with their parameters and return types.

gRPC lets you define four kinds of service method:
1. Single Request, Single Response `Unary RPC `
2. Single Request, Stream Response `Serve Streaming RPC`
3. Stream Request, Single Response `Client Streaming RPC`
4. Stream Request, Stream Response  `Bidirectional streaming RPC`

The gRPC programming API in most languages comes in both synchronous and asynchronous flavors. 

gRPC supports termination and cancellation of RPC request and deadline for waits.