---
title: JsonArray::get&lt;T&gt;()
description: The function JsonArray::get&lt;T&gt;() returns the value at specified index.
keywords: ArduinoJson,JsonArray,get,read
layout: api
tags: api
api-group: JsonArray
---

##### Description

Gets the value at the specified index.

##### Signature

```c++
bool            get<bool>           (size_t index) const;
const char*     get<const char*>    (size_t index) const;
const char*     get<char*>          (size_t index) const;
double          get<double>         (size_t index) const;
float           get<float>          (size_t index) const;
signed char     get<signed char>    (size_t index) const;
signed int      get<signed int>     (size_t index) const;
signed long     get<signed long>    (size_t index) const;
signed short    get<signed short>   (size_t index) const;
unsigned char   get<unsigned char>  (size_t index) const;
unsigned int    get<unsigned int>   (size_t index) const;
unsigned long   get<unsigned long>  (size_t index) const;
unsigned short  get<unsigned short> (size_t index) const;
JsonVariant     get<JsonVariant>    (size_t index) const;
std::string     get<std::string>    (size_t index) const;
String          get<String>         (size_t index) const;
```

##### Arguments

`index`: the index of the value in the array.

`T`: the type of the value.

##### Return value

The value at the specified index. This can be a [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/description/) or a value of type T.

Returns a value whose type matches the template parameter `T`.

In the case of an error (index out of range or incompatible type), the default value for the type `T` is returned:

* `0` for an integer
* `0.0` for a double
* `NULL` for a `char*`
* etc.

##### Example

```c++
char json[] = "[1,3.14]";
StaticJsonBuffer<256> jsonBuffer;
JsonArray& array = jsonBuffer.parseArray(json);
int value0 = array.get(0); // implicit cast of the JsonVariant
float value1 = array.get<float>(1); // template version of get()
const char* value2 = array.get(2); // returns NULL
```

##### See also

* [`JsonArray::operator[]`]({{site.baseurl}}/api/jsonarray/subscript/)
* [`JsonArray::set()`]({{site.baseurl}}/api/jsonarray/set/)
* [`JsonObject::get<T>()`]({{site.baseurl}}/api/jsonobject/get/)
