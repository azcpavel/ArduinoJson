---
title: What's the best way to use the library?
description: The best way to use ArduinoJson is to scope the usage of the library to functions dedicated to the serialization
keywords: ArduinoJson,design,patter,style,recommendation,advice
layout: faq
tags: faq
faq-group: Common
popularity: 425
---

Here is the canonical example for serializing and deserializing with ArduinoJson.

By following this example, you are making the best usage of your memory and you maintain a good software design.

```c++
struct SensorData {
   const char* name;
   int time;
   float value;
};

#define SENSORDATA_JSON_SIZE (JSON_OBJECT_SIZE(3))

bool deserialize(SensorData& data, char* json)
{
    StaticJsonBuffer<SENSORDATA_JSON_SIZE> jsonBuffer;
    JsonObject& root = jsonBuffer.parseObject(json);
    data.name = root["name"];
    data.time = root["time"];
    data.value = root["value"];
    return root.success();
}

void serialize(const SensorData& data, char* json, size_t maxSize)
{
    StaticJsonBuffer<SENSORDATA_JSON_SIZE> jsonBuffer;
    JsonObject& root = jsonBuffer.createObject();
    root["name"] = data.name;
    root["time"] = data.time;
    root["value"] = data.value;
    root.printTo(json, maxSize);
}
```

As you can see the `StaticJsonBuffer` is kept in memory as short as possible, so that the remain of your program is unaffected by the JSON serialization.

Also you can see that neither `JsonArray` nor `JsonObject` leak out of the serialization code. This maintain a good isolation and reduce the coupling with the library.

### Where to go next?

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

If you are interested in writing good code and make the best possible use of the library, be sure to check the [ArduinoJson ebook](https://leanpub.com/arduinojson/).

By understanding how the library is made, you will certainly make a better use of it. In particular, it is essential to prevent useless duplication, as time and memory is precious in an embedded environment.

The book also contains a quick C++ course to catch up with pointers, references, and memory management. Indeed, the most common source of pain with ArduinoJson is a lake of understanding of basic C++ concepts.
