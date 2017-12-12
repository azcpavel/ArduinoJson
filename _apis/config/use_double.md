---
title: ARDUINOJSON_USE_DOUBLE
description: ARDUINOJSON_USE_DOUBLE changes the type used to store floating-point values values in `JsonVariant`.
keywords: ArduinoJson,float,double
layout: api
tags: api
api-group: Configuration
---

`ARDUINOJSON_USE_DOUBLE` determines the type used to store floating point values in [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/description):

* If `ARDUINOJSON_USE_DOUBLE == 0`, then [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/description) stores a `float`
* If `ARDUINOJSON_USE_DOUBLE == 1`, then [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/description) stores a `double`

The default is `0` on embedded systems, `1` otherwise.

```c++
#define ARDUINOJSON_USE_DOUBLE 1 // we need to store 64-bit doubles
#include <ArduinoJson.h>
```

:warning: Caution: the memory consumption will be higher, and the results from the [ArduinoJson Assistant]({{site.baseurl}}/assistant/) will be wrong.

:warning: Caution: make sure you use the same value for each compilation unit, i.e., for each `.ino` and `.cpp` in your project.

