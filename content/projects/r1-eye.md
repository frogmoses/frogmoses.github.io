+++
title = "R1-Eye, vision analysis of coffee bean roasts"
date = 2026-03-14
draft = false
+++

As I described in my previous post [Automated Coffee Roasting Analysis](https://briancarroll.cool/projects/coffee-roasting/), I roast coffee at home on a Hottop KN-8828b-2k+. The Hottop has a viewport on the left side facing away from the control panel. When roasting all my focus is on the laptop, which sits on the right side of the roaster. I can't really see the beans during the roast and can't visually assess the changes, which is a key criteria of the beans' development.

After jailbreaking the Rabbit R1, I was looking to use it for something real, then inspiration struck. Since I could now do whatever I want with the R1, including having live control over it, why not use it to watch the beans for me, capture point-in-time images of the roast, and have the images visually analyzed via AI to include in my larger coffee roasting analysis pipeline.

That's what this project does...and here is how it does it.

The R1 sits in front of the roaster viewport. When I start a roast in Artisan, the r1-eye (Claude named it "sentinel") automatically receives roast events via WebSocket. On each event, the sentinel:

1. Raises the R1's motorized camera via sysfs
2. Taps the camera UI programmatically to take a full 8MP photo
3. Pulls the photo over ADB, crops to the bean viewport (which is the bottom right quadrant where the beans are most visible), then applies white balance correction and sharpening
4. Sends it to Claude Vision with roast context (elapsed time, current phase) for color assessment and a 1-10 development score
5. Logs everything to a timestamped JSON that feeds into my roast analysis pipeline

Captures are phase-adaptive — every 30s during drying (slow changes), every 20s during Maillard, and every 10s during development (when color shifts fast). Key events like first crack trigger an immediate capture regardless of timing.

This started as "can I make the R1 do something useful?" and turned into a tool I actually use every roast. I was surprised by how quickly it came together. I would have been daunted in the past by the thought of having to learn all the intricacies of ADB and WebSocket and the like. Working with AI became a joy because I could get it done by conducting, not grunt work. It unlocked all this possibility. Matt Webb said in a great blog series, 
> "AI tools provide what I’ve previously called Universal Basic Agency and it is wonderful. When individuals are unblocked, we get an abundance of creativity in the world." [Matt Webb's post](https://interconnected.org/home/2026/03/12/nwh)


I've never felt more unblocked.

If you have an R1 collecting dust and a hobby that could use a dedicated camera with AI analysis, the code is generic enough to adapt.

I do intend to expand the r1 to be a real AI device in the near future. Something like a 1-button push to activate an AI workflow - maybe like the *claw tooling - an agent trigger. 

GitHub: [github.com/frogmoses/r1-eye](https://github.com/frogmoses/r1-eye) 
