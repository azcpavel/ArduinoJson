---
layout: page
title: Mastering ArduinoJson
subtitle: Learn how to use the most popular Arduino library, from the author himself!
description: "The book Mastering ArduinoJson is the official guide for using ArduinoJson. It is for both beginners and advanced users."
keywords: ArduinoJson,book
---

<img src="{{site.baseurl}}/images/cover500.png" class="float-right" alt="Mastering ArduinoJson">

The book "Mastering ArduinoJson"  is the ultimate guide to learn how to use the library efficiently.
This book explains everything you need to know to serialize and deserialize JSON documents in a deeply embedded environment.
It is written by Benoit Blanchon, the author of ArduinoJson.

## Who is this book for?

If you never used ArduinoJson, you will appreciate this book because it guides you through your learning. It starts with the basic usage of the library and increments the complexity step by step. The last chapter analyzes several example projects and explains the design choices. It is a much better way to learn than blindly copy-pasting the examples.

If you are already using ArduinoJson, you will learn how to get the best performance and the most straightforward code. You will discover that many examples found on the Internet are suboptimal and even dangerous. The sample projects will you a sense of how the library should be used and will give you a new perspective on your projects.

## What knowledge is required?

This book is not a course on Arduino or embedded programming. It assumes a small experience with Arduino; you do not need to be a master, just to be able to compile and run a simple sketch.

Many Arduino users lack some of the fundamental principles of C++, that is why this book starts with a quick refresher. However, it does not pretend to teach C++ from scratch; it assumes the knowledge of another object-oriented programming language, such as C# or Java. There is much material to learn how to program with Arduino, but most of them miss essential parts that are crucial in your development career. This chapter covers the holes left by the other Arduino books, that is why I called it "the missing C++ course."

## What is in the book?

This book is not a compilation of resource already available online. All the content is new, and nothing was recycled from existing documents.

It contains many new code samples and original illustrations.

Contrary to the documentation on arduinojson.org, which grew organically from the GitHub wiki, this book is the result of several months of continuous work, starting from scratch. The result is a coherent and complete learning material.

<iframe width="560" height="315" src="https://www.youtube.com/embed/iSYXTchIU1I" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

### Table of content:

1. Introduction
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
3. Deserialize with ArduinoJson
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

## Code samples

The book comes with several new sample projects.
When you buy the book, you get access to a zip file with all the code samples.

<a href="{{site.baseurl}}{% link images/7zip.png %}"><img class="img-thumbnail" src="{{site.baseurl}}{% link images/7zip.png %}" width="560" alt="Content of the zip file"></a>

## How is the book written?

This book is optimized for fast and easy reading.

It uses short sentences, active voice, and conversational style, to ensure a smooth understanding, even for non-English speakers.

The book is well balanced between text and code.

Code snippets are short and focused, so there are easy to digest, but the complete programs are available in the zip file.

The book is designed to be read from cover to cover without a computer, so it is the perfect format to learn in your commute.

It is also well segmented, so you can quickly skim when you are looking something in particular.

## Why buy this book?

By buying this book, you encourage the development of high-quality libraries. By providing a (modest) source of revenue for open-source developers like me, you ensure that the libraries that you rely on are continuously improved and won't be abandoned after a year.

The current version of the book covers ArduinoJson 5.12, but you will have access to newer revisions as soon as they exist. You only have to buy this book once, you won't have to pay for upgrades.

## Buying option 1: Leanpub

<div class="row">
    <div class="col-2">
    </div>
    <div class="col-2">
        <h4>PDF</h4>
        <a href="{{site.baseurl}}{% link images/acrobat.png %}">
        <img src="{{site.baseurl}}{% link images/acrobat-thumb.png %}" alt="Mastering ArduinoJson on Adobe Reader">
        </a>
    </div>
    <div class="col-2">
        <h4>ePub</h4>
        <a href="{{site.baseurl}}{% link images/tablet.png %}">
        <img src="{{site.baseurl}}{% link images/tablet-thumb.png %}" alt="Mastering ArduinoJson on Tablet">
        </a>
    </div>
    <div class="col-2">
        <h4>Kindle</h4>
        <a href="{{site.baseurl}}{% link images/kindle.png %}">
        <img src="{{site.baseurl}}{% link images/kindle-thumb.png %}" alt="Mastering ArduinoJson on Kindle">
        </a>
    </div>
    <div class="col-2">
        <h4>Online</h4>
        <a href="{{site.baseurl}}{% link images/leanpub-online.png %}">
        <img src="{{site.baseurl}}{% link images/leanpub-online-thumb.png %}" alt="Mastering ArduinoJson on Leanpub">
        </a>
    </div>
</div>

<b style="font-size: 160%; color: red">All formats, DRM-free, for only $14.99 ! ! !</b>

<a class="btn btn-primary btn-lg" href="https://leanpub.com/arduinojson">Buy on <img alt="Leanpub" src="{{site.baseurl}}{% link images/leanpub-20.png %}"></a>
<img class="mx-2" alt="PayPal" src="{{site.baseurl}}{% link images/paypal.png %}">
<img class="mx-2" alt="Visa" src="{{site.baseurl}}{% link images/visa.png %}">
<img class="mx-2" alt="Mastercard" src="{{site.baseurl}}{% link images/mastercard.png %}">

## Buying option 2: Amazon

<div class="row">
    <div class="col-2">
    </div>
    <div class="col-2">
        <h4>Kindle</h4>
        <a href="{{site.baseurl}}{% link images/kindle.png %}">
        <img src="{{site.baseurl}}{% link images/kindle-thumb.png %}" alt="Mastering ArduinoJson on Kindle">
        </a>
    </div>
</div>

<b style="font-size: 160%; color: red">Kindle only, $9.99</b>

<a class="btn btn-warning btn-lg" href="https://www.amazon.com/dp/B078NB88G3">Buy on <img alt="Amazon" src="{{site.baseurl}}{% link images/amazon-20.png %}"></a>
<img class="mx-2" alt="Visa" src="{{site.baseurl}}{% link images/visa.png %}">
<img class="mx-2" alt="Mastercard" src="{{site.baseurl}}{% link images/mastercard.png %}">