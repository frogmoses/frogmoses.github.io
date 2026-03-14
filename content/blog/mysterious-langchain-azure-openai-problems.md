+++
title = 'Mysterious Langchain Azure OpenAI Problems'
date = 2024-11-08
draft = false
tags = ['LLM', 'python', 'Azure', 'debugging', 'langchain']
+++

I was banging my head on this problem for hours. Using langchain and our Azure OpenAI model, I kept getting a Value error:

```
As of openai>=1.0.0, Azure endpoints should be specified via the
`azure_endpoint` param not `openai_api_base` (or alias `base_url`).
```

I was not defining `openai_api_base` anywhere in my code. LLMs were no use but I did find the suggestion on Reddit to check if `openai_api_base` was an environment variable.

Sure enough, I had defined that months ago, never used it, and forgot it. Deleted the variable and problem solved.

Check the basics!
