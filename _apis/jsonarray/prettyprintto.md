---
title: JsonArray::prettyPrintTo()
description: The function JsonArray::prettyPrintTo() serializes the JsonArray:to create a prettified JSON document.
keywords: ArduinoJson,JsonArray,serialize,encode,generate
layout: api
tags: api
api-group: JsonArray
---

## Description

Serializes the [`JsonArray`]({{site.baseurl}}/api/jsonarray/) to create a prettified JSON document.

If you want a compact JSON without space or line break, use [`JsonArray::printTo()`]({{site.baseurl}}/api/jsonarray/printto/)

## Signatures

```c++
size_t prettyPrintTo(char* buffer, size_t size) const;
size_t prettyPrintTo(char buffer[size]) const;
size_t prettyPrintTo(Print &) const;
size_t prettyPrintTo(String &) const;
size_t prettyPrintTo(std::string &) const;
```

## Arguments

The destination where the JSON document should be written.
It can be either:

* a `buffer` with specified `size` (the size includes the zero-terminator),
* an implementation of `Print` (like `Serial`, `EthernetClient`...),
* a `String` or an `std::string`.

## Return value

The number of bytes written.

## Example

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

## See also

* [`JsonArray::printTo()`]({{site.baseurl}}/api/jsonarray/printto/)
* [`JsonArray::measurePrettyLength()`]({{site.baseurl}}/api/jsonarray/measureprettylength/)
* [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/)
* [`JsonVariant::prettyPrintTo()`]({{site.baseurl}}/api/jsonvariant/prettyprintto/)
