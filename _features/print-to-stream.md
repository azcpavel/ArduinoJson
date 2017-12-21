---
title: Print to Stream
popularity: 40
---

ArduinoJson is able to print directly to a `Print` or `std::ostream`

```c++
// Send the JSON to the serial port
root.printTo(Serial);
```

...an Ethernet connection

```c++
root.printTo(ethernetClient);
```

...or a Wifi connection

```c++
root.printTo(wifiClient);
```