---
title: JsonArray
description: A JsonArray is a collection of JsonVariant; it allows getting and setting a value by its index.
keywords: ArduinoJson,JsonArray
layout: api
tags: api
api-group: class
---

## Description

A collection of [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/)

The constructor is private, you cannot instantiate a [`JsonArray`]({{site.baseurl}}/api/jsonarray/) directly.
Instead, you must use  [`JsonBuffer::createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/).

Because the memory of a [`JsonArray`]({{site.baseurl}}/api/jsonarray/) is located a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), you always manipulate it through reference and you cannot copy it.

## Example

```c++
StaticJsonBuffer<200> jsonBuffer;

// create an empty array
JsonArray& array1 = jsonBuffer.createArray();

// parse a JSON array
char json[] = "[1,2,3]";
JsonArray& array2 = jsonBuffer.parseArray(json);
```

## Member functions

<ul>
{% assign methods = site.apis | where:"api-group",page.title %}
{% for method in methods %}
  <li><a href="{{ site.baseurl }}{{ method.url }}"><code>{{ method.title }}</code></a></li>
{% endfor %}
</ul>

## See also

* [`JsonObject`]({{site.baseurl}}/api/jsonobject/)
* [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/)
* [Serialization tutorial]({{site.baseurl}}/doc/encoding/)
* [Deserialization tutorial]({{site.baseurl}}/doc/decoding/)

## Keep learning

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson.

Chapter 3 is a tutorial on deserialization; it explains the various ways to convert an input JSON document into a [`JsonArray`]({{site.baseurl}}/api/jsonarray/).

Chapter 4 is a tutorial on serialization; it explains the various was to convert a [`JsonArray`]({{site.baseurl}}/api/jsonarray/) into a JSON document.

Chapter 5 explains how [`JsonArray`]({{site.baseurl}}/api/jsonarray/) is implemented.

