---
title: JsonObject
description: A JsonObject is a collection of named JsonVariant; it allows getting and setting a value by its name.
keywords: ArduinoJson,JsonObject
layout: api
tags: api
api-group: class
---

## Description

A collection of named [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/).

The constructor is private, you cannot instantiate a `JsonObject` directly, you have to use a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer).

Because the memory of a `JsonObject` is located a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), you always manipulate it through reference and you cannot copy it.

## Example

```c++
StaticJsonBuffer<200> jsonBuffer;

// create an object
JsonObject& object1 = jsonBuffer.createObject();
object1["hello"] = "world";

// parse a JSON object
char json[] = "{\"hello\":\"world\"}";
JsonObject& object2 = jsonBuffer.parseObject(json);
```

## Member functions

<ul>
{% assign methods = site.apis | where:"api-group",page.title %}
{% for method in methods %}
  <li><a href="{{ site.baseurl }}{{ method.url }}"><code>{{ method.title }}</code></a></li>
{% endfor %}
</ul>

## See also

* [`JsonArray`]({{site.baseurl}}/api/jsonarray/)
* [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/)
* [Serialization tutorial]({{site.baseurl}}/doc/encoding/)
* [Deserialization tutorial]({{site.baseurl}}/doc/decoding/)

## Keep learning

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson.

Chapter 3 is a tutorial on deserialization; it explains the various ways to convert an input JSON document into a `JsonObject`.

Chapter 4 is a tutorial on serialization; it explains the various was to convert a `JsonObject` into a JSON document.

Chapter 5 explains how `JsonObject` is implemented.
