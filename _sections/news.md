---
layout: page
title: News
description: "News from the ArduinoJson library: new versions, projets, advices and more!"
keywords: ArduinoJson,news
tags: news
section_tag: news
popularity: 0
---

<dl>
  {% for post in site.posts %}
	<dt>{{ post.date | date: "%Y-%m-%d" }} <a href ="{{site.baseurl}}{{post.url}}">{{post.title}}</a></dt>
    <dd>{{post.description}}</dd>
  {% endfor %}
</dl>

> #### Do you want to receive updates from ArduinoJson?
>
> You can [subscribe to the Atom feed (similar to RSS)]({{site.baseurl}}/feed.xml).
{: .alert .alert-info}