---
title: JsonArray::operator[]
description: Gets or replaces a value in a JsonArray
keywords: ArduinoJson,JsonArray,get,set,read,write
layout: api
tags: api
api-group: JsonArray
---

### Description

A shortcut for [`JsonArray::get()`]({{site.baseurl}}/api/jsonarray/get/) and [`JsonArray::set()`]({{site.baseurl}}/api/jsonarray/set/), with an array-like syntax.

### Signatures

```c++
JsonVariant& operator[](size_t index);
const JsonVariant& operator[](size_t index) const;
```

### Arguments

`index`: the zero-based position of the value in the array.

### Return value

A reference to the [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/) in the array.

### Example

```c++
JsonArray& array = jsonBuffer::createArray();
array.add(42);
int value = array[0];
array[0] = 666;
```

### See also

* [`JsonArray::get<T>()`]({{site.baseurl}}/api/jsonarray/get/)
* [`JsonArray::set()`]({{site.baseurl}}/api/jsonarray/set/)
* [`JsonObject::operator[]`]({{site.baseurl}}/api/jsonobject/subscript/)
