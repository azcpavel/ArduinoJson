---
title: JsonVariant::success()
description: Tests if parsing of JsonVariant succeeded
keywords: ArduinoJson,JsonVariant,parsing,valid
layout: api
tags: api
api-group: JsonVariant
---

### Description

Tells whether the variant contains a value.

### Signature

```c++
bool success() const;
```

### Return value

* `true` if the variant contains a value,
* `false` if the variant is empty or invalid.

### Example

```c++
JsonVariant variant;
bool beforeAssign = variant.success(); // false
variant = 42;
bool afterAssign = variant.success(); // true
```

### See also

* [`JsonArray::success()`]({{site.baseurl}}/api/jsonarray/success/)
* [`JsonObject::success()`]({{site.baseurl}}/api/jsonobject/success/)