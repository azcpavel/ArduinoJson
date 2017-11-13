---
layout: doc
tags: doc
title: Quickstart
keywords: ArduinoJson
description: ArduinoJson in a nutshell
---

#### Decoding / Parsing

```c++   
char json[] = "{\"sensor\":\"gps\",\"time\":1351824120,\"data\":[48.756080,2.302038]}";

StaticJsonBuffer<200> jsonBuffer;

JsonObject& root = jsonBuffer.parseObject(json);

const char* sensor = root["sensor"];
long time          = root["time"];
double latitude    = root["data"][0];
double longitude   = root["data"][1];
```

[See complete guide]({{site.baseurl}}/doc/decoding/)

#### Encoding / Generating

```c++   
StaticJsonBuffer<200> jsonBuffer;

JsonObject& root = jsonBuffer.createObject();
root["sensor"] = "gps";
root["time"] = 1351824120;

JsonArray& data = root.createNestedArray("data");
data.add(48.756080);
data.add(2.302038);

root.printTo(Serial);
// This prints:
// {"sensor":"gps","time":1351824120,"data":[48.756080,2.302038]}
```

[See complete guide]({{site.baseurl}}/doc/encoding/)