---
title: JsonArray::size()
description: Gets the number of element in a JsonArray
keywords: ArduinoJson,JsonArray,size,length
layout: api
tags: api
api-group: JsonArray
---

### Description

Returns the number of element in the array.

### Signature

```c++
size_t size() const;
```

### Return value

An unsigned integer containing the number of elements in the array.

### Example

```c++
JsonArray& array = jsonBuffer.createArray();
array.add("hello");
array.add("world");
Serial.println(array.size()); // 2
```

### See also

* [`JsonObject::size()`]({{site.baseurl}}/api/jsonobject/size/)
