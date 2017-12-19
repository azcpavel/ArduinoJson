---
title: JsonBuffer::strdup()
description: Copies a string in a JsonBuffer
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,strdup
layout: api
tags: api
api-group: JsonBuffer
---

### Description

Make a copy of the specified string in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).

The memory is released when the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is destructed.

### Signatures

```c++
char* strdup(const char* str);
char* strdup(const String& str);
char* strdup(const std::string& str);
char* strdup(const __FlashStringHelper* str);
```

### Arguments

`str`, the string to duplicate.

### Return value

A newly allocate string, filled with a copy of `str`.

### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
char orig[16] = "hello";
char* dupl = jsonBuffer.strdup(orig);
strcpy(orig, "world");
Serial.println(dupl); // world
Serial.println(orig); // hello
```

### See also

* [`JsonBuffer::createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/)
* [`JsonBuffer::createObject()`]({{site.baseurl}}/api/jsonbuffer/createobject/)


