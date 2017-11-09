---
title: "Error: 'equals' is not a member of 'ArduinoJson::Internals::StringTraits<const int&, void>'"
description: This error happens because an integer has been used instead of a string.
keywords: ArduinoJson,error
layout: faq
tags: faq
faq-group: Known problems
popularity: 0
---

This error occurs when you index a `JsonObject` with an integer instead of a string.

For example, it happens with the following code:

```c++
int i = 0;
auto value = obj[i];
```

The compiler generates an error similar to this one:

    error: 'equals' is not a member of 'ArduinoJson::Internals::StringTraits<const int&, void>'

Indeed, a `JsonObject` can only be indexed by a string, like this:

```c++
const char* key = "key";
auto value = obj[key];
```

If you do need to access the members of the `JsonObject` one by one, consider iterating over the key-value pairs:

```c++
for (JsonPair& kv : obj) {
    Serial.println(kv.key);
    Serial.println(kv.value.as<char*>());
}
```

See:

* [`JsonObject::operator[]`]({{site.baseurl}}/api/jsonobject/subscript/)
* [`JsonObject::begin() / end()`]({{site.baseurl}}/api/jsonobject/begin_end/)
