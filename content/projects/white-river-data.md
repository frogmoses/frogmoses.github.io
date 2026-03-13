+++
title = "Can I Go Fishing?"
date = 2026-03-13
draft = false
+++

My family and I go fishing regularly at the White River below Bull Shoals Dam. One of the main topics of conversation is "how many generators are running", as that impacts where you can go, what the fishing might be like, whether you can get out and wade. To get that information, you call the Army Corps of Engineers and listen to the recording.

I thought that was so old-fashioned, why can't we do that with a bot...just send a text and get the data back through an api. The thing was there was no simple generation count. The data was all in cubic feet per second (CFS)...and down the rabbit hole I went.

Not only was the recorded phone number oversimplifying the water conditions, it didn't account for the travel time of the latest release.

So this project was built to help solve that. It scrapes the Army Corps data for Bull Shoals Dam, and tries to show the current and near-future conditions at the White Hole Resort, 7 miles downstream. 

It accounts for the 2–4 hours it takes released water to travel from the dam to the White Hole. You're seeing what's actually happening at the fishing spot, not what left the dam an hour ago.

The report updates every hour, automatically. 

As for the accuracy, I'm not sure I have it nailed down yet. This is actually version 2, which has a much better accuracy. 

One of the interesting challenges I've seen as I've shared this with the old timers is that they are conditioned to think in generators. Their long-term experience with the river is tied to that metric. CFS is very different and there is a natural skepticism of this data. This makes it hard to defend. The only valid proof would be a CFS monitor at the White Hole to correlate the data. 

I'm indebted to the Cotter Trout Dock for providing their great analysis of the data, which they post on their site: [Cotter Trout Dock](https://www.cottertroutdock.com/Bull_Shoals_Dam_generation.htm)

[View the live report](https://briancarroll.cool/WhiteRiverData/white_hole_conditions.html)

[View the code on GitHub](https://github.com/frogmoses/WhiteRiverData)
