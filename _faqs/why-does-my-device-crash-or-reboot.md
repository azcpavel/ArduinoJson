---
title: Why does my device crash or reboot?
description: "The two main reasons for a program to crash are: a stack-overflow or a null pointer dereferencing."
keywords: ArduinoJson,crash,bug,reboot,exception
layout: faq
tags: faq
faq-group: Common
popularity: 187
redirect_from:
 - /faq/why-do-i-have-a-segmentation-fault/
---

The two main reasons for a program to crash are: a stack-overflow or a null pointer dereferencing.

### Stack-overflow

A stack overflow happens when you have too many variables in the "stack" memory.

Before reading further, make sure that your target platform does have enough RAM to store the `JsonBuffer` and possibly the JSON input too:

* Use [ArduinoJson Assistant]({{site.baseurl}}/assistant/) to see how much memory you need.
* See [How to reduce memory usage?]({{site.baseurl}}/faq/how-to-reduce-memory-usage/).
* See [Can I parse a JSON input that is too big to fit in memory?]({{site.baseurl}}/faq/can-i-parse-a-json-input-that-is-too-big-to-fit-in-memory/)

Once you're sure that your device has enough RAM, you should move the`JsonBuffer`
to the heap. Just replace your `StaticJsonBuffer` with a `DynamicJsonBuffer`.

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

### Null pointer dereferencing

Usually, a null pointer dereferencing happens when ArduinoJson returns a null
whereas the program expects a string.

Here is an example:

```c++
char name[32];

JsonObject& obj = jsonBuffer.parseObject(input);
strlcpy(name, obj["name"], 32);
```

This program works fine, except when the value `"name"` is missing from the
object, because `obj["name"]` return `NULL`.
The same thing happens if parsing fails.

Here is how to fix this program:

```c++
char name[32];

JsonObject& obj = jsonBuffer.parseObject(input);

const char* jsonName = obj["name"];
if (jsonName)
  strlcpy(name, obj["name"], 32);
else
  strcpy(name, "N/A");
```

If you use the `master` branch of ArduinoJson, you can simplify to:

```c++
char name[32];

JsonObject& obj = jsonBuffer.parseObject(input);
strlcpy(name, obj["name"] | "N/A", 32);
```

This new feature should be available in v5.12.