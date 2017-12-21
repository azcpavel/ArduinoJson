---
title: JsonObject::prettyPrintTo()
description: The function JsonObject::prettyPrintTo() serializes the JsonObject to create a prettified JSON document.
keywords: ArduinoJson,JsonObject,serialize
layout: api
tags: api
api-group: JsonObject
---

## Description

Serializes the [`JsonObject`]({{site.baseurl}}/api/jsonobject/) to create a prettified JSON document.

If you want a "minified" JSON document, use [`JsonObject::printTo()`]({{site.baseurl}}/api/jsonobject/printto/)

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
JsonObject& object = jsonBuffer.createObject();
object["hello"] = "world";
object.prettyPrintTo(Serial);
```

will write the following string to the serial output:

```json
{
  "hello": "world"
}
```

## See also

* [`JsonObject::printTo()`]({{site.baseurl}}/api/jsonobject/printto/)
* [`JsonObject::measurePrettyLength()`]({{site.baseurl}}/api/jsonobject/measureprettylength/)
* [`JsonArray::prettyPrintTo()`]({{site.baseurl}}/api/jsonarray/prettyprintto/)
* [`JsonVariant::prettyPrintTo()`]({{site.baseurl}}/api/jsonvariant/prettyprintto/)
