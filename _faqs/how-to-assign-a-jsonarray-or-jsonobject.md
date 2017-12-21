---
title: How to assign a <code>JsonArray</code> or <code>JsonObject</code>?
description: It's not possible to reassign a C++ reference. Instead use a pointer or a JsonVariant.
keywords: ArduinoJson,JsonArray,JsonObject,reference
layout: faq
tags: faq
faq-group: Common
popularity: 116
---

If you try to reassign a [`JsonArray`]({{site.baseurl}}/api/jsonarray/) or a [`JsonObject`]({{site.baseurl}}/api/jsonobject/), you'll have the following error:

```
error: use of deleted function 'ArduinoJson::JsonArray& ArduinoJson::JsonArray::operator=(const ArduinoJson::JsonArray&)'
error: use of deleted function 'ArduinoJson::JsonObject& ArduinoJson::JsonObject::operator=(const ArduinoJson::JsonObject&)'
```

Indeed, [`JsonArray`]({{site.baseurl}}/api/jsonarray/) and [`JsonObject`]({{site.baseurl}}/api/jsonobject/) have their assignment operators private, so you cannot reassign them. Moreover, it's impossible to reassign a C++ reference.

One solution is to use a pointer instead.

```c++
JsonObject* myObject = &root["myObject"].as<JsonObject>();
```

You can also use a [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/) which will act as a wrapper around the pointer.

```c++
JsonVariant myObject = root["myObject"];
```
