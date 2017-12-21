---
title: JsonObject::is&lt;T&gt;()
description: The function JsonObject::is&lt;T&gt;() tests if the value at specified key has the type T.
keywords: ArduinoJson,JsonObject,get,read
layout: api
tags: api
api-group: JsonObject
---

## Description

Tests if the value at specified key has the type `T`.

## Signature

```c++
bool is<bool>              (TString key) const;

bool is<const char*>       (TString key) const;
bool is<char*>             (TString key) const;

bool is<double>            (TString key) const;
bool is<float>             (TString key) const;

bool is<signed char>       (TString key) const;
bool is<signed int>        (TString key) const;
bool is<signed long>       (TString key) const;
bool is<signed short>      (TString key) const;
bool is<unsigned char>     (TString key) const;
bool is<unsigned int>      (TString key) const;
bool is<unsigned long>     (TString key) const;
bool is<unsigned short>    (TString key) const;
bool is<signed long long>  (TString key) const;   // <- may require ARDUINOJSON_USE_LONG_LONG
bool is<unsigned long long>(TString key) const;   // <- may require ARDUINOJSON_USE_LONG_LONG

bool is<JsonArray>         (TString key) const;
bool is<JsonObject>        (TString key) const;
```

## Arguments

`key`: the key of the value in the object, can be a:

* `const char*`,
* `String`,
* `std::string`, or
* `const __FlashStringHelper*`.

`T`: the type to test.

## Return value

* `true` if value at specified key matches the type `T`,
* `false` if not

## Remarks

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

## Example

```c++
char json[] = "{\"name\":\"toto\",\"pi\":3.14}";
StaticJsonBuffer<256> jsonBuffer;
JsonObject& obj = jsonBuffer.parseObject(json);

bool nameIsString = obj.is<char*>("name"); // <- true
bool piIsFloat = obj.is<float>("pi"); // <- true

// but we could also use JsonVariant.is<T>(), like that:
nameIsString = obj["name"].is<char*>(); // <- true
piIsFloat = obj["pi"].is<float>(); // <- true
```

## See also

* [`JsonVariant::is<T>()`]({{site.baseurl}}/api/jsonvariant/is/)
* [`JsonArray::is<T>()`]({{site.baseurl}}/api/jsonarray/is/)
* [`JsonObject::get<T>()`]({{site.baseurl}}/api/jsonobject/get/)
