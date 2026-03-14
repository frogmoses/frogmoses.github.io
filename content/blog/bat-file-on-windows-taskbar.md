+++
title = '.bat File on Windows Taskbar'
date = 2024-09-28
draft = false
tags = ['windows', 'python', 'automation']
+++

When building my [Active Directory search tool](/blog/llm-assisted-active-directory-search/), I wanted to launch it from the Windows taskbar. I created a .bat file to activate the python virtual environment and run the program. However, you can't directly add a .bat file to the taskbar.

To get around this you can rename the .bat file extension to .exe, add it to the taskbar, rename the .exe back to .bat, finally edit the properties of the taskbar icon to point back to the renamed .bat file. Why Microsoft?
