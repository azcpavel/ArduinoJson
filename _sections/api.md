---
layout: page
title: API Reference
description: This is the reference documentation for the ArduinoJson API
keywords: ArduinoJson,api,reference
tags: api
section_tag: api
popularity: 10
---

This is the detailed documentation of every class and function of the ArduinoJson library.
Some parts have been simplified to be easier to understand, so if you look at the source code, you might see some differences.

<ul>
{% assign groups = site.apis | group_by: 'api-group' %}
{% for group in groups %}
  <li><code>{{ group.name }}</code>
    <ul>
    {% assign items = group.items | sort: 'title' %}
    {% for api in items %}
      <li><a href="{{ site.baseurl }}{{ api.url }}"><code>{{ api.title }}</code></a></li>
    {% endfor %}
    </ul>
  </li>
{% endfor %}
</ul>


## Where to go next?

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

Although it does not contain an exhaustive list of function like this page, the [ArduinoJson ebook](https://leanpub.com/arduinojson/) is a more convenient and more pleasant way to learn how to use the library.

It contains step-by-step tutorials to learn how to serialize or parse JSON with ArduinoJson. It also explains how `StaticJsonBuffer` and `DynamicJsonBuffer` work, and how to choose between them.

If C++ is not your strength, you will appreciate the quick C++ course which will help you catch up with pointers, references, and other subtilities.