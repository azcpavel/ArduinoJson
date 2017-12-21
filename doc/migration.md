---
layout: doc
title: Migrating from ArduinoJson v3
description: How to upgrade code written for ArduinoJson version 3
keywords: ArduinoJson,migration,breaking
tags: doc
---

ArduinoJson v4 (and thus v5) was a major rewrite of the library, and the API changed significantly.

## Includes

ArduinoJson v3 had two include files:

    #include <JsonParser.h>
    #include <JsonGenerator.h>

ArduinoJson v4 only has one:

	#include <ArduinoJson.h>

## Namespaces

ArduinoJson v3 had two namespaces:

	using namespace ArduinoJson::Parser;
	using namespace ArduinoJson::Generator;

ArduinoJson v4 doesn't require the `using namespace` statement.
It has a namespace but the `using namespace` is done in the header file.

## StaticJsonBuffer

ArduinoJson v3 had different memory allocation models for the parser:

	JsonParser<16> parser; // 16 being the capacity in "tokens"

and for the generator:

	JsonArray<4> array; // 4 being the number of element
	JsonObject<4> object;

ArduinoJson v4 only has one memory allocation model:

	StaticJsonBuffer<128> buffer; // 128 being the capacity in bytes

## Return values for the parser

ArduinoJson v3 returned value types:

	JsonArray array = parser.parseArray(json);
	JsonObject object = parser.parseObject(json);

ArduinoJson v4 returns references types:

	JsonArray& array = buffer.parseArray(json);
	JsonObject& object = buffer.parseObject(json);

Everything else is compatible

## Creating arrays and objects

ArduinoJson v3 allowed to create [`JsonArray`]({{site.baseurl}}/api/jsonarray/) and [`JsonObject`]({{site.baseurl}}/api/jsonobject/) directly:

	JsonArray<4> array;
	JsonObject<4> object;

ArduinoJson v4 requires that you use a `StaticJsonBuffer` for that:

	JsonArray& array = buffer.createArray();
	JsonObject& object = buffer.createObject();

Note: you don't have to specify the capacity anymore.

## Printable interface

ArduinoJson v3 used to implement the Printable interface, which allowed statements like:

    Serial.print(array);

But ArduinoJson v4 doesn't, instead you need to write this:

	array.printTo(Serial);

Note: there was a good reason for removing that feature, and it's reducing the size of [`JsonArray`]({{site.baseurl}}/api/jsonarray/) and [`JsonObject`]({{site.baseurl}}/api/jsonobject/).