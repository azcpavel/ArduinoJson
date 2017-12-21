---
title: Why shouldn't I use a global <code>JsonBuffer</code>?
description: A JsonBuffer should not be reused. A global JsonBuffer wastes memory.
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,global
layout: faq
tags: faq
faq-group: Common
popularity: 244
---

## Why shouldn't I use a global <code>JsonBuffer</code>?

`StaticJsonBuffer` and `DynamicJsonBuffer` are ultra-fast memory pools.
But the drawback is that they are throwaways; they are not intended to be reused.
They can allocate memory, but not to release it; they always grow, but they never shrink.
The only way to release the memory is to destroy the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).

That's why using a global [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is always a bad idea!

## Why such a terrible limitation?

ArduinoJson is designed to do one thing and to do it well: **the JSON serialization**.
So before trying to use a global [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), ask yourself first:
*"Am I using ArduinoJson for serialization, or am I pushing it beyond its initial intent?"*

In particular, you should not use `JsonObject` and `JsonArray` to store the internal state of your program as this would be terribly inefficient. Instead, write your own data structure and use ArduinoJson only in serialization functions, as shown in [What's the best way to use the library?]({{site.baseurl}}/faq/whats-the-best-way-to-use-the-library/)

## The "global JsonObject configuration" anti-pattern

Many projects use a JSON file to store their configuration: the file is read at startup, and the content is kept in memory during the execution of the program.

In that situation, it's tempting to use a global `JsonObject` attached to a global [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).
In theory, it's OK to use a global read-only `JsonObject`, because the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) won't grow.
But in practice, it's a huge waste of memory and processor time.
The best way to deal with this is to use custom data structures as suggested in [What's the best way to use the library?]({{site.baseurl}}/faq/whats-the-best-way-to-use-the-library/).

This is a win on four levels:
1. Faster code (the object tree is walked only once at boot time)
2. Smaller RAM footprint (`JsonObject`, `JsonVariant`... have significant overhead)
3. Smaller code
4. It decouples the memory representation from the file format, which will be very handy when the file format evolves

Reducing the size of global variables is crucial as they reduce the RAM remaining for the rest.
Moreover, the JSON object tree consumes memory even if the program doesn't use it.
For example, if someone adds values in the JSON settings that are not actually used by the program, the memory will be used anyway.
One could even get to a situation where the program is unable to run because all the memory will be consumed by the settings.

## The `.data` segment anti-pattern

One might think that a legitimate usage of a global buffer is to have a `StaticJsonBuffer` in the `.data` segment so that the compiler will issue an error if there is not enough memory.

While this seems like a good idea, it wastes a lot of RAM as it reserves memory that is used only a fraction of the time.

## Where to go next?

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The [ArduinoJson ebook](https://leanpub.com/arduinojson/) explains the compromises made to allow JSON serialization in deeply embedded systems.

There is an entire chapter dedicated to `StaticJsonBuffer` and `DynamicJsonBuffer`.
It explains why they behave that way and why it doesn't make sense to reuse it.

The "Case Studies" chapter contains an example of a global configuration object stored in a file.
As you'll see, no global [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is required.

The book begins with a quick C++ course as the global [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) obsession is mostly attributed to developers used to other programming languages and paradigms.

