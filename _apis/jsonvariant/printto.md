---
title: JsonVariant::printTo()
description: The function JsonVariant::printTo() serializes the JsonVariant to create a minified JSON document.
keywords: ArduinoJson,JsonVariant,serialize,encode,generate
layout: api
tags: api
api-group: JsonVariant
---

## Description

Serializes the `JsonVariant` to create a *minified* JSON document.

If you want a pretty JSON with spaces and line breaks, use [`JsonVariant::prettyPrintTo()`]({{site.baseurl}}/api/jsonvariant/prettyprintto/)

## Signatures

```c++
size_t printTo(char* buffer, size_t size) const;
size_t printTo(char buffer[size]) const;
size_t printTo(Print &) const;
size_t printTo(String &) const;
size_t printTo(std::string &) const;
```

## Arguments

The destination where the JSON document should be written.
It can be either:

* a `buffer` with specified `size` (the size includes the zero-terminator),
* an implementation of `Print` (like `Serial`, `EthernetClient`...),
* a `String` or `std::string`.

## Return value

The number of bytes written.

## Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonObject& object = jsonBuffer.createObject();
object["hello"] = "world";

JsonVariant variant = object;
variant.printTo(Serial);
```

will write the following string to the serial port:

```json
{"hello":"world"}
```

## See also

* [`JsonVariant::prettyPrintTo()`]({{site.baseurl}}/api/jsonvariant/prettyprintto/)
* [`JsonVariant::measureLength()`]({{site.baseurl}}/api/jsonvariant/measurelength/)
* [`JsonArray::printTo()`]({{site.baseurl}}/api/jsonarray/printto/)
* [`JsonObject::printTo()`]({{site.baseurl}}/api/jsonobject/printto/)