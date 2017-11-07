---
title: JsonArray::add()
description: Adds a value to a JsonArray
keywords: ArduinoJson,JsonArray,add
layout: api
tags: api
api-group: JsonArray
---

##### Description

Adds a value to the end of the array.

##### Signatures

```c++
bool add(bool value);
bool add(float value);
bool add(double value);
bool add(signed char value);
bool add(signed long value);
bool add(signed int value);
bool add(signed short value);
bool add(unsigned char value);
bool add(unsigned long value);
bool add(unsigned int value);
bool add(unsigned short value);
bool add(const char *value);
bool add(const String &value); // see Remarks
bool add(const std::string &value); // see Remarks
bool add(const __FlashStringHelper *value); // see Remarks
bool add(JsonArray &array);
bool add(JsonObject &object);
bool add(const JsonVariant &variant);
```

##### Arguments

`value`: the value to add to the array.

##### Return value

`true` if the value was successfully added.

`false` if there was not enough memory in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/).

##### Remarks

A copy of the string is made when you call this function with one of the following types:

* `String`
* `std::string`
* Flash string (`PROGMEM`)

This duplication causes the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/) to grow.
The memory allocated for the copy will only be freed when the whole [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/) is discarded.

To avoid this behavior, use `const char*` to pass the string.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.createArray();
array.add("hello");
array.add(3.14156);
array.printTo(Serial);
```

will write

```json
["hello",3.14156]
```

##### See also

* [`JsonArray::set()`]({{site.baseurl}}/api/jsonarray/set/)
