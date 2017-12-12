---
title: JsonVariant::is&lt;T&gt;()
description: The function JsonVariant::is&lt;T&gt;() tests if the value has the type T.
keywords: ArduinoJson,JsonVariant,is,cast,type
layout: api
tags: api
api-group: JsonVariant
---

##### Description

Tests if the variant is currently holding a value of type `T`.

##### Signatures

```c++
bool is<bool>() const;

bool is<float>() const;
bool is<double>() const;

bool is<signed char>() const;
bool is<unsigned char>() const;
bool is<signed int>() const;
bool is<unsigned int>() const;
bool is<signed short>() const;
bool is<unsigned short>() const;
bool is<signed long>() const;
bool is<unsigned long>() const;
bool is<signed long long>() const;     // <- may require ARDUINOJSON_USE_LONG_LONG
bool is<unsigned long long>() const;   // <- may require ARDUINOJSON_USE_LONG_LONG

bool is<char*>() const;
bool is<const char*>() const;

bool is<JsonArray>() const;
bool is<JsonObject>() const;
```

##### Return value

* `true` if the variant is currently holding a value of type `T`,
* `false` if not

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
JsonVariant variant = 42;
bool i = variant.is<int>(); // <- i == true
bool d = variant.is<double>(); // <- d == false
bool s = variant.is<char*>(); // <- s == false
```

##### See also

* [`JsonVariant::as<T>()`]({{site.baseurl}}/api/jsonvariant/as/)
* [`JsonArray::is<T>()`]({{site.baseurl}}/api/jsonarray/is/)
* [`JsonObject::is<T>()`]({{site.baseurl}}/api/jsonobject/is/)