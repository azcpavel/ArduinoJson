---
title: "Warning: ignoring packed attribute because of unpacked non-POD field"
description: The compiler flag --fpack-struct is causing this warning. There is no solution.
keywords: ArduinoJson,warning,non-POD
layout: faq
tags: faq
faq-group: Known problems
popularity: 32
---

If you pass the flag `--fpack-struct` to the compiler, it will generate the following warning:

```
warning: ignoring packed attribute because of unpacked non-POD field
```

No solution has been found so far: you need to remove that flag if you want to get rid of that warning.
