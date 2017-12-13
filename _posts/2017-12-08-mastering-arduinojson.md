---
title: The book "Mastering ArduinoJson" out!
description: The long awaited book on ArduinoJson is finally out. Let's wee what's inside!
layout: post
---

I announced a ebook on ArduinoJson in October, before it was even completed.
Many people contacted me about that; please apologies, the writing absorbed all my energy.

Well, the book is finally out!

It's called "Mastering ArduinoJson", is published on Leanpub and is written by me.

<a href="https://leanpub.com/arduinojson/"><img src="{{site.baseurl}}/images/cover200.png" class="float-right" alt="Mastering ArduinoJson"></a>

### Who is this book for?

If you never used ArduinoJson, you will appreciate this book because it guides you through your learning. It starts with the basic usage of the library and increments the complexity step by step. The last chapter analyzes several example projects and explains the design choices. It is a much better way to learn than blindly copy-pasting the examples.

If you are already using ArduinoJson, you will learn how to get the best performance and the most straightforward code. You will discover that many examples found on the Internet are suboptimal and even dangerous. The sample projects will you a sense of how the library should be used and will give you a new perspective on your projects.

### What knowledge is required?

This book is not a course on Arduino or embedded programming. It assumes a small experience with Arduino; you do not need to be a master, just to be able to compile and run a simple sketch.

Many Arduino users lack some of the fundamental principles of C++, that is why this book starts with a quick refresher. However, it does not pretend to teach C++ from scratch; it assumes the knowledge of another object-oriented programming language, such as C# or Java. There is much material to learn how to program with Arduino, but most of them miss essential parts that are crucial in your development career. This chapter covers the holes left by the other Arduino books, that is why I called it "the missing C++ course."

### What is in the book?

This book is not a compilation of resource already available online. All the content is new, and nothing was recycled from existing documents.

It contains many new code samples and original illustrations. 

Contrary to the documentation on arduinojson.org, which grew organically from the GitHub wiki, this book is the result of several months of continuous work, starting from scratch. The result is a coherent and complete learning material.

Table of content

1. Introduction *(included in the free sample)*
    1. About this book
    2. Introduction to JSON
    3. Introduction to ArduinoJson
2. The missing C++ course
    1. Why a C++ course?
    2. Stack, heap and globals
    3. Pointers
    4. Memory management
    5. References
    6. Strings
3. Deserialize with ArduinoJson *(included in the free sample)*
    1. The example of this chapter
    2. Parse a JSON object
    3. Extract values from an object
    4. Inspect an unknown object
    5. Parse a JSON array
    6. Extract values from an array
    7. Inspect an unknown array
    8. The zero-copy mode
    9. Parse from read-only memory
    10. Parse from stream
4. Serialize with ArduinoJson
    1. The example of this chapter
    2. Create an object
    3. Create an array
    4. Serialize to memory
    5. Serialize to stream
    6. Duplication of strings
5. Inside ArduinoJson
    1. Why JsonBuffer?
    2. Inside StaticJsonBuffer
    3. Inside DynamicJsonBuffer
    4. Inside JsonArray
    5. Inside JsonObject
    6. Inside JsonVariant
    7. Inside the parser
    8. Inside the serializer
    9. Miscellaneous
6. Troubleshooting
    1. Program crashes
    2. Deserialization issues
    3. Serialization issues
    4. Understand compiler errors
    5. Common error messages
    6. Logging
    7. Ask for help
7. Case Studies
    1. Configuration in SPIFFS
    2. OpenWeatherMap on mkr1000
    3. Weather Underground on ESP8266
    4. JSON-RPC with Kodi
    5. Recursive analyzer
8. Conclusion

### How is the book written?

This book is optimized for fast and easy reading.

It uses short sentences, active voice, and conversational style, to ensure a smooth understanding, even for non-English speakers.

The book is well balanced between text and code.

Code snippets are short and focused, so there are easy to digest, but the complete programs are available in the zip file.

The book is designed to be read from cover to cover without a computer, so it is the perfect format to learn in your commute.

It is also well segmented, so you can quickly skim when you are looking something in particular.

### Why buy this book?

By buying this book, you encourage the development of high-quality libraries. By providing a (modest) source of revenue for open-source developers like me, you ensure that the libraries that you rely on are continuously improved and won't be abandoned after a year.

The current version of the book covers ArduinoJson 5.12, but you will have access to newer revisions as soon as they exist. You only have to buy this book once, you won't have to pay for upgrades.

**Interested? Go to [leanpub.com/arduinojson](https://leanpub.com/arduinojson)**