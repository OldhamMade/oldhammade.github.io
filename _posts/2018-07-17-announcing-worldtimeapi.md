---
layout: post
title: "Announcing the launch of WorldTimeAPI.org"
excerpt: "A simple JSON/plain-text API to obtain the current time in, and related data about, a timzone."
category: blog
tags:
  - tools
  - elixir
  - phoenix
published: true
---

OldhamMade has recently completed the initial development and deployment of [WorldTimeAPI](http://worldtimeapi.org), a simple web service which returns the local-time for a given timezone as either JSON or plain-text. Some additional information is provided, such as whether that timezone is currently in Daylight Savings Time, when DST starts and ends, the UTC offset, etc.

The API also exposes endpoints to obtain this information by translating an IP to a timezone. This can be done either for the IP of the system making the request, or for an explicitly provided IP address. Currently, this lookup is IPv4 only, uses freely available GeoIP databases, and is provided on a "best effort" basis -- errors and omissions may occur.

The API supports returning data in both JSON and plain-text formats, and is mostly targetted as a free service for low-power IoT devices.

[WorldTimeAPI](http://worldtimeapi.org) was developed in [Elixir](https://elixir-lang.org) using the [Phoenix framework](https://phoenixframework.org) and plain-old HTML, with a focus on simplicity and speed.
