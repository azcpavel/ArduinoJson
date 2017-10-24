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

<a href="https://ebook.benoitblanchon.fr/"><img src="https://ebook.benoitblanchon.fr/cover200.png" class="float-right"></a>

The [ArduinoJson ebook](https://ebook.benoitblanchon.fr/) contains an in-depth analysis of these examples. It is a more convenient and more pleasant way to learn how to use the library.

In particular, it teaches how ArduinoJson manages the memory and what `StaticJsonBuffer` and `DynamicJsonBuffer` are. It shows how to make the best use of the library by avoiding memory allocation and duplications.

