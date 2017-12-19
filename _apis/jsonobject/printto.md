---
title: JsonObject::printTo()
description: The function JsonObject::printTo() serializes the JsonObject to create a minified JSON document.
keywords: ArduinoJson,JsonObject,serialize,minified
layout: api
tags: api
api-group: JsonObject
---

### Description

Serializes the `JsonObject` to create a *minified* JSON document.

If you want a *prettified* JSON document, use [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/).

### Signatures

```c++
size_t printTo(char* buffer, size_t size) const;
size_t printTo(char buffer[size]) const;
size_t printTo(Print &) const;
size_t printTo(String &) const;
size_t printTo(std::string &) const;
```

### Arguments

The destination where the JSON document should be written.
It can be either:

* a `buffer` with specified `size` (the size includes the zero-terminator),
* an implementation of `Print` (like `Serial`, `EthernetClient`...),
* a `String` or an `std::string`.

### Return value

The number of bytes written.

### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonObject& object = jsonBuffer.createObject();
object["hello"] = "world";
object.printTo(Serial);
```

will write the following string to the serial port:

```json
{"hello":"world"}
```

### See also

* [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/)
* [`JsonObject::measureLength()`]({{site.baseurl}}/api/jsonobject/measurelength/)
* [`JsonArray::printTo()`]({{site.baseurl}}/api/jsonarray/printto/)
* [`JsonVariant::printTo()`]({{site.baseurl}}/api/jsonvariant/printto/)