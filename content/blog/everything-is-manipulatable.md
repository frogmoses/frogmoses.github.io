+++
title = 'Everything is Manipulatable'
date = 2024-09-23
draft = false
tags = ['windows', 'security', 'problem-solving', 'hacking']
+++

When working on the [task scheduler issue](/blog/windows-task-scheduler-woes/) I previously posted, I managed to lock myself out of my computer. It’s been a long time since I have done that. I had some research to do. These days that means querying an LLM but I actually didn’t find this answer through them. Good ol’ Reddit solved it.

See, on the Windows login screen, there is a button for the Ease of Access settings. If you click it, it will run an .exe called utilman.exe. This password recovery process involves you booting from the USB, opening the command-line, backing up utilman.exe, creating a copy of cmd.exe, renamed as utilman.exe. Now when you boot back to Windows, you can access the command prompt from the login screen by clicking Ease of Access and resetting your password.

This is all well-known and many people have commented on it. What is interesting about this approach is the mindset behind it, the one that thinks all things are manipulatable. (I heard that phrase on The History of The Gibson on the Hacker History Podcast.) It is the heart of creativity to transpose one thing into another, often unrelated context.

I remember feeling happy doing this hack. It was joyful to remember this lesson. Day-to-day life seems to dull this askance approach to problem solving. Any time I can create something new or solve a problem through a sideways approach is very fulfilling.

Any way, I reset my password, figured out the task scheduling problem (by going an entirely different route), and am now debating whether to encrypt my drive!