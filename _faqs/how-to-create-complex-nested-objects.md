---
title: How to create complex nested objects?
description: To create complex objects, call createNestedArray() and createNestedObject()
keywords: ArduinoJson,createNestedArray,createNestedObject,JsonArray,JsonObject
layout: faq
tags: faq
faq-group: Serialization
popularity: 211
---

To create a nested object, call `createNestedObject()`.
To create a nested array, call `createNestedArray()`.

For example:

```c++
DynamicJsonBuffer jsonBuffer;
JsonObject& root = jsonBuffer.createObject();

JsonObject& weather = root.createNestedObject("weather");
weather["temperature"] = 12;
weather["condition"] = "cloudy";

JsonArray& coords = root.createNestedArray("coords");
coords.add(48.7507371, 7);
coords.add(2.2625587, 7);

root.prettyPrintTo(Serial);
```

will generate:

```json
{
  "weather": {
    "temperature": 12,
    "condition": "cloudy"
  },
  "coords": [
    48.7507371,
    2.2625587
  ]
}
```

The [ArduinoJson Assistant]({{site.baseurl}}/assistant/) can generate the skeleton for you.

See:

* [API Reference: JsonArray::createNestedArray()]({{site.baseurl}}/api/jsonarray/createnestedarray)
* [API Reference: JsonArray::createNestedArray()]({{site.baseurl}}/api/jsonarray/createnestedarray)
* [API Reference: JsonObject::createNestedArray()]({{site.baseurl}}/api/jsonobject/createnestedarray)
* [API Reference: JsonObject::createNestedObject()]({{site.baseurl}}/api/jsonobject/createnestedobject)
* [ArduinoJson Assistant]({{site.baseurl}}/assistant/)
