---
title: JsonObject::operator[]
description: Gets or replaces a value in a JsonObject
keywords: ArduinoJson,JsonObject,get,set,read,write
layout: api
tags: api
api-group: JsonObject
---

##### Description

A shortcut for [`JsonObject::get()`]({{site.baseurl}}/api/jsonobject/get/) and
[`JsonObject::set()`]({{site.baseurl}}/api/jsonobject/set/), with a map-like syntax.

##### Signatures

```c++
JsonVariant& operator[](const char* key);
JsonVariant& operator[](const String& key);
JsonVariant& operator[](const std::string& key);
JsonVariant& operator[](const __FlashStringHelper* key);

const JsonVariant& operator[](const char* key) const;
const JsonVariant& operator[](const String& key) const;
const JsonVariant& operator[](const std::string& key) const;
const JsonVariant& operator[](const __FlashStringHelper* key) const;
```

##### Arguments

`key`: the key that the value will be associated to.

##### Return value

A reference to the [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/description/) in the object.

##### Remarks

When you add a value using a `String`, an `std::string` or a
`const __FlashStringHelper*` for key, a copy of the string is made, causing the
[`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/) to grow.
The memory allocated for the copy will only be freed when the whole
[`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/) is discarded.
To avoid this behavior, use a `const char*` key instead.

##### Example

```c++
JsonObject& object = jsonBuffer::createObject();
object["hello"] = "world";
const char* world = object["hello"];
```

##### See also

* [`JsonObject::get<T>()`]({{site.baseurl}}/api/jsonobject/get/)
* [`JsonObject::set()`]({{site.baseurl}}/api/jsonobject/set/)
* [`JsonArray::operator[]`]({{site.baseurl}}/api/jsonarray/subscript/)
