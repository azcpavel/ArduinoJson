---
title: How to compute the JSON length?
description: To compute JSON length, call measureLength()
keywords: ArduinoJson,JSON,size,length,JsonArray,JsonObject
layout: faq
tags: faq
faq-group: Serialization
popularity: 58
---

Use [`measureLength()`]({{site.baseurl}}/api/jsonobject/measurelength/) to compute the number of characters that will be printed by [`printTo()`]({{site.baseurl}}/api/jsonobject/printto/).

Use [`measurePrettyLength()`]({{site.baseurl}}/api/jsonobject/measureprettylength/) to compute the number of characters that will be printed by [`prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/).

None of these methods includes the zero-terminator; so, if you need to allocate a buffer, don't forget to add 1 to the size.

```c++
StaticJsonBuffer<200> jsonBuffer;
JsonObject& root = jsonBuffer.createObject();
root["hello"] = world;

size_t len = root.measureLength(); // returns 17

size_t size = len+1;
char json[size];
root.printTo(json, size); // writes {"hello":"world"}
```

