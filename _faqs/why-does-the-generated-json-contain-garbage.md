---
title: Why does the generated JSON contain garbage?
description: Garbage in the JSON is caused by a dangling pointer or reference
keywords: ArduinoJson,error,garbage,gibberish
layout: faq
tags: faq
faq-group: Serialization
popularity: 46
---

There are two key concepts you need to understand to use ArduinoJson:

1. [`JsonObject`]({{site.baseurl}}/api/jsonobject/)s and [`JsonArray`]({{site.baseurl}}/api/jsonarray/)s are stored in a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/)
2. `char*` are not copied

Similarly, there are two reasons to get garbage in the output:

1. [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is not in memory anymore
2. The string pointed by the `char*` is not in memory anymore.

#### Example 1 of what you should not do:

```c++
JsonObject& myFunction() {
  StaticJsonBuffer<200> jsonBuffer;
  return jsonBuffer.createObject();
}
```

This is wrong because it returns a reference (a pointer if you prefer) to a [`JsonObject`]({{site.baseurl}}/api/jsonobject/) that is not in memory anymore.

#### Example 2 of what you should not do:

```c++
void myFunction(JsonObject& obj) {
  char myValue[] = "Hello World!";
  obj["value"] = myValue;
}
```

This is wrong because the [`JsonObject`]({{site.baseurl}}/api/jsonobject/) now contains a pointer to a string that is not in memory anymore.

See also:

* [Avoiding pitfalls: Do not assume that strings are copied](https://github.com/bblanchon/ArduinoJson/wiki/Avoiding-pitfalls#6-do-not-assume-that-strings-are-copied)
* Issues [#364](https://github.com/bblanchon/ArduinoJson/issues/364), [#366](https://github.com/bblanchon/ArduinoJson/issues/366)
