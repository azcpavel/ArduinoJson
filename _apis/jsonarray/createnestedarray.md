---
title: JsonArray::createNestedArray()
description: Adds a JsonArray in a JsonArray
keywords: ArduinoJson,JsonArray,createNestedArray
layout: api
tags: api
api-group: JsonArray
---

##### Description

Adds a new nested array to the end of the array.

##### Signature

```c++
JsonArray& createNestedArray();
```

##### Return value

A reference to the new `JsonArray`.
You can check [`JsonArray::success()`]({{site.baseurl}}/api/jsonarray/success/) to verify that the allocation succeeded.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.createArray();
array.add("hello");
JsonArray& nested = array.createNestedArray();
nested.add("world");
array.printTo(Serial);
```

will write

```json
["hello",["world"]]
```

##### See also

* [`JsonArray::createNestedObject()`]({{site.baseurl}}/api/jsonarray/createnestedobject/)
* [`JsonBuffer::createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/)
* [`JsonArray::add()`]({{site.baseurl}}/api/jsonarray/add/)