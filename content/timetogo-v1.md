---
title: "TimeToGo v1.0.0"
date: 2014-11-15T00:00:04Z
slug: "timetogo-v1"
description: ''
image: '/images/blog/time-to-go.jpg'
tags: ['java']
---
I’m releasing [TimeToGo v1.0.0](https://github.com/nitesh-/TimeToGo) class which converts a future date to ‘time to go’ format. My goal was to develop a class with no dependencies.

So basically, TimeToGo determines time left between the current date and a future date very much like ‘10 days to go or 1 month to go’.

## Usage:
``` java
String timeToGo = TimeToGo.getTimeLeft("2014-11-29"); // Date Should be YYYY-mm-dd format
System.out.println(timeToGo);
```