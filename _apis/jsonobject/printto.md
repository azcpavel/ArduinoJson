---
title: JsonObject::printTo()
description: Serializes a JsonObject to JSON
keywords: ArduinoJson,JsonObject,serialize
layout: api
tags: api
api-group: JsonObject
---

##### Description

Serialize the object to a JSON string.

This function will create a "minified" JSON document.
If you want a "prettified" JSON document, use [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/).

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

* a `buffer` with specified `size` (this includes the zero-terminator),
* an implementation of `Print` (like `Serial`, `EthernetClient`...),
* a `String` or an `std::string`.

##### Return value

The number of bytes written.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonObject& object = jsonBuffer.createObject();
object["hello"] = "world";
object.printTo(Serial);
```

will write the following string to the serial output:

```json
{"hello":"world"}
```

##### See also

* [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/)
* [`JsonObject::measureLength()`]({{site.baseurl}}/api/jsonobject/measurelength/)
* [`JsonArray::printTo()`]({{site.baseurl}}/api/jsonarray/printto/)