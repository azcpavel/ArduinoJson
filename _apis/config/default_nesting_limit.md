---
title: ARDUINOJSON_DEFAULT_NESTING_LIMIT
description: Changes the default nesting limit of the JSON parser
keywords: ArduinoJson,parsing,nesting
layout: api
tags: api
api-group: Configuration
---

Defines the default value the second parameter of [`JsonBuffer::parseArray()`]({{site.baseurl}}/api/jsonbuffer/parsearray/) and [`JsonBuffer::parseObject()`]({{site.baseurl}}/api/jsonbuffer/parseobject/), which limit the nesting in the JSON input. (the goal is to prevent stackoverflow).

Default is `10` of `ARDUINO` is defined, `50` otherwise.
