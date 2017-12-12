---
layout: page
title: Examples
description: These are the official examples of ArduinoJson
keywords: ArduinoJson,examples
tags: example
section_tag: example
popularity: 6
---

The following examples are also available in Arduino's "Examples" menu.

<dl>
{% assign examples = site.examples | sort: 'popularity' | reverse %}
{% for example in examples %}
  <dt><a href="{{ site.baseurl }}{{ example.url }}">{{ example.title }}</a></dt>
  <dd>{{ example.description }}</dd>
{% endfor %}
</dl>

---

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The [ArduinoJson ebook](https://leanpub.com/arduinojson/) contains new examples and a complete chapter is dedicated to the study of these examples.

In particular, it teaches how ArduinoJson manages the memory and what `StaticJsonBuffer` and `DynamicJsonBuffer` are. It shows how to make the best use of the library by avoiding memory allocation and duplications.

