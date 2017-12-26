---
title: Why does my device crash or reboot?
description: "This page describes the three reason why a program could crash while using ArduinoJson"
keywords: ArduinoJson,crash,bug,reboot,exception
layout: faq
tags: faq
faq-group: Common
popularity: 187
redirect_from:
 - /faq/why-do-i-have-a-segmentation-fault/
---

## Reason 1: Null pointer dereferencing

Usually, a null pointer dereferencing happens when ArduinoJson returns a null whereas the program expects a string.

Here is an example:

```c++
char name[32];

JsonObject& obj = jsonBuffer.parseObject(input);
strlcpy(name, obj["name"], 32);
```

This program works fine, except when the value `"name"` is missing from the object, because `obj["name"]` return `NULL`.
The same thing happens if parsing fails.

Here is how to fix this program:

```c++
char name[32];

JsonObject& obj = jsonBuffer.parseObject(input);
strlcpy(name, obj["name"] | "N/A", 32);
```

This snippet uses the `|` syntax introduced in ArduinoJson 5.12.
It is equivalent to the following code:

```c++
char name[32];

JsonObject& obj = jsonBuffer.parseObject(input);

const char* jsonName = obj["name"];
if (jsonName)
  strlcpy(name, obj["name"], 32);
else
  strcpy(name, "N/A");
```

## Reason 2: Stack-overflow

A stack overflow happens when you have too many variables in the "stack" memory.

Before reading further, make sure that your target platform does have enough RAM to store the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) and possibly the JSON input too:

* Use [ArduinoJson Assistant]({{site.baseurl}}/assistant/) to see how much memory you need.
* See [How to reduce memory usage?]({{site.baseurl}}/faq/how-to-reduce-memory-usage/).
* See [Can I parse a JSON input that is too big to fit in memory?]({{site.baseurl}}/faq/can-i-parse-a-json-input-that-is-too-big-to-fit-in-memory/)

Once you're sure that your device has enough RAM, you should move the[`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) to the heap. Just replace your `StaticJsonBuffer` with a `DynamicJsonBuffer`.

If your JSON input is stored in the stack, you should move it to the heap too.

For instance, if you have a program like this:

```c++
char content[MAX_CONTENT_SIZE];
StaticJsonBuffer<JSON_BUFFER_SIZE> jsonBuffer;

receive(content);
JsonObject& root = jsonBuffer.parseObject(content);

Serial.println(root["name"].asString());
```

you should transform it like that:

```c++
char* content = malloc(MAX_CONTENT_SIZE);
DynamicJsonBuffer jsonBuffer(JSON_BUFFER_SIZE);

receive(content);
JsonObject& root = jsonBuffer.parseObject(content);

Serial.println(root["name"].asString());

free(content);
```

## Reason 3: Incompatible configurations in compilation units

If your program behaves unpredictably, it may be because a different configuration is used in each `.ino` or `.cpp` file.

For example, imagine you have two files `my_sketch.ino` and `my_lib.cpp`.

The first file starts with:

```c++
// File: my_sketch.ino
#define ARDUINOJSON_USE_LONG_LONG 1
#include <ArduinoJson.h>
```

whereas the second starts with:

```c++
// File: my_lib.ino
#define ARDUINOJSON_USE_LONG_LONG 0
#include <ArduinoJson.h>
```

In that situation, the two compilation units have different sizes for [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/).
Since the linker is not able to detect this problem, it will create an executable with some functions using a big [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/) and others using small [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/).
The executable may work under some conditions but will crash sooner or later.

To fix this bug, you must use the same configuration in all compilation units.
A simple way to do that is to share the configuration in a `.h` file.

## Where to go next?

<a href="{{ site.baseurl }}{% link book/index.md %}"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"]({{ site.baseurl }}{% link book/index.md %}) is the best material to learn how to use ArduinoJson, and it's only 15 bucks!

The chapter "Troubleshooting" explains how you can debug a program using ArduinoJson. It teaches useful techniques to fix any problem with serialization, deserialization, and crashes.

If C++ is not your strength, you will appreciate the quick C++ course which will help you catch up with pointers, references, and other subtilities.