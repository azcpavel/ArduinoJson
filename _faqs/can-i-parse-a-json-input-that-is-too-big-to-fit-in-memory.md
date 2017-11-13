---
title: Can I parse a JSON input that is too big to fit in memory?
description: It's not possible to parse a JSON that doesn't fit in memory
keywords: ArduinoJson,StaticJsonBuffer,DynamicJsonBuffer
layout: faq
tags: faq
faq-group: Deserialization
popularity: 161
---

### Is it possible?

No.

### Why?

By design, ArduinoJson stores the complete representation of the JSON object tree in memory.

If you use the zero-copy mode (mutable input), the whole JSON input must stay in memory.

If the input is read-only (like a [`Stream`](https://www.arduino.cc/en/Reference/Stream)), the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/) needs to make copies of the input, so the result is almost the same (except for spaces and punctuation).

### How to solve?

#### Option 1: Parse the stream in chunk

One cool feature of ArduinoJson is that, when it parses an object from a [`Stream`](https://www.arduino.cc/en/Reference/Stream), it stops reading when it encounters the closing `}`, and the same is true for arrays.

This feature allows to parse streams in chunks, you just need to call [`JsonBuffer::parseObject()`]({{site.baseurl}}/api/jsonbuffer/parseobject/) in a loop.
Of course, don't forget to skip the commas (`,`) between the objects.
As usual, don't reuse the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/description/), declare it inside the loop.

For example, if you want to parse the huge response of a 10-day forecast of Weather Underground, you can skip the beginning until `"forecastday": [` is found (use [`Stream::find()`](https://www.arduino.cc/en/Reference/StreamFind)), and then parse the objects for each day one after the other.

#### Option 2: bye-bye ArduinoJson :cry:

The library [json-streaming-parser](https://github.com/squix78/json-streaming-parser) takes an entirely different approach to ArduinoJson, which makes it suitable for this kind of problems.
