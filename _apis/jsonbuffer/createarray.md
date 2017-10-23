---
title: JsonBuffer::createArray()
description: Creates a JsonArray
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,createArray,JsonArray
layout: api
tags: api
api-group: JsonBuffer
---

##### Description
Allocates an empty JsonArray.

##### Signature
```c++
JsonArray& createArray();
```
##### Return value
Returns a reference to the new JsonArray or JsonArray::invalid() if the allocation fails.
##### Example
```c++
StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.createArray();
array.add("hello");
array.add("world");
```
