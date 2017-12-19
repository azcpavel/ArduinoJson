---
title: JsonArray::set()
description: Replaces a value in a JsonArray
keywords: ArduinoJson,JsonArray,set,write,replace
layout: api
tags: api
api-group: JsonArray
---

### Description

Sets the value at specified index.

### Signatures

```c++
bool set(size_t index, bool value);
bool set(size_t index, const char *value);
bool set(size_t index, double value);
bool set(size_t index, float value);
bool set(size_t index, signed char value);
bool set(size_t index, signed int value);
bool set(size_t index, signed long value);
bool set(size_t index, signed short value);
bool set(size_t index, unsigned char value);
bool set(size_t index, unsigned int value);
bool set(size_t index, unsigned long value);
bool set(size_t index, unsigned short value);
bool set(size_t index, const std::string &value); // see Remarks
bool set(size_t index, const String &value); // see Remarks
bool set(size_t index, const __FlashStringHelper *value); // see Remarks
bool set(size_t index, JsonArray &array);
bool set(size_t index, JsonObject &object);
bool set(size_t index, const JsonVariant &value);
```

### Arguments

`index`: the index in the array (starting from 0).

`value`: the value to set.

### Return value

`true` if allocation succeeded.

`false` if there was not enough space left in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), this can only happen when `value` needs to be copied (see below).

### Remarks

A copy of the string is made when you call this function with one of the following types:

* `String`
* `std::string`
* Flash string (`PROGMEM`)

This duplication causes the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) to grow.
The memory allocated for the copy will only be freed when the whole [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is discarded.

To avoid this behavior, use `const char*` to pass the string.

### Example

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.createArray();

// increase the size of the array
array.add(666);
array.add(666);

// replace the values
array.set(0, "hello");
array.add(1, 3.14156);

// serialize
array.printTo(Serial);
```

will write

```json
["hello",3.14156]
```

### See also

* [`JsonArray::add()`]({{site.baseurl}}/api/jsonarray/add/)
* [`JsonArray::get<T>()`]({{site.baseurl}}/api/jsonarray/get/)
* [`JsonArray::operator[]`]({{site.baseurl}}/api/jsonarray/subscript/)
* [`JsonObject::set()`]({{site.baseurl}}/api/jsonobject/get/)
