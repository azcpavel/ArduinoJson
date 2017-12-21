---
title: The first parsing succeeds, why do the next ones fail?
description: If your program works for one or more iterations but then fails, it's probably because the same JsonBuffer is used multiple time.
keywords: ArduinoJson,JsonBuffer
layout: faq
tags: faq
faq-group: Deserialization
popularity: 216
---

You wrote a program that works fine for one or more iterations, but then fails?

## Cause 1: reuse of [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/)

First, this can happen if you reuse the same [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), for example:

```c++
StaticJsonBuffer<200> jsonBuffer;

for (int i=0; i<10; i++) {
    char json[256];
    readJsonFromSomewhere(json, sizeof(json));

    JsonObject& root = jsonBuffer.parse(json);
    if (root.success()) {
       Serial.println("parseObject() succeeded");
    } else {
       Serial.println("parseObject() failed!");
    }
}
```

The solution is simply to NOT reuse the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), like this:

```c++
for (int i=0; i<10; i++) {
    char json[256];
    readJsonFromSomewhere(json, sizeof(json));

    StaticJsonBuffer<200> jsonBuffer;

    JsonObject& root = jsonBuffer.parse(json);
    if (root.success()) {
       Serial.println("parseObject() succeeded");
    } else {
       Serial.println("parseObject() failed!");
    }
}
```

Note that, contrary to common belief, moving a `StaticJsonBuffer` inside of a loop has no negative impact on performance.

## Cause 2: reuse of JSON input

This second case only concerns the "zero-copy" mode.
This mode is selected when the input is writable (`char[]` or a `char*`).
In this mode, ArduinoJson modifies the input string in place: it inserts null terminators and unescapes special characters.
If you call `parseObject()` twice with the same input buffer, the first will work, but the second will fail because the input buffer doesn't contain a valid JSON document anymore.

Here is a program that has this problem:

```c++
char json[256];
readJsonFromSomewhere(json, sizeof(json));

for (int i=0; i<10; i++) {
    StaticJsonBuffer<200> jsonBuffer;

    JsonObject& root = jsonBuffer.parse(json);
    if (root.success()) {
       Serial.println("parseObject() succeeded");
    } else {
       Serial.println("parseObject() failed!");
    }
}
```

The solution is simply to parse the input only once, or get a fresh input at each iteration:

```c++
for (int i=0; i<10; i++) {
    char json[256];
    readJsonFromSomewhere(json, sizeof(json));

    StaticJsonBuffer<200> jsonBuffer;

    JsonObject& root = jsonBuffer.parse(json);
    if (root.success()) {
       Serial.println("parseObject() succeeded");
    } else {
       Serial.println("parseObject() failed!");
    }
}
```

## Where to go next?

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson.

It begins with a quick C++ course as reusing a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is often requested by developers who are not familiar with C++. This chapter is called "The missing C++ course", because it covers topics that are skipped by other books: heap, stack, globals, RAII...

The "Case Studies" chapter dissects sample projects that use the best practices. You'll see that reusing a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is not required.

The chapter "Inside ArduinoJson", explains how `StaticJsonBuffer` and `DynamicJsonBuffer` are implemented. Once you know how they work, you will understand why they cannot be reused.
