---
title: Arduino Library Manager doesn't list the latest versions of ArduinoJson
description: How to fix Arduino Library Manager
keywords: ArduinoJson,Arduino,Library,Manager
layout: faq
tags: faq
faq-group: Known problems
popularity: 38
---

This is a very common issue.

If ArduinoJson doesn't appear in Library Manager, or if only old versions are listed, try to delete the local cache.
This will force the Library Manager to download the library list from scratch.

For example, on Windows, you need to delete:

* `%LOCALAPPDATA%\Arduino15\library_index.json`
* `%LOCALAPPDATA%\Arduino15\library_index.json.tmp.gz`

You don't even need to close Arduino, just re-open the Library Manager.
