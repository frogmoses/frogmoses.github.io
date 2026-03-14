+++
title = 'LLM-assisted Active Directory Search'
date = 2024-09-27
draft = false
tags = ['LLM', 'python', 'active-directory', 'automation', 'PowerShell']
+++

I needed to check Active Directory (AD) to see who was part of a group. I use AD infrequently and keep a list of queries in a text file on my desktop, as I can’t ever remember the syntax.

As I opened my list I thought...wait, I don’t ever have to do this again. Let’s write a program to take a natural language prompt and have our LLM figure out the PowerShell commands. Within 30 minutes I had a functional program. It took several small iterations and these are the prompts I used. Unfortunately, I can’t share the program.

The initial prompt was:

> Create a python program that will query Active Directory based on a user's natural language query. Suggestion is to send the query to an LLM to determine the correct command(s) for Active Directory. Once the command(s) is returned, the python script should execute it. There should be a standard list of properties to return. There should be an automatic export of any returned valid data to Excel. Can use LDAP and/or Powershell AD Cmdlets. Provide the complete script to do all of these tasks. Ask any clarification questions you may have.

Asking the LLM to return any clarifications was helpful. However, it produced a functioning program with the first prompt.

> Clarifications Needed:
>
> 1. LLM Setup: Do you have the necessary LLM endpoint, API key, and deployment name?
>
> 2. Active Directory Access: Are you using LDAP, PowerShell, or both for querying Active Directory?
>
> 3. Data Format: What is the expected format of the data returned from Active Directory? This will help in parsing the results correctly.
>
> 4. Error Handling: How should errors be handled, especially if the LLM response is not a valid command or if the AD query fails?”

I responded with:

> 1. I have the LLM variables set up already as environment variables in Windows. 2. Use Powershell. 3. Data is table format, exported to Excel. 4. Errors should be handled in a Try Except clause and any exceptions printed to terminal.
>
> Question: can this code handle any query about AD? For example I may want basic user attributes, or find out all groups a user is a part of, or all users within a group.

These 2 clarifications were enough to get a robust script. The next couple of iterations were usability related.

> One more addition, enable the user to keep making queries until they enter the 'q' key to quit. Add a prompt to the input to use 'q' to quit.
>
> Add a function that if a user inputs 'help' then return a series of example queries. update the input prompt to include that help information.

That’s it. It built a great tool. Really enjoyable. There is one small thing I don’t like about this process. Over time, the LLM keeps returning the full code script on each response. It takes too long. I have yet to come up with a way to focus in on just a part of the code, without starting a new thread.

After I had this script I thought that I needed to create something for my whole team, which meant a web front-end. I decided to convert this to a Shiny app and it failed miserably. Same with trying to convert it to use the ldap3 library. I’m still working on that one.

I think the failure of these 2 approaches is because I know less about the technology behind Shiny and the ldap protocol.

Anyway, a great tool and I was reminded of Al Sweigart’s book, Automate the Boring Stuff with Python.