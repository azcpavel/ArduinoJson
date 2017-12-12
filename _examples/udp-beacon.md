---
title: JsonUdpBeacon.ino
description: This example shows how to send a JSON document to a UDP socket. It uses the Ethernet library but could easily be changed to support Wifi.
keywords: ArduinoJson,UDP,example
tags: example
layout: example
---

## Description

This example shows how to send a JSON document to a UDP socket.

It uses the [Ethernet library](https://www.arduino.cc/en/Reference/Ethernet), but can be easily adapted for [Wifi](https://www.arduino.cc/en/Reference/WiFi).

At regular interval, it sends a UDP packet containing the status of analog and digital pins.
The JSON document looks like the following:

```json
{
  "analog": [ 0, 1, 2, 3, 4, 5 ],
  "digital": [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13 ]
}
```

If you want to test this program, you need to be able to receive the UDP packets.
For example, you can run [netcat](https://nmap.org/ncat/) on your computer

    ncat -ulp 8888

## Source code

```c++
// ArduinoJson - arduinojson.org
// Copyright Benoit Blanchon 2014-2017
// MIT License

#include <ArduinoJson.h>
#include <Ethernet.h>
#include <SPI.h>

byte mac[] = {0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED};
IPAddress remoteIp(192, 168, 0, 108);  // <- EDIT!!!!
unsigned short remotePort = 8888;
unsigned short localPort = 8888;
EthernetUDP udp;

void setup() {
  // Initialize serial port
  Serial.begin(9600);
  while (!Serial) continue;

  // Initialize Ethernet libary
  if (!Ethernet.begin(mac)) {
    Serial.println(F("Failed to initialize Ethernet library"));
    return;
  }

  // Enable UDP
  udp.begin(localPort);
}

void loop() {
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

  // Log
  Serial.print(F("Sending to "));
  Serial.print(remoteIp);
  Serial.print(F(" on port "));
  Serial.println(remotePort);
  root.printTo(Serial);

  // Send UDP packet
  udp.beginPacket(remoteIp, remotePort);
  root.printTo(udp);
  udp.println();
  udp.endPacket();

  // Wait
  delay(10000);
}
```

## Where to go next?

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The book ["Mastering ArduinoJson"](https://leanpub.com/arduinojson/) is the best material to learn how to use ArduinoJson, and it's only 15 bucks!

The chapter "Serialize with ArduinoJson" is a tutorial to learn how to generate JSON documents with the library. It begins with a simple example, and then adds more features like serializing directly to a file or a stream.
