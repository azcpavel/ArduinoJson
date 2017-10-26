---
title: How to determine the buffer size?
description: The AduinoJson Assistant will compute the right expression
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,size
layout: faq
tags: faq
faq-group: Common
popularity: 296
date: 2017-10-26
---

There are basically two radically different approaches:

1. compute the buffer size from the input layout
2. use whatever amount of memory is available.

## Compute the buffer size from the input layout

In this situation, we assume that you know what kind of input you want to parse.
From that, we can predict how the JSON will be stored in memory and therefore compute the required space.

For instance, let's say that you know in advance (and by that I mean "at compilation time") that you want to generate an object with 3 values, one of them being an array with 2 values, like the following:

    {"sensor":"gps","time":1351824120,"data":[48.756080,2.302038]}

To determine the memory usage of this object tree, you use the two macros `JSON_ARRAY_SIZE(n)` and `JSON_OBJECT_SIZE(n)`, both take the number of elements as an argument.
For the example above, it would be:

    const int BUFFER_SIZE = JSON_OBJECT_SIZE(3) + JSON_ARRAY_SIZE(2);
    StaticJsonBuffer<BUFFER_SIZE> jsonBuffer;

This is really cumbersome and error prone, that's why there is a tool for that: the [ArduinoJson Assistant]({{ site.baseurl }}/assistant/).
Simply a sample JSON in the [ArduinoJson Assistant]({{ site.baseurl }}/assistant/) and it will return the buffer size.

>### String duplication
>
> Depending on the type of the input, the parser uses a different strategy concerning string.
>
> If the input is mutable (ie a `char*` or a `char[]`), the parser assumes that the input buffer is persistent.<br>
> In that case, it stores pointers to the string in the input.<br>
> This is the "zero-copy" mode.
>
> On the other hand, if the input is read-only (ie a `const char*`, a `String` or a `Stream`), the parse assumes that the input is volatile.<br>
> In that case, it makes copies of the strings in the `JsonBuffer`.<br>
> This obviously has an impact on the size of the `JsonBuffer`<br>
> The string duplication also happens when you construct use `String` while constructing a `JsonObject` (either as a key or as value).
>
> So don't forget to take this into consideration when you compute the `JsonBuffer` size.<br>
> The [ArduinoJson Assistant]({{ site.baseurl }}/assistant/) shows how much extra bytes are required for the string duplications.
{: .alert .alert-danger}

## Use whatever amount of memory is available.

In the second case, let's say you dynamically generate a JSON object tree of a random complexity so you can't put a limit based on that.
But on the other hand, you don't want your program to crash because the object tree doesn't fit in memory.
The solution here is to determine how much memory is available, or in other words how much memory you can afford for the JSON object tree.

## Where to go next?

<a href="https://ebook.benoitblanchon.fr/"><img src="https://ebook.benoitblanchon.fr/cover200.png" class="float-right"></a>

The [ArduinoJson ebook](https://ebook.benoitblanchon.fr/) details how `JsonArray` and `JsonObject` are represented in memory, and therefore how the computation of the size is done.

The book has an entire chapter for `StaticJsonBuffer` and `DynamicJsonBuffer`. It explains how they differ and how to choose between one and the other.

It also explains the difference between "stack," "heap" and "global" memories. Understanding these concepts is crucial to the success of any deeply embedded project.