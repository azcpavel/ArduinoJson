---
title: JsonArray::copyTo()
description: Copies a JsonArray
keywords: ArduinoJson,JsonArray,copyTo
layout: api
tags: api
api-group: JsonArray
---

## Description

Extracts a C array from the [`JsonArray`]({{site.baseurl}}/api/jsonarray/).

## Signatures

```c++
JsonArray::copyTo(int array[]);
JsonArray::copyTo(double array[]);
JsonArray::copyTo(const char* array[]);
```

## Return value

A `size_t` containing the number of values written in the array.

## Example

```c++
int values[3];

StaticJsonBuffer<200> jsonBuffer;
JsonArray& array = jsonBuffer.parseArray("[1,2,3]");
array.copyTo(values);
```

now `values` contais `1`, `2` and `3`.

## See also

* [JsonArray::copyFrom()]({{site.baseurl}}/api/jsonarray/copyfrom/)