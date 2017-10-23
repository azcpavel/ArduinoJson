---
title: Why some parts are missing?
description: The JSON is incomplete because the JsonBuffer is too small
keywords: ArduinoJson,incomplete,missing,empty
layout: faq
tags: faq
faq-group: Serialization
popularity: 76
---

Example: you want to write `{"p1":[0, 1]}`, but instead you get `{"p1":[]}`.

This is because the `StaticJsonBuffer` too small.

Solution: Increase the size of the `StaticJsonBuffer` or switch to a `DynamicJsonBuffer`.

The [ArduinoJson Assistant](https://bblanchon.github.io/ArduinoJson/assistant/) can compute the size for you.

See also:

* [What are the differences between StaticJsonBuffer and DynamicJsonBuffer?]({{site.baseurl}}/faq/what-are-the-differences-between-staticjsonbuffer-and-dynamicjsonbuffer)
* [How to determine the buffer size?]({{site.baseurl}}/faq/how-to-determine-the-buffer-size)
* [ArduinoJson Assistant](https://bblanchon.github.io/ArduinoJson/assistant/)
