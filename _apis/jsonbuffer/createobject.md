---
title: JsonBuffer::createObject()
description: Creates a JsonObject
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,createObject,JsonObject
layout: api
tags: api
api-group: JsonBuffer
---

### Description

Allocates an empty `JsonObject`.

### Signature

```c++
JsonObject createObject();
```

### Return value

Returns a reference to the new `JsonObject` or `JsonObject::invalid()` if the allocation fails.

### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonObject& object = jsonBuffer.createObject();
object["hello"] = "world";
```

### See also

* [`JsonBuffer::createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/)
* [`JsonArray::createNestedObject()`]({{site.baseurl}}/api/jsonarray/createnestedobject/)
* [`JsonObject::createNestedObject()`]({{site.baseurl}}/api/jsonobject/createnestedobject/)