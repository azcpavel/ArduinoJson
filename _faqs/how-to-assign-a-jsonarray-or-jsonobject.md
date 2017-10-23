---
title: How to assign a <code>JsonArray</code> or <code>JsonObject</code>?
description: It's not possible to reassign a C++ reference. Instead use a pointer or a JsonVariant.
layout: faq
tags: faq
faq-group: Common
popularity: 116
---

If you try to reassign a `JsonArray&` or a `JsonObject&`, you'll have the following error:

```
error: use of deleted function 'ArduinoJson::JsonArray& ArduinoJson::JsonArray::operator=(const ArduinoJson::JsonArray&)'
error: use of deleted function 'ArduinoJson::JsonObject& ArduinoJson::JsonObject::operator=(const ArduinoJson::JsonObject&)'
```

Indeed, you cannot reassign a `JsonObject&`.

One solution is to use a pointer instead.

```c++
JsonObject* myObject = &root["myObject"].as<JsonObject>();
```

You can also use a `JsonVariant` which will act as a wrapper around the pointer.

```c++
JsonVariant myObject = root["myObject"];
```
