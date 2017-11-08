---
title: JsonArray::prettyPrintTo()
description: Serializes a JsonArray to prettified JSON
keywords: ArduinoJson,JsonArray,serialize,encode,generate
layout: api
tags: api
api-group: JsonArray
---

##### Description

Serialize the array to an indented JSON string.

This will create a "prettified" JSON, if you want a compact JSON without space or line break, use [`JsonArray::printTo()`]({{site.baseurl}}/api/jsonarray/printto/)

##### Signatures

```c++
size_t prettyPrintTo(char* buffer, size_t size) const;
size_t prettyPrintTo(char buffer[size]) const;
size_t prettyPrintTo(Print &) const;
size_t prettyPrintTo(String &) const;
size_t prettyPrintTo(std::string &) const;
```

##### Arguments

The destination of the JSON string.

Can be either:

* a `buffer` with specified `size` (this includes the zero-terminator)
* an implementation of `Print` (like `Serial`, `EthernetClient`...)
* a `String` or `std::string`

##### Return value

The number of bytes written

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.createArray();
array.add("hello");
array.add("world");
array.prettyPrintTo(Serial);
```

will write the following string to the serial output:

```json
[
  "hello",
  "world"
]
```

##### See also

* [`JsonArray::printTo()`]({{site.baseurl}}/api/jsonarray/printto/)
* [`JsonArray::measurePrettyLength()`]({{site.baseurl}}/api/jsonarray/measureprettylength/)
* [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/)
