---
title: JsonVariant
description: A JsonVariant can hold any JSON value; it can be a string, a number, a boolean, an array or an object.
keywords: ArduinoJson,JsonVariant
layout: api
tags: api
api-group: class
---

## Description

A variable that can hold different type of values:

* a boolean
* a char, short, int or a long (signed or unsigned)
* a string (const char*)
* a reference to a JsonArray or JsonObject

A `JsonVariant` can be any of theses types at a time, but can only hold one value.
Its type can change at run time.

## Member functions

<ul>
{% assign methods = site.apis | where:"api-group",page.title %}
{% for method in methods %}
  <li><a href="{{ site.baseurl }}{{ method.url }}"><code>{{ method.title }}</code></a></li>
{% endfor %}
</ul>

## See also

* [`JsonArray`]({{site.baseurl}}/api/jsonarray/)
* [`JsonObject`]({{site.baseurl}}/api/jsonobject/)

## Keep learning

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson.

Chapter 5 explains how ArduinoJson works from the inside.
For example, it dissects the class `JsonVariant` and explains how it works.

Chapter 7 presents new sample project and explains how they work.
For example, the project "Recursive Analyzer" extracts the content of a `JsonVariant` recursively, i.e., it retrieves the content of all its children.