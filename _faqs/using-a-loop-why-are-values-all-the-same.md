---
title: Using a loop, why are values all the same?
description: ArduinoJson doesn't copy strings, instead it stores a pointer.
keywords: ArduinoJson,loop,string
layout: faq
tags: faq
faq-group: Serialization
popularity: 0
---

By default, ArduinoJson does not make copies of strings.
This behavior allows it to work with full static memory allocation and ensure an efficient use of CPU cycles.

However, this can have surprising effects...

For instance the following code will not work as expected:

```c++
JsonArray& array = jsonBuffer.createArray();
for (int i=0; i<3; i++) {
    char buffer[16];
    sprintf(buffer, "iteration %d", i);
    array.add(buffer);
}
array.printTo(Serial);
```

One will probably expect the following result:

```json
["iteration 0","iteration 1","iteration 2"]
```

but the actual result would be:

```json
["iteration 2","iteration 2","iteration 2"]
```

That is because the program uses the same memory area for each iteration.

The simplest solution is to explicitly duplicate the strings in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/):

```c++
JsonArray& array = jsonBuffer.createArray();
for (int i=0; i<3; i++) {
    char buffer[16];
    sprintf(buffer, "iteration %d", 0);
    array.add(jsonBuffer.strdup(buffer));
}
array.printTo(Serial);
```

The same principle applies to key and values of [`JsonObject`]({{site.baseurl}}/api/jsonobject/).

Note: If you use `String` instead of a `const char*`, ArduinoJson calls [`JsonBuffer::strdup()`]({{site.baseurl}}/api/jsonbuffer/strdup/) implicitly.