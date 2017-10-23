---
title: "Warning: floating constant exceeds range of 'double'"
description: The problem has been fixed in ArduinoJson 5.11.1
layout: faq
tags: faq
faq-group: Known problems
popularity: 11
---

NOTE: this is only applicable for ArduinoJson strictly older to 5.11.1

This may happen if you're targetting a platform where `double`s have only 32-bits.

Usually ArduinoJson can detect this, but when it doesn't you may have the following errors:

```
warning: floating constant exceeds range of 'double' [-Woverflow]
warning: floating constant truncated to zero [-Woverflow]
```

or

```
Error[Pe030]: floating constant is out of range
```

The solution is to define `ARDUINOJSON_DOUBLE_IS_64BITS` to `0`:

```c++
#define ARDUINOJSON_DOUBLE_IS_64BITS 0
#include <ArduinoJson.h>
```