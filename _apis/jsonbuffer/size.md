---
title: JsonBuffer::size()
description: Gets memory usage of a JsonBuffer
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,size,length
layout: api
tags: api
api-group: JsonBuffer
---

## Description

Gets the current size (i.e. the number of bytes used) of the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).

This should not be confused with the capacity of the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), which is the total number of bytes that the buffer can hold.

## Signatures

```c++
size_t size() const;
```

## Return value

The size (ie the number of bytes used) of the `JsonBuffer`.

## Example

```c++
StaticJsonBuffer<200> jsonBuffer;
Serial.println(jsonBuffer.size());
jsonBuffer.createObject();
Serial.println(jsonBuffer.size());
jsonBuffer.createArray();
Serial.println(jsonBuffer.size());
```

would print this on an 8-bit AVR:

```
0
4
8
```

## See also

* [`JsonArray::size()`]({{site.baseurl}}/api/jsonarray/size/)
* [`JsonObject::size()`]({{site.baseurl}}/api/jsonobject/size/)
