---
title: JsonServer.ino
description: This example shows how to implement an HTTP server that sends JSON document in the responses.
keywords: ArduinoJson,HTTP,serialize,encode,generate,example
tags: example
layout: example
---

### Description

This example shows how to implement an HTTP server that sends JSON document in the responses.

It uses the [Ethernet library](https://www.arduino.cc/en/Reference/Ethernet), but can be easily adapted for [Wifi](https://www.arduino.cc/en/Reference/WiFi).

It sends the value of the analog and digital pins.
The JSON document looks like the following:

```json
{
  "analog": [ 0, 1, 2, 3, 4, 5 ],
  "digital": [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13 ]
}
```

### Source code

```c++
// ArduinoJson - arduinojson.org
// Copyright Benoit Blanchon 2014-2017
// MIT License

#include <ArduinoJson.h>
#include <Ethernet.h>
#include <SPI.h>

byte mac[] = {0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED};
EthernetServer server(80);

void setup() {
  // Initialize serial port
  Serial.begin(9600);
  while (!Serial) continue;

  // Initialize Ethernet libary
  if (!Ethernet.begin(mac)) {
    Serial.println(F("Failed to initialize Ethernet library"));
    return;
  }

  // Start to listen
  server.begin();

  Serial.println(F("Server is ready."));
  Serial.print(F("Please connect to http://"));
  Serial.println(Ethernet.localIP());
}

void loop() {
  // Wait for an incomming connection
  EthernetClient client = server.available();

  // Do we have a client?
  if (!client) return;

  Serial.println(F("New client"));

  // Read the request (we ignore the content in this example)
  while (client.available()) client.read();

  // Allocate JsonBuffer
  // Use arduinojson.org/assistant to compute the capacity.
  StaticJsonBuffer<500> jsonBuffer;

  // Create the root object
  JsonObject& root = jsonBuffer.createObject();

  // Create the "analog" array
  JsonArray& analogValues = root.createNestedArray("analog");
  for (int pin = 0; pin < 6; pin++) {
    // Read the analog input
    int value = analogRead(pin);

    // Add the value at the end of the array
    analogValues.add(value);
  }

  // Create the "digital" array
  JsonArray& digitalValues = root.createNestedArray("digital");
  for (int pin = 0; pin < 14; pin++) {
    // Read the digital input
    int value = digitalRead(pin);

    // Add the value at the end of the array
    digitalValues.add(value);
  }

  Serial.print(F("Sending: "));
  root.printTo(Serial);
  Serial.println();

  // Write response headers
  client.println("HTTP/1.0 200 OK");
  client.println("Content-Type: application/json");
  client.println("Connection: close");
  client.println();

  // Write JSON document
  root.prettyPrintTo(client);

  // Disconnect
  client.stop();
}
```

### Classes used in this example

* [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/)
* [`JsonObject`]({{site.baseurl}}/api/jsonobject/)

### Functions used in this example

* [`JsonArray::add()`]({{site.baseurl}}/api/jsonarray/add/)
* [`JsonBuffer::createObject()`]({{site.baseurl}}/api/jsonbuffer/createobject/)
* [`JsonObject::createNestedArray()`]({{site.baseurl}}/api/jsonobject/createnestedarray/)
* [`JsonObject::prettyPrintTo()`]({{site.baseurl}}/api/jsonobject/prettyprintto/)
* [`JsonObject::printPrintTo()`]({{site.baseurl}}/api/jsonobject/printprintto/)

### Keep learning

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson, and it's only 15 bucks!

The chapter "Serialize with ArduinoJson" is a tutorial to learn how to generate JSON documents with the library. It begins with a simple example, and then adds more features like serializing directly to a file or an HTTP client.