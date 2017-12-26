---
title: StringExample.ino
description: "This example shows the different ways you can use String objects with ArduinoJson."
keywords: ArduinoJson,string,example
tags: example
layout: example
---

## Description

This example shows the different ways you can use `String` with ArduinoJson.

Use `String` objects sparingly, because ArduinoJson duplicates them in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/). Prefer plain old `char[]`, as they are more efficient in term of code size, speed, and memory usage.

## Source code

```c++
// ArduinoJson - arduinojson.org
// Copyright Benoit Blanchon 2014-2017
// MIT License

#include <ArduinoJson.h>

void setup() {
  DynamicJsonBuffer jsonBuffer;

  // You can use a String as your JSON input.
  // WARNING: the content of the String will be duplicated in the JsonBuffer.
  String input =
      "{\"sensor\":\"gps\",\"time\":1351824120,\"data\":[48.756080,2.302038]}";
  JsonObject& root = jsonBuffer.parseObject(input);

  // You can use a String to get an element of a JsonObject
  // No duplication is done.
  long time = root[String("time")];

  // You can use a String to set an element of a JsonObject
  // WARNING: the content of the String will be duplicated in the JsonBuffer.
  root[String("time")] = time;

  // You can get a String from a JsonObject or JsonArray:
  // No duplication is done, at least not in the JsonBuffer.
  String sensor = root["sensor"];

  // Unfortunately, the following doesn't work (issue #118):
  // sensor = root["sensor"]; // <-  error "ambiguous overload for 'operator='"
  // As a workaround, you need to replace by:
  sensor = root["sensor"].as<String>();

  // You can set a String to a JsonObject or JsonArray:
  // WARNING: the content of the String will be duplicated in the JsonBuffer.
  root["sensor"] = sensor;

  // You can also concatenate strings
  // WARNING: the content of the String will be duplicated in the JsonBuffer.
  root[String("sen") + "sor"] = String("gp") + "s";

  // You can compare the content of a JsonObject with a String
  if (root["sensor"] == sensor) {
    // ...
  }

  // Lastly, you can print the resulting JSON to a String
  String output;
  root.printTo(output);
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