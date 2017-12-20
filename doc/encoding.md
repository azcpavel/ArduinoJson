---
layout: doc
tags: doc
title: Serialization tutorial
keywords: ArduinoJson,serialize,encode,generate
description: This page teaches how to serialize a JSON document using the library ArduinoJson.
---

There are several ways to serialize a JSON document; in this tutorial, we'll only see the simplest.

Before writing any code, don't forget to include the header:

## The example

For our example, we'll consider the following JSON document:

```json
{"sensor":"gps","time":1351824120,"data":[48.756080,2.302038]}
```

## The steps

### 1. Include ArduinoJson

Before writing any code, don't forget to include the header:

```c++
#include <ArduinoJson.h>
```

### 2. Allocate a JsonBuffer

ArduinoJson uses a memory pool, the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), to perform all memory allocations.

In this tutorial, we create a 200-byte pool in the stack, with the following statement:

```c++
StaticJsonBuffer<200> jsonBuffer;
```

You can learn more on this topic in the page ["ArduinoJson memory model"]({{ site.baseurl }}/doc/memory/).

### 3. Create object tree in memory

We'll now create an in-memory representation of the JSON document.

The document contains a JSON object as its root, so we start by creating a [`JsonObject`]({{site.baseurl}}/api/jsonobject/). We do that by calling [`JsonBuffer::createObject()`]({{site.baseurl}}/api/jsonbuffer/createobject/)

```c++
JsonObject& root = jsonBuffer.createObject();
```

It's important to understand that the [`JsonObject`]({{site.baseurl}}/api/jsonobject/) resides in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) and will be destructed with it.

Now we can add values to the root object:

```c++
root["sensor"] = "gps";
root["time"] = 1351824120;
```

To create the nested array "data", we need to call [`JsonObject::createNestedArray()`]({{site.baseurl}}/api/jsonobject/createnestedarray/):

```c++
JsonArray& data = root.createNestedArray("data");
```

To add the values in the array, we need to call [`JsonArray::add()`]({{site.baseurl}}/api/jsonarray/add/):

```c++
data.add(48.756080);
data.add(2.302038);
```

### 4. Serialize the document

Now that we have an in-memory representation of the JSON document, we can to convert it into a string; this step is called "serialization".

To serialize a [`JsonObject`]({{site.baseurl}}/api/jsonobject/), we just need to call [`JsonObject::printTo()`]({{site.baseurl}}/api/jsonobject/printto/) and specify the destination.

For example, we can send the JSON document to the serial port:

```c++
root.printTo(Serial);
```

The statement above produces a minified JSON document.

To produce a prettified JSON document, we need to call [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/):

```c++
root.prettyPrintTo(Serial);
```

## Complete source code

```c++
// Step 1
#include <ArduinoJson.h>

void setup() {
  Serial.begin(9600);
  while (!Serial) continue;

  // Step 2
  StaticJsonBuffer<200> jsonBuffer;

  // Step 3
  JsonObject& root = jsonBuffer.createObject();
  root["sensor"] = "gps";
  root["time"] = 1351824120;
  JsonArray& data = root.createNestedArray("data");
  data.add(48.756080);
  data.add(2.302038);

  // Step 4
  root.printTo(Serial);
  Serial.println();
  root.prettyPrintTo(Serial);
}

void loop() {}
```

## See also

* [JsonGeneratorExample.ino]({{site.baseurl}}/example/generator/) is the example described in this tutorial.
* [JsonServer.ino]({{site.baseurl}}/example/http-server/) sends the JSON document in an HTTP response.
* [JsonUdpBeacon.ino]({{site.baseurl}}/example/udp-beacon/) sends the JSON document in a UDP datagram.
* [JsonConfigFile.ino]({{site.baseurl}}/example/config/) saves the JSON document on an SD card.

## Keep learning

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

This tutorial was only a quickstart introduction to the library. For a complete course on ArduinoJson, I strongly recommend reading the book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/).

Chapter 4 is a much longer tutorial on serialization. It starts with a simple example, like this one, but then gradually adds complexity to show all the features of the library. At the end of the chapter, we see how to upload measured data to Adafruit IO.

Chapter 2 is a quick C++ course to catch up with concepts like stack and heap memory, pointer, reference... I know from experience that new users of ArduinoJson have more difficulties with the language than with the library; that's why the book starts with this course.

If you want to see what's more in ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/), please check out the Table of Content.