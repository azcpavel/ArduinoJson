---
title: ProgmemExample.ino
description: This example shows the different ways you can use Flash strings with ArduinoJson.
keywords: ArduinoJson,PROGMEM,Flash,example
tags: example
layout: example
---

## Description

This example shows the different ways you can use Flash strings with ArduinoJson.

Use Flash strings sparingly, because ArduinoJson duplicates them in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).
Prefer plain old `char*`, as they are more efficient in term of code size, speed, and memory usage.

## Source code

```c++
// ArduinoJson - arduinojson.org
// Copyright Benoit Blanchon 2014-2017
// MIT License

#include <ArduinoJson.h>

void setup() {
  DynamicJsonBuffer jsonBuffer;

  // You can use a Flash String as your JSON input.
  // WARNING: the content of the Flash String will be duplicated in the
  // JsonBuffer.
  JsonObject& root =
      jsonBuffer.parseObject(F("{\"sensor\":\"gps\",\"time\":1351824120,"
                               "\"data\":[48.756080,2.302038]}"));

  // You can use a Flash String to get an element of a JsonObject
  // No duplication is done.
  long time = root[F("time")];

  // You can use a Flash String to set an element of a JsonObject
  // WARNING: the content of the Flash String will be duplicated in the
  // JsonBuffer.
  root[F("time")] = time;

  // You can set a Flash String to a JsonObject or JsonArray:
  // WARNING: the content of the Flash String will be duplicated in the
  // JsonBuffer.
  root["sensor"] = F("gps");

  // You can compare the content of a JsonVariant to a Flash String
  if (root["sensor"] == F("gps")) {
    // ...
  }
}

void loop() {
  // not used in this example
}

```

## Classes used in this example

* [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/)
* [`JsonObject`]({{site.baseurl}}/api/jsonobject/)

## Functions used in this example

* [`JsonBuffer::parseObject()`]({{site.baseurl}}/api/jsonbuffer/parseobject/)
* [`JsonObject::operator[]`]({{site.baseurl}}/api/jsonobject/subscript/)

## Keep learning

<a href="{{ site.baseurl }}{% link book/index.md %}"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"]({{ site.baseurl }}{% link book/index.md %}) is the best material to learn how to use ArduinoJson, and it's only 15 bucks!

It begins with a quick C++ course that explains how your microcontroller stores strings in memory, so you can perfectly understand what happens behind the scenes.

The chapter "Inside ArduinoJson" explains what a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is and why it is essential for the performance of the library. This chapter also describes how `StaticJsonBuffer` and `DynamicJsonBuffer` work, and how to choose between them.