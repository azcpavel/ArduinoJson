---
title: JsonArray::createNestedObject()
description: Adds a JsonObject in a JsonArray
keywords: ArduinoJson,JsonArray,createNestedObject
layout: api
tags: api
api-group: JsonArray
---

##### Description

Adds a new nested object to the end of the array.

##### Signature

```c++
JsonObject& createNestedObject();
```

##### Return value

A reference to the new `JsonObject`.
You can check [`JsonObject::success()`]({{site.baseurl}}/api/jsonobject/success/) to verify that the allocation succeeded.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.createArray();
JsonObject& nested = array.createNestedObject();
nested["hello"] = "world";
array.printTo(Serial);
```

will write

```json
[{"hello":"world"}]
```

##### See also

* [`JsonArray::createNestedArray()`]({{site.baseurl}}/api/jsonarray/createnestedarray/)
* [`JsonBuffer::createObject()`]({{site.baseurl}}/api/jsonbuffer/createobject/)
* [`JsonArray::add()`]({{site.baseurl}}/api/jsonarray/add/)