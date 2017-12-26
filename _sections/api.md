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
{% assign classes = site.apis | where:"api-group","class" %}
{% for class in classes %}
  <li><a href="{{ site.baseurl }}{{ class.url }}"><code>{{ class.title }}</code></a>
    <ul>
    {% assign methods = site.apis | where:"api-group",class.title %}
    {% for method in methods %}
      <li><a href="{{ site.baseurl }}{{ method.url }}"><code>{{ method.title }}</code></a></li>
    {% endfor %}
    </ul>
  </li>
{% endfor %}
  <li>Compile time configuration
    <ul>
    {% assign methods = site.apis | where:"api-group","Configuration" %}
    {% for method in methods %}
      <li><a href="{{ site.baseurl }}{{ method.url }}"><code>{{ method.title }}</code></a></li>
    {% endfor %}
    </ul>
  </li>
</ul>

## Where to go next?

<a href="{{ site.baseurl }}{% link book/index.md %}"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

Although it does not contain an exhaustive list of function like this page, the [ArduinoJson ebook]({{ site.baseurl }}{% link book/index.md %}) is a more convenient and more pleasant way to learn how to use the library.

It contains step-by-step tutorials to learn how to serialize or parse JSON with ArduinoJson. It also explains how `StaticJsonBuffer` and `DynamicJsonBuffer` work, and how to choose between them.

If C++ is not your strength, you will appreciate the quick C++ course which will help you catch up with pointers, references, and other subtilities.