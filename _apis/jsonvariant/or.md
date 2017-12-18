---
title: JsonVariant::operator|
description: The operator | changes the value return when the JsonVariant is undefined or incompatible.
keywords: ArduinoJson,JsonVariant,or,default,operator
layout: api
tags: api
api-group: JsonVariant
---

##### Description

Changes the value return when the [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/) is undefined or incompatible.

In other words, it changes the default value.

This feature was introduced in version 5.12.

##### Signatures

```c++
bool               operator|(bool defaultValue) const;

float              operator|(float defaultValue) const;
double             operator|(double defaultValue) const;

signed char        operator|(signed char defaultValue) const;
unsigned char      operator|(unsigned char defaultValue) const;
signed int         operator|(signed int defaultValue) const;
unsigned int       operator|(unsigned int defaultValue) const;
signed short       operator|(signed short defaultValue) const;
unsigned short     operator|(unsigned short defaultValue) const;
signed long        operator|(signed long defaultValue) const;
unsigned long      operator|(unsigned long defaultValue) const;
unsigned long long operator|(unsigned long long defaultValue) const; // <- may require ARDUINOJSON_USE_LONG_LONG
signed long long   operator|(signed long long defaultValue) const;   // <- may require ARDUINOJSON_USE_LONG_LONG

const char*        operator|(char* defaultValue) const;
const char*        operator|(const char* defaultValue) const;
String             operator|(String defaultValue) const;
std::string        operator|(const std::string& defaultValue) const;
```

##### Arguments

`defaultValue`: the value to return is the [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/) is undefined or incompatible.

##### Return value

* The value of the variant, if it can be converted to the type of `defaultValue`.
* `defaultValue` if not.

Remark: even if `JsonVariant::is<char*>()` returns `true` for `null`, the operator `|` returns `defaultValue` when that happens.

##### Example

```c++
int port = config["port"] | 80;
strlcpy(hostname, config["hostname"] | "example.com", sizeof(hostname));
```

##### See also

* [`JsonVariant::as<T>()`]({{site.baseurl}}/api/jsonvariant/as/)
* [`JsonVariant::is<T>()`]({{site.baseurl}}/api/jsonvariant/is/)
* [`JsonConfigFile.ino`]({{site.baseurl}}/example/config/)
