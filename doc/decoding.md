---
layout: doc
tags: doc
title: Deserialization tutorial
keywords: ArduinoJson,parse,decode
description: This page teaches how to deserialize a JSON document using the library ArduinoJson.
---

There are several ways to deserialize a JSON document; in this tutorial, we'll only see the simplest.

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

### 2. Place the JSON document in memory

In this tutorial, we use ArduinoJson in the zero-copy mode, so the input must be writable.

We'll place the document in stack memory with the following statement:

```c++
char json[] = "{\"sensor\":\"gps\",\"time\":1351824120,\"data\":[48.756080,2.302038]}";
```

### 3. Allocate a JsonBuffer

ArduinoJson uses a memory pool, the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), to perform all memory allocations.

In this tutorial, we create a 200-byte pool in the stack, with the following statement:

```c++
StaticJsonBuffer<200> jsonBuffer;
```

You can learn more on this topic in the page ["ArduinoJson memory model"]({{ site.baseurl }}/doc/memory/).

### 4. Deserialize the JSON document

To deserialize a JSON object, you need to call [`JsonBuffer::parseObject()`]({{site.baseurl}}/api/jsonbuffer/parseobject/). This function takes the JSON document as input and returns a reference to a [`JsonObject`]({{site.baseurl}}/api/jsonobject/).

```c++
JsonObject& root = jsonBuffer.parseObject(json);
```

It's important to understand that the [`JsonObject`]({{site.baseurl}}/api/jsonobject/) resides in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) and will be destructed with it.

### 5. Check if deserialization succeeded

To check if the parsing was successful, you call [`JsonObject::success()`]({{site.baseurl}}/api/jsonobject/success/):

```c++
if (!root.success()) {
  // Parsing failed :-(
}
```

There are only a few reasons why parsing can fail; please read [Why parsing fails?]({{site.baseurl}}/faq/why-parsing-fails/).

### 6. Retrieve the values

[`JsonObject`]({{site.baseurl}}/api/jsonobject/) provides an in-memory representation of the JSON document; you can use it to extract values from the document.

In most case, you can simply use [`JsonObject::operator[]`]({{site.baseurl}}/api/jsonobject/subscript/):

```c++
const char* sensor = root["sensor"];
long time = root["time"];
double latitude  = root["data"][0];
double longitude = root["data"][1];
```

However, if the same array is used many times, it's faster to extract a reference to the [`JsonArray`]({{site.baseurl}}/api/jsonarray/):

```c++
JsonArray& data = root["data"];
double latitude  = data[0];
double longitude = data[1];
```

## Complete source code

```c++
// Step 1
#include <ArduinoJson.h>

void setup() {
  Serial.begin(9600);
  while (!Serial) continue;

  // Step 2
  char json[] =
      "{\"sensor\":\"gps\",\"time\":1351824120,\"data\":[48.756080,2.302038]}";

  // Step 3
  StaticJsonBuffer<200> jsonBuffer;

  // Step 4
  JsonObject& root = jsonBuffer.parseObject(json);

  // Step 5
  if (!root.success()) {
    Serial.println("parseObject() failed");
    return;
  }

  // Step 6
  const char* sensor = root["sensor"];
  long time = root["time"];
  double latitude = root["data"][0];
  double longitude = root["data"][1];

  Serial.println(sensor);
  Serial.println(time);
  Serial.println(latitude, 6);
  Serial.println(longitude, 6);
}

void loop() {}
```

## See also

* [JsonParserExample.ino]({{site.baseurl}}/example/parser/) is the example described in this tutorial.
* [JsonHttpClient.ino]({{site.baseurl}}/example/http-client/) deserialize the JSON document from an HTTP response.
* [JsonConfigFile.ino]({{site.baseurl}}/example/config/) loads the JSON document on an SD card.

## Keep learning

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

This tutorial was only a quickstart introduction to the library. For a complete course on ArduinoJson, I strongly recommend reading the book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/).

Chapter 3 is a much longer tutorial on deserialization. It starts with a simple example, like this one, but then gradually adds complexity to show all the features of the library. At the end of the chapter, we see how to download weather forecast from Yahoo Weather.

Chapter 2 is a quick C++ course to catch up with concepts like stack and heap memory, pointer, reference... I know from experience that new users of ArduinoJson have more difficulties with the language than with the library; that's why the book starts with this course.

If you want to see what's more in ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/), please check out the Table of Content.