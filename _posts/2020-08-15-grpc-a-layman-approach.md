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

### Where we use gRPC
1. connecting services in microservices style architecture
2. Connecting mobile devices and browser client to Backend Service
3. gRPC user protobuf, contrary to JSON. Hence follows strict specification