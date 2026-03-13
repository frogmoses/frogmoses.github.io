+++
title = "Coffee Roasting Analysis"
date = 2026-03-13
draft = false
+++

I roast coffee at home on a Hottop KN-8828B-2K+. This roaster can connect to [Artisan](https://artisan-scope.org/) for logging and roaster control. When I first bought the roaster I tried using it with Artisan but I fundamentally didn't understand the roasting process. It was too confusing to know what to change. The software felt very overwhelming. I like to learn on my own and I couldn't find any source of information that really helped me understand both the process and the software. I wound up defaulting to the automatic program on the Hottop.

This winter I got the idea that maybe AI could help me understand the process and improve my roasts systematically. So I threw the Hottop manual into Claude's maw and the data collected from the automatic program, then asked it for a 5 roast improvement plan. At this point everything was done manually.

I was pretty impressed by the advice given by AI and started to glimpse the process through the smoke. After roasting several more batches, manually collecting the data and feeding it into AI for recommendations, I thought...wait, we can automate this and drive a pipeline to analyze the data and suggest next steps. 

So this project was born. 

I hooked up the roaster to my laptop, got Artisan running, and wrote some code to transfer both the `.alog` roasting logs and the accompanying `.pngs` of the graph back to my dev computer. There I wrote some more code to ingest the logs and images, compare them to the targets based on the bean profile and my last batch, and get a recommendation of what to do differently for the next batch. The recommendation was tailored to action...not just "your drying phase was long" but "charge hotter — aim for a turning point around 145-150F to compress drying."

So now, after each roast, I get a full report: summary, bean profile, target comparison, prioritized recommendations, and a "Next Roast" box with 2-4 concrete things to change. Over multiple roasts, it shows a trend table so I can see if I'm actually getting better.

As for the bean profile which informs the target, I buy all my green coffee from [Sweet Maria's Coffee](https://www.sweetmarias.com). For each coffee, they provide an extensive set of cupping notes and bean attributes. I feed that data into the analysis pipeline to inform AI what the bean targets should look like. It's some kind of objective value to compare against.

Anyway, I've used the full pipeline several times now and my coffee roasts have definitely improved. I understand both the Hottop roaster and the process much better through this exploration. 

There are several other tools that play into this ecosystem. I'll be describing them shortly and releasing the code for them as well.

[View the code on GitHub](https://github.com/frogmoses/coffee-roasting)
