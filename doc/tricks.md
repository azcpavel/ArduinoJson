---
layout: doc
tags: doc
title: Bag of Tricks
keywords: ArduinoJson
description: A collection of useful techniques to accomplish unusual things with ArduinoJson.
---

This page contains some useful techniques to accomplish unusual things with ArduinoJson.

## Look for a nested key

Suppose you have the following JSON document:

```json
{
  "key1": 1,
  "key2": {
    "subkey1": 3,
    "subkey2": 4
  }
}
```

And suppose that you want to check the presence of `subkey1`.

[`JsonObject::containsKey()`]({{site.baseurl}}/api/jsonobject/containskey/) will not work, since `subkey1` is nested inside `key2`.

The following function find a key even if is nested:

```c++
bool containsNestedKey(const JsonObject& obj, const char* key) {
    for (const JsonPair& pair : obj) {
        if (!strcmp(pair.key, key))
            return true;

        if (containsNestedKey(pair.value.as<JsonObject>(), key)) 
            return true;
    }

    return false;
}
```

## Extract an array of integer

Suppose you have an input like this:

```json
{"leds":[56,60,46]}
```

And support that you want to get an `int[]` out of it.

Here is the simplest way to do that:

```c++
#define MAX_LED_COUNT 10

int leds[MAX_LED_COUNT];
int ledCount = root["leds"].as<JsonArray>().copyTo(leds);
```

See [`JsonArray::copyTo()`]({{site.baseurl}}/api/jsonarray/copyto/)

## Merging JSON objects

Suppose you have two JSON objects:

```json
{
  "name": "Benoit"
}
```

and

```json
{
  "age": 36
}
```

And suppose that your goal is to merge the two objects into one:

```json
{
  "name": "Benoit",
  "age": 36
}
```

Well, you can do that easily with the following function:

```c++
void merge(JsonObject& dest, const JsonObject& src) {
   for (auto kvp : src) {
     dest[kvp.key] = kvp.value;
   }
}
```

## Buffered output

Here is a proxy that will put bytes in a buffer before actually writing them to the destination:

```c++
template <size_t CAPACITY>
class BufferedPrint : public Print {
 public:
  BufferedPrint(Print& destination) : _destination(destination), _size(0) {}

  ~BufferedPrint() { flush(); }

  virtual size_t write(uint8_t c) {
    _buffer[_size++] = c;

    if (_size + 1 == CAPACITY) {
      flush();
    }
  }

  void flush() {
    _buffer[_size] = '\0';
    _destination.print(_buffer);
    _size = 0;
  }

 private:
  Print& _destination;
  size_t _size;
  char _buffer[CAPACITY];
};
```

To use this in your code:

```c++
BufferedPrint<256> bufferedPrint(Serial)
root.printTo(bufferedPrint);
```

Use this class if the `Print` implementation sends bytes one-by-one, it will greatly improve the performance of your program.

## Chunked output

Here is a proxy that allow to get only part of the output:

```c++
class ChunkPrint : public Print {
 public:
  ChunkPrint(Print& destination, size_t from, size_t to)
      : _destination(destination), _to_skip(from), _to_write(to - from) {}

  virtual size_t write(uint8_t c) {
    if (_to_skip > 0) {
      _to_skip--;
    } else if (_to_write > 0) {
      _to_write--;
      return _destination.write(c);
    }
    return 0;
  }

 private:
  Print& _destination;
  size_t _to_skip;
  size_t _to_write;
};
```

To use this in your code:

```c++
// print only range [10,20[
ChunkPrint chunkPrint(Serial,10,20);
root.printTo(chunkPrint);
```

Use this class when you need to send the JSON document in chunks, i.e., not all at once.

## Compute hash of JSON output

Here is how you can compute the CRC32 hash of the JSON document without consuming a lot of memory.

```c++
#include <FastCRC.h> // https://github.com/FrankBoesing/FastCRC

class HashPrint : public Print {
public:
    HashPrint() {
      _hash = _hasher.crc32(NULL, 0);
    }

    virtual size_t write(uint8_t c) {
        _hash = _hasher.crc32_upd(&c, 1);
    }

    uint32_t hash() const {
        return _hash;
    }

private:
    FastCRC32 _hasher;
    uint32_t _hash;
};
```

To use this in your code:

```c++
HashPrint hashPrint;
root.printTo(hashPrint);
Serial.println(hashPrint.hash());
```

Use this class when you want to compare two JSON documents

## Throw exception when JsonBuffer is too small

Here is a class that behaves as a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/), except that it will throw an exception if the allocation fails:

```c++
#include <stdexcept>

template <typename TJsonBuffer>
struct Throwing : TJsonBuffer {
  virtual void *alloc(size_t bytes) {
    void *ptr = TJsonBuffer::alloc(bytes);
    if (ptr)
      return ptr;
    else
      throw std::runtime_error("allocation failed");
  }
};
```

This class implement the static decorator pattern, and therefore must be used as below:

```c++
Throwing<StaticJsonBuffer<200> > jsonBuffer;
// or
Throwing<DynamicJsonBuffer> jsonBuffer;
```

## Clone an object or an array

Here is a function that makes a deep copy of a [`JsonVariant`]({{site.baseurl}}/api/jsonvariant/):

```c++
JsonVariant clone(JsonBuffer& jb, JsonVariant prototype)
{
  if (prototype.is<JsonObject>()) {
    const JsonObject& protoObj = prototype;
    JsonObject& newObj = jb.createObject();
    for (const auto& kvp : protoObj) {
      newObj[clone(jb, kvp.key)] = clone(jb, kvp.value);
    }
    return newObj;
  }

  if (prototype.is<JsonArray>()) {
    const JsonArray& protoArr = prototype;
    JsonArray& newArr = jb.createArray();
    for (const auto& elem : protoArr) {
      newArr.add(clone(jb, elem));
    }
    return newArr;
  }

  if (prototype.is<char*>()) {
    return jb.strdup(prototype.as<char*>());
  }

  return prototype;
}
```

This function works with [`JsonObject`]({{site.baseurl}}/api/jsonobject/) and [`JsonArray`]({{site.baseurl}}/api/jsonarray/).