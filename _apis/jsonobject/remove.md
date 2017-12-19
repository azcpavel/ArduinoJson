---
title: JsonObject::remove()
description: Removes an element from a JsonObject
keywords: ArduinoJson,JsonObject,remove,delete,erase
layout: api
tags: api
api-group: JsonObject
---

### Description

Removes the element at the specified key.

### Signatures

```c++
void remove(const char* key);
void remove(const String& key);
void remove(const std::string& key);
void remove(const __FlashStringHelper* key);
```

### Arguments

`key`: the key to remove from the object.

### Example

```c++
JsonObject& object = jsonBuffer.createObject();
object["A"] = 1;
object["B"] = 2;
object["C"] = 3;
object.remove("B");
object.printTo(Serial);
```

will print the following string to the serial output:

```json
{"A":1,"C":3}
```

### See also

* [`JsonArray::remove()`]({{site.baseurl}}/api/jsonarray/remove/)

> ##### Causes memory leaks :warning:
>
> This function doesn't free the memory allocated to the element in the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).
>
> This is a conscious design decision made to keep the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) fast and small, which is a fundamental principle of the library.
>
> As a consequence, you cannot remove and add elements in a loop, otherwise the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) will overflow.
>
> Don't try to keep the state of your application in a `JsonObject`, instead use custom structures.
{: .alert .alert-danger}