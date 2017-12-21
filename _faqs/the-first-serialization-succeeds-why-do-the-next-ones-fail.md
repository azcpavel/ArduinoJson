---
title: The first serialization succeeds, why do the next ones fail?
description: Serialization fails because the JsonBuffer is reused
keywords: ArduinoJson,failure
layout: faq
tags: faq
faq-group: Serialization
popularity: 61
---

This is usually caused by a reused [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).
The solution is simply to NOT reuse the [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/).

See [The first parsing succeeds, why do the next ones fail?]({{ site.baseurl }}/faq/the-first-parsing-succeeds-why-do-the-next-ones-fail/)
