---
title: How to reuse a <code>JsonBuffer</code>?
description: Do not reuse a JsonBuffer
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer,reuse,reset,clear
layout: faq
tags: faq
faq-group: Common
popularity: 639
---

## Disclaimer

Since ArduinoJson 5.11.0, it's possible to reuse a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) thank to the [`clear()`]({{site.baseurl}}/api/jsonbuffer/clear/) method.
However, it's very risky and can be avoided most of the time.

Please take a second to see this example:

```c++
// STEP1: parse input
StaticJsonBuffer<200> jsonBuffer;
JsonObject& inputObject = jsonBuffer.parseObject(inputJson);

...etc...

// STEP2: generate output
jsonBuffer.clear();
JsonObject& outputObject = jsonBuffer.createObject();
outputObject["hello"] = inputObject["world"];
```

The program above looks OK but causes an access violation.

An experienced C++ developer would find the error instantly, especially if she has a debugger.
But most Arduino developers are new to C++ and none of them have a debugger.

Here is what happens in this buggy program:

* `inputObject` is a pointer to an object whose memory is in [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).
* `clear()` resets the memory pool in [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), allowing to reuse the memory of `inputObject`
* `outputObject` is created at the same address as `inputObject`
* `inputObject` is now a dangling pointer and the behavior is undefined.

## How to fix this code?

To rewrite this code without `clear()`, we have two possibilities.

Suggestion 1: use a bigger [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/):

```c++
// STEP1: parse input
StaticJsonBuffer<400> jsonBuffer;
JsonObject& inputObject = jsonBuffer.parseObject(inputJson);

...etc...

// STEP2: generate output
JsonObject& outputObject = jsonBuffer.createObject();
outputObject["hello"] = inputObject["world"];
```

Suggestion 2: use a second [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/):

```c++
// STEP1: parse input
StaticJsonBuffer<200> jsonBuffer1;
JsonObject& inputObject = jsonBuffer1.parseObject(inputJson);

...etc...

// STEP2: generate output
StaticJsonBuffer<200> jsonBuffer2;
JsonObject& outputObject = jsonBuffer2.createObject();
outputObject["hello"] = inputObject["world"];
```

## What if I don't reference the memory after clearing?

You mean, like this?

```c++
void sendAll()
{
  // Create JSON buffer
  StaticJsonBuffer<100> jsonBuffer;
  
  // Create object
  JsonObject& root = jsonBuffer.createObject();
  
  // Send volume
  root[F("cmd")] = F("volume");
  root[F("volume")] = dsp.volumeData;
  root[F("slew")] = dsp.volumeSlewData;
  rs485.send(jsonAck, jsonBuffer);

  // Send mux
  // Clear or delete JSON buffer here
  root[F("cmd")] = F("mux");
  root[F("muxdata")] = dsp.muxdata;
  rs485.send(jsonAck, jsonBuffer);

  // ...
}
```

well, just split the function:

```c++
void sendAll()
{
    sendVolume();
    sendMux();
    //...
}

void sendVolume()
{
  StaticJsonBuffer<100> jsonBuffer;
  JsonObject& root = jsonBuffer.createObject();
  root[F("cmd")] = F("volume");
  root[F("volume")] = dsp.volumeData;
  root[F("slew")] = dsp.volumeSlewData;
  rs485.send(jsonAck, jsonBuffer);
}

void sendMux()
{
  StaticJsonBuffer<100> jsonBuffer;
  JsonObject& root = jsonBuffer.createObject();
  root[F("cmd")] = F("mux");
  root[F("muxdata")] = dsp.muxdata;
  rs485.send(jsonAck, jsonBuffer);
}
```

## See also

* [Avoiding pitfalls: Don't reuse the same JsonBuffer]({{site.baseurl}}/doc/pitfalls/#4-dont-reuse-the-same-jsonbuffer/)
* [FAQ: Why shouldn't I use a global `JsonBuffer`?]({{site.baseurl}}/faq/why-shouldnt-i-use-a-global-jsonbuffer/).
* [FAQ: What's the best way to use the library?]({{site.baseurl}}/faq/whats-the-best-way-to-use-the-library/)

## Where to go next?

<a href="{{ site.baseurl }}{% link book/index.md %}"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

In the [ArduinoJson ebook]({{ site.baseurl }}{% link book/index.md %}), explains extensively how `StaticJsonBuffer` and `DynamicJsonBuffer` works. Once you understand how they are made, it becomes obvious why they cannot be reused.

The book also contains a quick C++ course to catch up with pointers, references, and how they cause failures. It describes the concept of RAII (Resource Acquisition Is Initialization) which is the foundation for proper memory management in C++.
