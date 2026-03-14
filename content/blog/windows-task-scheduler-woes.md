+++
title = 'Windows Task Scheduler Woes'
date = 2024-09-20
draft = false
tags = ['python', 'windows', 'automation', 'NSSM']
+++

My favorite cartoonist has a website where he displays daily selections from his archive. I want this in my life but I can’t be bothered to go to a website everyday. So several years ago, I wrote a python script to take screenshots of the cartoons and email them to me (scraping didn’t work). The script was scheduled through Windows Task Scheduler.

Then I changed computers, brought over the code, and have been struggling for days to get the task scheduler to work. The task wouldn’t run the python script directly. I wrote .bat and .ps1 files to try and activate the virtual environment, then run the scripts. I fixed that, then the images were downloaded as black images. Over and over, problem after problem, including changing my password and getting locked out of my computer (… cool hack to restore to come).

I finally decided to run the script as a Windows Service. Using pywin, I installed the service but could not get it to start or provide any meaningful error logging. I went round and round on this as well. LLMs suggested using NSSM, Non-Sucking Service Manager. I agree, it does not suck, and my code now runs as a Windows Service. I’m sharing the NSSM code in case it helps somebody.

In a future post, I am going to talk about using LLMs through this process. The original code was written before they were available. Now I use them incessantly.

As I was writing this I heard a voice in my head “Did you ever check if there was an RSS feed?” There is…

1. Installing a python script as a Windows Service using NSSM
2. Open powershell as an administrator
3. Change to the NSSM.EXE working directory

Run these commands:

```
# install service
.\nssm.exe install "MyServiceName" "<full path>\venv\Scripts\python.exe" "<full path>\<python script name>.py" 

# Set up logging for service
.\nssm.exe set "MyServiceName" AppStdout "<full path>\service.log"
.\nssm.exe set "MyServiceName" AppStderr "<full path>\service_error.log"

# Set working directory
.\nssm.exe set "MyServiceName" AppDirectory "<full path>"

# Set environment variable accessed in python using os.environ 
.\nssm.exe set "MyServiceName" AppEnvironmentExtra MY_ENVIRONMENT_VARIABLE=ev_value

# Run service
.\nssm.exe start “MyServiceName” (stop, remove, etc.)
```