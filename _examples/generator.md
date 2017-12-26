---
title: JsonGeneratorExample.ino
description: This example shows how to generate a JSON document with the ArduinoJson library.
keywords: ArduinoJson,serialize,encode,generate,example
layout: example
tags: example
---

## Description

This example shows how to generate a JSON document with ArduinoJson.

## Source code

```c++
// ArduinoJson - arduinojson.org
// Copyright Benoit Blanchon 2014-2017
// MIT License

#include <ArduinoJson.h>

void setup() {
  // Initialize Serial port
  Serial.begin(9600);
  while (!Serial) continue;

  // Memory pool for JSON object tree.
  //
  // Inside the brackets, 200 is the size of the pool in bytes.
  // Don't forget to change this value to match your JSON document.
  // Use arduinojson.org/assistant to compute the capacity.
  StaticJsonBuffer<200> jsonBuffer;

  // StaticJsonBuffer allocates memory on the stack, it can be
  // replaced by DynamicJsonBuffer which allocates in the heap.
  //
  // DynamicJsonBuffer  jsonBuffer(200);

  // Create the root of the object tree.
  //
  // It's a reference to the JsonObject, the actual bytes are inside the
  // JsonBuffer with all the other nodes of the object tree.
  // Memory is freed when jsonBuffer goes out of scope.
  JsonObject& root = jsonBuffer.createObject();

  // Add values in the object
  //
  // Most of the time, you can rely on the implicit casts.
  // In other case, you can do root.set<long>("time", 1351824120);
  root["sensor"] = "gps";
  root["time"] = 1351824120;

  // Add a nested array.
  //
  // It's also possible to create the array separately and add it to the
  // JsonObject but it's less efficient.
  JsonArray& data = root.createNestedArray("data");
  data.add(48.756080);
  data.add(2.302038);

  root.printTo(Serial);
  // This prints:
  // {"sensor":"gps","time":1351824120,"data":[48.756080,2.302038]}

  Serial.println();

  root.prettyPrintTo(Serial);
  // This prints:
  // {
  //   "sensor": "gps",
  //   "time": 1351824120,
  //   "data": [
  //     48.756080,
  //     2.302038
  //   ]
  // }
}

void loop() {
  // not used in this example
}
```

## Classes used in this example

* [`JsonArray`]({{site.baseurl}}/api/jsonarray/)
* [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/)
* [`JsonObject`]({{site.baseurl}}/api/jsonobject/)

## Functions used in this example

* [`JsonArray::add()`]({{site.baseurl}}/api/jsonarray/add/)
* [`JsonBuffer::createObject()`]({{site.baseurl}}/api/jsonbuffer/createobject/)
* [`JsonObject::createNestedArray()`]({{site.baseurl}}/api/jsonobject/createnestedarray/)
* [`JsonObject::operator[]`]({{site.baseurl}}/api/jsonobject/subscript/)
* [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/)
* [`JsonObject::printTo()`]({{site.baseurl}}/api/jsonobject/printto/)

## Keep learning

<a href="{{ site.baseurl }}{% link book/index.md %}"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"]({{ site.baseurl }}{% link book/index.md %}) is the best material to learn how to use ArduinoJson, and it's only 15 bucks!

The chapter "Serialize with ArduinoJson" is a tutorial to learn how to generate JSON documents with the library. It begins with a simple example, like the one above, and then adds more features like serializing directly to a file or an HTTP request.