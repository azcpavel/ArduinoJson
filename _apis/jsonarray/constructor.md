---
title: JsonArray constructor
keywords: ArduinoJson,JsonArray
layout: api
tags: api
api-group: JsonArray
---

The constructor is private, you cannot instantiate a `JsonArray` directly.
Instead, you must use  [`JsonBuffer::createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/).

Because the memory of a `JsonArray` is located a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/), you always manipulate it through reference and you cannot copy it.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;

// create an empty array
JsonArray& array1 = jsonBuffer.createArray();

// parse a JSON array
char json[] = "[1,2,3]";
JsonArray& array2 = jsonBuffer.parseArray(json);
```

##### See also

* [`JsonBuffer::createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/)
* [`JsonBuffer::parseArray()`]({{site.baseurl}}/api/jsonbuffer/parsearray/)