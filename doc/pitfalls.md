---
layout: doc
title: Avoiding Pitfalls
description: What are the common pitfalls of ArduinoJson
keywords: ArduinoJson,pitfalls,caveats,mistakes,tips
tags: doc
---

As [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) is the corner stone of this library, you'll see that every pitfall listed here is related to a wrong understanding of the memory model.

Make sure you read [ArduinoJson memory model]({{site.baseurl}}/doc/memory/) before going further.

## 1. Make `StaticJsonBuffer` big enough

By design, the library has no way to tell you why `parseArray()` or `parseObject()` failed.

There are basically two reasons why they may fail:

1. the JSON string is invalid,
2. the JSON string contains more values that the buffer can store.

So, if you are sure the JSON string is correct and you still can't parse it, you should try to increase the size of the `StaticJsonBuffer`.

You can use the [ArduinoJson Assistant]({{site.baseurl}}/assistant/) to compute the required size.

See:

* [FAQ: Why parsing fails?]({{site.baseurl}}/faq/why-parsing-fails/)
* [FAQ: How to determine the buffer size?]({{site.baseurl}}/faq/how-to-determine-the-buffer-size/)


## 2. Make sure everything fits in memory

You may go into unpredictable trouble if you allocate more memory than your processor really has.
It's a very common issue in embedded development.

To diagnose this, look at every big objects in your code and sum their size to check that they fit in RAM.

For example, don't do this:

```c++
char json[1024];                // 1 KB
StaticJsonBuffer<512> buffer;   // 514 B
```

because it may be too big for a processor with only 2 KB: you need free memory to store other variables and the call stack.

That is why an 8-bit processor is not able to parse long and complex JSON strings.

See:

* [FAQ: Can I parse a JSON input that is too big to fit in memory?]({{site.baseurl}}/faq/can-i-parse-a-json-input-that-is-too-big-to-fit-in-memory/)
* [FAQ: Why does my device crash or reboot?]({{site.baseurl}}/faq/why-does-my-device-crash-or-reboot/)


## 3. Keep the `StaticJsonBuffer` in memory long enough

Remember that [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/)'s functions return references.
References don't contain data, they are just pointers to the actual.
So they can only work if the actual data is in memory.

For example, don't do this:

```c++
JsonArray& getArray(char* json)
{
    StaticJsonBuffer<200> buffer;
    return buffer.parseArray(json);
}
```

because the local variable `buffer` will be *removed* from memory when the function [`parseArray()`]({{site.baseurl}}/api/jsonbuffer/parsearray/) returns, and the `JsonArray&` will point to an invalid location.

## 4. Don't reuse the same [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/)

During is lifetime a [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) growth until it's discarded. If you try to reuse the same instance several times, it will rapidly get full. This is true for both `DynamicJsonBuffer` and `StaticJsonBuffer`.

For this reason, **you should not use a global variable** for your [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/). I don't think there is any scenario in which a global [`JsonBuffer`]({{site.baseurl}}/api/jsonbuffer/) would be a valid option.

The best practice is to **declare it in a local scope**, so that it's discarded as soon as possible. My advice is to declare it in a function whose unique role is to handle the JSON serialization.

See:

* [FAQ: The first parsing succeeds, why does the next ones fail?]({{site.baseurl}}/faq/the-first-parsing-succeeds-why-do-the-next-ones-fail)
* [FAQ: The first serialization succeeds, why do the next ones fail?]({{site.baseurl}}/faq/the-first-serialization-succeeds-why-do-the-next-ones-fail/)
* [FAQ: How to reuse a JsonBuffer?]({{site.baseurl}}/faq/how-to-reuse-a-jsonbuffer/)

## 5. Keep the JSON string in memory long enough

The library never make memory duplication.
This has an important implication on string values, it means that the library will return pointer to chunks of the string.

For instance, let's imagine that you parse `["hello","world"]`, like this:

```c++
char[] json = "[\"hello\",\"world\"]";
StaticJsonBuffer<32> buffer;
JsonArray& array = buffer.parseArray(json);

const char* first = array[0];
const char* second = array[1];
```

In that case, both `first` and `second` are pointers to the content of the original string `json`.
So this will only work if `json` is still in memory.

## 6. Do not assume that strings are copied

By default, ArduinoJson doesn't make copies of strings, it only stores pointers.
So, if you declare a `char[]` in a loop, the same pointer will be added several times.
As a workaround, you can use [`JsonBuffer::strdup()`]({{site.baseurl}}/api/jsonbuffer/strdup/) to make a copy.

See:

* [FAQ: Using a loop, why are values all the same?]({{site.baseurl}}/faq/using-a-loop-why-are-values-all-the-same/)

## 7. Avoid read-only string for input

ArduinoJson has two parsing modes depending on the type of input

1. If the input is read-only, the parser copies the input
2. If the input is writeable, the parser modifies the input and doesn't make copies.

In the "zero-copy" mode, the parser modifies the string for two reasons:

1. it inserts `\0` to terminate substrings,
2. it translates escaped characters like `\n` or `\t`.

Most of the time this wont be an issue, but there are some corner cases that can be problematic.

Let take the example bellow:

```c++
char[] json = "[\"hello\",\"world\"]";
StaticJsonBuffer<32> buffer;
JsonArray& array = buffer.parseArray(json);
```

If you replace it by:

```c++
char* json = "[\"hello\",\"world\"]";
StaticJsonBuffer<32> buffer;
JsonArray& array = buffer.parseArray(json);
```

Depending on your platform, you may have an exception because the parser tries to write at a location that is read-only.
In the first case `char json[]` declares an array of `char` initialized to the specified string.
In the second case `char* json` declares a pointer to a read-only string, in fact it should be a `const char*` instead of a `char*`.

See:

* [FAQ: How to reduce memory usage]({{site.baseurl}}/faq/how-to-reduce-memory-usage/)


## Where to go next?

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

The [ArduinoJson ebook](https://leanpub.com/arduinojson/), contains two complete tutorials on serialization and deserialization. It shows every pitfalls on the way. It finishes with an analysis of the best practices in several sample projects.

Most of the time, the problem comes from a poor understanding of basic C++ concepts such as pointers, references and object lifetime. That is why the book also contains a quick C++ course to catch up with those things.
