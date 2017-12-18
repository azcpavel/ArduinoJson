---
title: JsonArray
description: A JsonArray is a collection of JsonVariant; it allows getting and setting a value by its index.
keywords: ArduinoJson,JsonArray
layout: api
tags: api
api-group: class
---

##### Description

A collection of [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/)

The constructor is private, you cannot instantiate a `JsonArray` directly.
Instead, you must use  [`JsonBuffer::createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/).

Because the memory of a `JsonArray` is located a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), you always manipulate it through reference and you cannot copy it.

##### Example

```c++
StaticJsonBuffer<200> jsonBuffer;

// create an empty array
JsonArray& array1 = jsonBuffer.createArray();

// parse a JSON array
char json[] = "[1,2,3]";
JsonArray& array2 = jsonBuffer.parseArray(json);
```

##### Member functions

<ul>
{% assign methods = site.apis | where:"api-group",page.title %}
{% for method in methods %}
  <li><a href="{{ site.baseurl }}{{ method.url }}"><code>{{ method.title }}</code></a></li>
{% endfor %}
</ul>


