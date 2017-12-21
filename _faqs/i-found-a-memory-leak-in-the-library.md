---
title: I found a memory leak in the library!
description: There is no memory leak in ArduinoJson, you are just using it improperly
keywords: ArduinoJson,leak,bug
layout: faq
tags: faq
faq-group: Common
popularity: 107
---

This is very unlikely. You're probably using the library incorrectly.

The typical problem comes from reusing a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) several time.
Each time you call [`parseArray()`]({{site.baseurl}}/api/jsonbuffer/parsearray/), [`parseObject()`]({{site.baseurl}}/api/jsonbuffer/parseobject/), [`createArray()`]({{site.baseurl}}/api/jsonbuffer/createarray/) and [`createObject()`]({{site.baseurl}}/api/jsonbuffer/createobject/), you consume memory in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).
To avoid running out of memory, you should discard unused data as soon as possible.

The recommended practice is to do the JSON handling in a dedicated function, with a local [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) that will be automatically reclaimed when the function exits.
This means that you cannot return a [`JsonArray`]({{site.baseurl}}/api/jsonarray/) or a [`JsonObject`]({{site.baseurl}}/api/jsonobject/) from that function, because they would contain dangling pointers to what used to be the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).
Instead, you should convert the content of the [`JsonArray`]({{site.baseurl}}/api/jsonarray/) to a custom array or `vector`; or the content of the [`JsonObject`]({{site.baseurl}}/api/jsonobject/) to your own data structure.

This seems like a constraint, but remember that you're programming for an embedded platform with very limited resources, and that requires special techniques.

A positive side effect of following this recommendation is that the code is safe and memory efficient. It also encourages the separation of responsibilities: the function is only in charge of the JSON serialization and no specific JSON data leaks elsewhere is the program.

See:

* [What's the best way to use the library]({{ site.baseurl }}/faq/whats-the-best-way-to-use-the-library/)
* [Why shouldn't I use a global JsonBuffer?]({{ site.baseurl }}/faq/why-shouldnt-i-use-a-global-jsonbuffer/)
* [The first parsing succeeds, why do the next ones fail?]({{ site.baseurl }}/faq/the-first-parsing-succeeds-why-do-the-next-ones-fail/)
* [ArduinoJson: Avoiding pitfalls](https://github.com/bblanchon/ArduinoJson/wiki/Avoiding%20pitfalls)
