---
title: JsonObject
description: A JsonObject is a collection of named JsonVariant; it allows getting and setting a value by its name.
keywords: ArduinoJson,JsonObject
layout: api
tags: api
api-group: class
---

##### Description

A collection of named [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/).

The constructor is private, you cannot instantiate a `JsonObject` directly, you have to use a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer).

Because the memory of a `JsonObject` is located a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), you always manipulate it through reference and you cannot copy it.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;

// create an object
JsonObject& object1 = jsonBuffer.createObject();
object1["hello"] = "world";

// parse a JSON object
char json[] = "{\"hello\":\"world\"}";
JsonObject& object2 = jsonBuffer.parseObject(json);
```

##### See also

* [`JsonBuffer::createObject()`]({{site.baseurl}}/api/jsonbuffer/createobject/)
* [`JsonBuffer::parseObject()`]({{site.baseurl}}/api/jsonbuffer/parseobject/)
