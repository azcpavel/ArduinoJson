---
title: JsonVariant::prettyPrintTo()
description: The function JsonVariant::prettyPrintTo() serializes the JsonVariant to create a prettified JSON document.
keywords: ArduinoJson,JsonVariant,serialize
layout: api
tags: api
api-group: JsonVariant
---

## Description

Serializes the [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/) to create a prettified JSON document.

If you want a "minified" JSON document, use [`JsonVariant::printTo()`]({{site.baseurl}}/api/jsonvariant/printto/)

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

JsonVariant variant = object;
variant.prettyPrintTo(Serial);
```

will write the following string to the serial output:

```json
{
  "hello": "world"
}
```

## See also

* [`JsonVariant::printTo()`]({{site.baseurl}}/api/jsonvariant/printto/)
* [`JsonVariant::measurePrettyLength()`]({{site.baseurl}}/api/jsonvariant/measureprettylength/)
* [`JsonArray::prettyPrintTo()`]({{site.baseurl}}/api/jsonarray/prettyprintto/)
* [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/)
