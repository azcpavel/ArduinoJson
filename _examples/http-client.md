---
title: JsonHttpClient.ino
description: This example shows how to parse a JSON document in an HTTP response. It uses the Ethernet library, but can be easily adapted for Wifi.
keywords: ArduinoJson,HTTP,parse,decode,example
layout: example
tags: example
---

## Description

This example shows how to parse a JSON document in an HTTP response.

It uses the [Ethernet library](https://www.arduino.cc/en/Reference/Ethernet), but can be easily adapted for [Wifi](https://www.arduino.cc/en/Reference/WiFi).

It performs a GET resquest on `arduinojson.org/example.json`.

Here is the expected response:

```json
{
  "sensor": "gps",
  "time": 1351824120,
  "data": [
    48.756080,
    2.302038
  ]
}
```

## Source code

```c++
// ArduinoJson - arduinojson.org
// Copyright Benoit Blanchon 2014-2017
// MIT License

#include <ArduinoJson.h>
#include <Ethernet.h>
#include <SPI.h>

void setup() {
  // Initialize Serial port
  Serial.begin(9600);
  while (!Serial) continue;

  // Initialize Ethernet library
  byte mac[] = {0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED};
  if (!Ethernet.begin(mac)) {
    Serial.println(F("Failed to configure Ethernet"));
    return;
  }
  delay(1000);

  Serial.println(F("Connecting..."));

  // Connect to HTTP server
  EthernetClient client;
  client.setTimeout(10000);
  if (!client.connect("arduinojson.org", 80)) {
    Serial.println(F("Connection failed"));
    return;
  }

  Serial.println(F("Connected!"));

  // Send HTTP request
  client.println(F("GET /example.json HTTP/1.0"));
  client.println(F("Host: arduinojson.org"));
  client.println(F("Connection: close"));
  if (client.println() == 0) {
    Serial.println(F("Failed to send request"));
    return;
  }

  // Check HTTP status
  char status[32] = {0};
  client.readBytesUntil('\r', status, sizeof(status));
  if (strcmp(status, "HTTP/1.1 200 OK") != 0) {
    Serial.print(F("Unexpected response: "));
    Serial.println(status);
    return;
  }

  // Skip HTTP headers
  char endOfHeaders[] = "\r\n\r\n";
  if (!client.find(endOfHeaders)) {
    Serial.println(F("Invalid response"));
    return;
  }

  // Allocate JsonBuffer
  // Use arduinojson.org/assistant to compute the capacity.
  const size_t capacity = JSON_OBJECT_SIZE(3) + JSON_ARRAY_SIZE(2) + 60;
  DynamicJsonBuffer jsonBuffer(capacity);

  // Parse JSON object
  JsonObject& root = jsonBuffer.parseObject(client);
  if (!root.success()) {
    Serial.println(F("Parsing failed!"));
    return;
  }

  // Extract values
  Serial.println(F("Response:"));
  Serial.println(root["sensor"].as<char*>());
  Serial.println(root["time"].as<char*>());
  Serial.println(root["data"][0].as<char*>());
  Serial.println(root["data"][1].as<char*>());

  // Disconnect
  client.stop();
}

void loop() {
  // not used in this example
}
```

## Where to go next?

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson, and it's only 15 bucks!

The chapter "Deserialize ArduinoJson" is a tutorial on deserialization, it shows how to parse the response from [Yahoo Weather](https://developer.yahoo.com/weather/). This chapter is in the book sample, so you can download it for free!

The chapter "Case Studies" shows how to parse the huge JSON documents from [OpenWeatherMap](https://openweathermap.org/) and [Weather Underground](https://www.wunderground.com/).
