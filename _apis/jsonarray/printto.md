---
title: JsonArray::printTo()
description: The function JsonArray::printTo() serializes the JsonArray to create a minified JSON document.
keywords: ArduinoJson,JsonArray,serialize,encode,generate
layout: api
tags: api
api-group: JsonArray
---

##### Description

Serializes the `JsonArray` to create a *minified* JSON document.

If you want a pretty JSON with spaces and line breaks, use [`JsonArray::prettyPrintTo()`]({{site.baseurl}}/api/jsonarray/prettyprintto/)

##### Signatures

```c++
size_t printTo(char* buffer, size_t size) const;
size_t printTo(char buffer[size]) const;
size_t printTo(Print &) const;
size_t printTo(String &) const;
size_t printTo(std::string &) const;
```

##### Arguments

The destination where the JSON document should be written.
It can be either:

* a `buffer` with specified `size` (the size includes the zero-terminator),
* an implementation of `Print` (like `Serial`, `EthernetClient`...),
* a `String` or `std::string`.

##### Return value

The number of bytes written.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.createArray();
array.add("hello");
array.add("world");
array.printTo(Serial);
```

will write the following string to the serial port:

```json
["hello","world"]
```

##### See also

* [`JsonArray::prettyPrintTo()`]({{site.baseurl}}/api/jsonarray/prettyprintto/)
* [`JsonArray::measureLength()`]({{site.baseurl}}/api/jsonarray/measurelength/)
* [`JsonObject::printTo()`]({{site.baseurl}}/api/jsonobject/printto/)
* [`JsonVariant::printTo()`]({{site.baseurl}}/api/jsonvariant/printto/)