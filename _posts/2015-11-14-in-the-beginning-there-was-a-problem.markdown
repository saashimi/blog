---
layout: post
title:  "In the Beginning There was a Problem"
date:   2015-11-15
categories: transit app update
---
In the beginning, there was a city planner-turned-(software)-developer who wanted 
to use his newfound powers to map *something.* Lacking imagination, he went back
to what he was familiar with--transit maps.  It seemed that the advice, whether
or not for writers of prose or of software, was to write what you know. 

**This blog will document my attempt at making a simple web-based transit mapping 
application.** 

As a novice programmer, there are a lot of moving parts to track, but if successfully
accomplished, I'll end up with a tool that is hopefully useful to transit users out there.

# Where's My Bus? #
As an occasional TriMet rider, I've often found myself wondering where a particular
TriMet vehicle is. While TriMet's website allows you to do this, it requires that 
you select a current stop to see the time-to-arrival of the closest vehicle. 

![TriMet screenshot]({{ site.baseurl }}/assets/2015-11-15_22-07-48.png)

This is fine for most purposes, but what if you were running late and wanted to 
see if you could meet a particular bus that wasn't the current or the next one?
Or if there was massive traffic in a given area and were wondering if you would
be able to walk and meet the bus at a particular stop?  This would all be possible
using the current interface, but simply *seeing* where your bus was at a given 
moment would seem to be more intuitive.

# There's My Bus! #
The problem of locating the transit vehicles did not seem too difficult. Fortunately,
TriMet uses the [General Transit Feed Specification Reference (GTFS)][gtfs], which 
outputs the realtime positions of equipped vehicles as a JSON file. Here's a sample
output:

{% highlight js%}
{
expires: 1447600333000,
signMessage: "17 To Saratoga",
serviceDate: 1447574400000,
loadPercentage: null,
latitude: 45.4897575,
nextStopSeq: 18,
type: "bus",
blockID: 1702,
signMessageLong: "17 Holgate/Broadway to NE Saratoga & 27th",
lastLocID: 2697,
nextLocID: 2695,
locationInScheduleDay: 25727,
newTrip: false,
longitude: -122.5480119,
direction: 1,
inCongestion: false,
routeNumber: 17,
bearing: 269,
garage: "CENTER",
tripID: "6025634",
delay: 34,
extraBlockID: null,
messageCode: 316,
lastStopSeq: 17,
vehicleID: 3115,
time: 1447600095234,
offRoute: false
},
{% endhighlight %}  

Keying into the JSON was not too difficult (more on this in a future post) and
allowed me to extract the latitude and longitude positions of the buses.

From there it was straightforward to pass the positions as markers into google 
static maps (again, more on this in a future post). 

![static map]({{ site.baseurl }}/assets/2015-11-15_test.png)

3 Route 9 vehicles in service (data is from early Saturday morning), as shown on
a google static map! And there is our proof of concept.  

From here it's a long way to a full-fledged app, but the critical functionality
is there.

[gtfs]: https://developers.google.com/transit/gtfs/reference?hl=en
