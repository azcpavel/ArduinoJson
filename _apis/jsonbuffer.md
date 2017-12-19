---
title: JsonBuffer
description: DynamicJsonBuffer and StaticJsonBuffer are memory pools
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer
layout: api
tags: api
api-group: class
---

##### Description

`JsonBuffer` is the entry point for using the library: it handles the memory management and calls the parser.

It implements a speed efficient memory pool and comes in two flavors:

1. `DynamicJsonBuffer` which is allocated on the heap and grows automatically
2. `StaticJsonBuffer` which is (most likely) allocated on the stack and has a fixed size.

`JsonBuffer` is optimized of fast allocation, but doesn't allow to free the allocated memory block.
To free a `JsonBuffer`, you must discard the entire object.

##### Member functions

<ul>
{% assign methods = site.apis | where:"api-group",page.title %}
{% for method in methods %}
  <li><a href="{{ site.baseurl }}{{ method.url }}"><code>{{ method.title }}</code></a></li>
{% endfor %}
</ul>

##### See also

* [Serialization tutorial]({{site.baseurl}}/doc/encoding/)
* [Deserialization tutorial]({{site.baseurl}}/doc/decoding/)
* [How to reuse a JsonBuffer?]({{site.baseurl}}/faq/how-to-reuse-a-jsonbuffer/)
* [What are the differences between StaticJsonBuffer and DynamicJsonBuffer?]({{site.baseurl}}/faq/what-are-the-differences-between-staticjsonbuffer-and-dynamicjsonbuffer/)
* [How to determine the buffer size?]({{site.baseurl}}/faq/how-to-determine-the-buffer-size/)
* [Why shouldn't I use a global JsonBuffer?]({{site.baseurl}}/faq/why-shouldnt-i-use-a-global-jsonbuffer/)
* [What are the common sizes for JsonBuffer?]({{site.baseurl}}/faq/what-are-the-common-sizes-for-jsonbuffer/)

##### Keep learning

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson.

Chapter 5 explains how ArduinoJson works from the inside.
It explains why the class `JsonBuffer` is crucial for the performance of the library.
It dissects `StaticJsonBuffer` and `DynamicJsonBuffer`, shows the differences between the two, and tells how to choose between them.

Chapter 6 is a troubleshooting guide that helps you get out of every difficult situation.