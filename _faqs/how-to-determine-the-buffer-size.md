---
title: How to determine the buffer size?
description: The AduinoJson Assistant will compute the right expression
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,size
layout: faq
tags: faq
faq-group: Common
popularity: 296
---

There are basically tree approaches here:

1. either you can predict the content of the object tree,
2. you know how much memory is available.
3. you simply use the [ArduinoJson Assistant]({{ site.baseurl }}/assistant/)

In the first case, you know some constraints on the object tree. For instance, let's say that you know in advance (and by that I mean "at compilation time") that you want to generate an object with 3 values, one of them being an array with 2 values, like the following:

    {"sensor":"gps","time":1351824120,"data":[48.756080,2.302038]}

To determine the memory usage of this object tree, you use the two macros `JSON_ARRAY_SIZE(n)` and `JSON_OBJECT_SIZE(n)`, both take the number of elements as an argument.
For the example above, it would be:

    const int BUFFER_SIZE = JSON_OBJECT_SIZE(3) + JSON_ARRAY_SIZE(2);
    StaticJsonBuffer<BUFFER_SIZE> jsonBuffer;

In the second case, let's say you dynamically generate a JSON object tree of a random complexity so you can't put a limit based on that. But on the other hand, you don't want your program to crash because the object tree doesn't fit in memory.
The solution here is to determine how much memory is available, or in other words how much memory you can afford for the JSON object tree.

The third solution is to paste your JSON in the [ArduinoJson Assistant]({{ site.baseurl }}/assistant/) and it will return the buffer size.

**WARNING 1**: if you pass a `String` or a `const char*` to `parseArray()` or `parseObject`, the `JsonBuffer` will make a copy of the input, so it will need to be significantly bigger.

**WARNING 2**: if you use `String` to create your JSON keys or values, their content will automatically be duplicated in the `JsonBuffer`, so you need to add the total length of all strings in the size of the `JsonBuffer`.

## Where to go next?

<a href="https://ebook.benoitblanchon.fr/"><img src="https://ebook.benoitblanchon.fr/cover200.png" class="float-right"></a>

The [ArduinoJson ebook](https://ebook.benoitblanchon.fr/) details how `JsonArray` and `JsonObject` are represented in memory, and therefore how the computation of the size is done.

The book has an entire chapter for `StaticJsonBuffer` and `DynamicJsonBuffer`. It explains how they differ and how to choose between one and the other.

It also explains the difference between "stack," "heap" and "global" memories. Understanding these concepts is crucial to the success of any deeply embedded project.