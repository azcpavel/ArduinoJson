---
title: JsonArray::is&lt;T&gt;()
description: The function JsonArray::is&lt;T&gt;() tests if the value at specified index has the type T.
keywords: ArduinoJson,JsonArray,get,read
layout: api
tags: api
api-group: JsonArray
---

##### Description

Tests if the value at specified index has the type `T`.

##### Signature

```c++
bool is<bool>           (size_t index) const;
bool is<const char*>    (size_t index) const;
bool is<char*>          (size_t index) const;
bool is<double>         (size_t index) const;
bool is<float>          (size_t index) const;
bool is<signed char>    (size_t index) const;
bool is<signed int>     (size_t index) const;
bool is<signed long>    (size_t index) const;
bool is<signed short>   (size_t index) const;
bool is<unsigned char>  (size_t index) const;
bool is<unsigned int>   (size_t index) const;
bool is<unsigned long>  (size_t index) const;
bool is<unsigned short> (size_t index) const;
bool is<JsonArray>      (size_t index) const;
bool is<JsonObject>     (size_t index) const;
```

##### Arguments

`index`: the index of the value in the array.

`T`: the type to test.

##### Return value

`true` if the value at specified index matches the type `T`; `false` otherwise.

##### Remarks

Different C++ types can store the same JSON value, so `is<T>()` can return `true` for several `T`s. For example, `is<float>()` always returns the same value as `is<double>()` .

The table below gives the correspondence between the JSON type and the C++ types:

| JSON type      | `T`                                 |
|:---------------|:------------------------------------|
| Floating point | `float`, `double`                   |
| Integer        | `int`, `short`, `long`, `long long` |
| String         | `const char*`, `char*`              |
| Boolean        | `bool`                              |
| Array          | `JsonArray`                         |
| Object         | `JsonObject`                        |
{: .table .table-bordered}

Caution: `is<float>()` and `is<double>()` returns `true` for integers too.

##### Example

```c++
char json[] = "[\"pi\",3.14]";
StaticJsonBuffer<256> jsonBuffer;
JsonArray& array = jsonBuffer.parseArray(json);

bool firstIsString = array.is<char*>(0); // <- true
bool secondIsFloat = array.is<float>(1); // <- true

// but we could also use JsonVariant.is<T>(), like that:
firstIsString = array[0].is<char*>(); // <- true
secondIsFloat = array[1].is<float>(); // <- true
```

##### See also

* [`JsonVariant::is<T>()`]({{site.baseurl}}/api/jsonvariant/is/)
* [`JsonObject::is<T>()`]({{site.baseurl}}/api/jsonobject/is/)
