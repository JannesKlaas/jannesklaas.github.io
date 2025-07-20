---
layout: post
title:  "Agent design lessons from Claude Code"
date:   2025-07-20 00:00:00 +0000
categories: AI
---

First, acknowledge the obvious: The last post on this blog is from 2019. Most of the other posts here are about Uni. Some are still pretty good! Others maybe less so.

In 2019 OpenAI released [GPT-2](https://en.wikipedia.org/wiki/GPT-2) as an open weights model. What a ride it has been.

Claude Code is currently the most popular and most advanced coding agent.
I will assume you already have some experience with coding agents and have used them before. I am not going to provide a how to guide here. Instead, I am interested in what we can learn from Claude Code when designing our own agents.

To understand how the agent works, I used [Seif Ghazi's excellent Claude Code Proxy](https://github.com/seifghazi/claude-code-proxy), which is very easy to set up and use to inspect the API requests the agent makes. You will see screenshots from the program throughout.

## Main Findings
What suprised me is that Claude Code's design is relatively simple. It is a standard agentic pattern for a single agent, combined with a host of tricks to enable running long sessions and well thought out tools to enable code editing.

Claude:
1. Uses simple TODO lists to plan out work
2. Uses tools and system reminders to stay on track
3. Uses sub-agents for speed and context manages.

This simplicity makes Claude so powerful. It can achieve a whole lot of tasks without having many specialized modules or components. Even many of the file editing tools should transfer well to non-code tasks, like writing or form filling. Clearly, a lot of credit must go to the model for knowing how to use these tools and for being able to follow a complex plan in one session. But there has also been great thinking here to make the most effective use of the model.

As more agents are built for any and all tasks, it is helpful to learn some lessons from the best.

## Simplicity
Claude Code is relatively simple. It is a single agent loop, with 14 tools available.
4 are command line related (bash, glob, grep, ls), 6 are about interacting with files (read, write, edit, multi edit, notebook read, notebook edit), 2 are about the web (web search, web fetch) and 2 about control flows (todo write, task).

Anthropic seems to have split out tools either because of permissions with bash requiring user approval but glob, grep & ls not requiring approval or to deal with the particulars of particular file types which are commonly used. Jupyter notebooks are very long documents when read raw, and so it makes sense to have a parser to ensure the code is easier to read and write.

But that's it. Notice how Claude Code does not use a critic pattern to review its own work, or assumes different roles. It also does not have a sophisticated memory system. It does not use any databases to represent knowledge or does anything else fancy.

## While Tool Loop
![Message Block]({{ site.url }}/assets/claude-code-message-block.png)

At it's core, Claude Code has a simple `while(tool_use)` loop, where model produces a message, if the message includes a tool call, the tool gets executed and results fed back into the model, if the message does not include a tool call, the loop stops and the agent waits for user input.

This simple pattern allows the model to e.g. ask clarifying questions by simply outputting the question as text and not calling a tool. There is no explicit way to stop the conversation such as a conversation_stop tool or a termination regex. If the agent is finished, it will usually just output a text explaining what it has done and not call tools.

## TODO Lists
To plan its work and stick to the plan, Claude Code uses TODO lists, an example tool call can be seen below.

```
{
  "name": "TodoWrite",
  "id": "toolu_01ELvCQDtLp5jMJAotucpTrE",
  "input": {
    "todos": [
      {
        "id": "1",
        "content": "Analyze current agent implementation to understand structure",
        "status": "completed",
        "priority": "high"
      },
      {
        "id": "2",
        "content": "Add streaming methods to Agent class (run_stream_async and run_stream)",
        "status": "completed",
        "priority": "high"
      },
      {
        "id": "3",
        "content": "Implement streaming API call with messages.stream()",
        "status": "in_progress",
        "priority": "high"
      },
    ]
  }
}
```

Creating the TODO list is usually the very first tool call. Over time, Claude will call the tool again to update the todo list. When it makes an update, it will provide the complete todo list again, there is no special logic about e.g. updating only a particular item.

The TODO list is often used in system hints (see below). It is also an important UX component, showing the user where Claude currently is in its work.

## Instructions in tool results
![Message Block]({{ site.url }}/assets/claude-code-tool-result.png)

A small but clever trick is that the tool results contain instructions, like not to engage with malicious files here. These instructions are fixed text appended to the tool result. By repeating them with every tool use there is likely much higher adherance to these instructions as if when they would only be in the system prompt.

This is very pronounced in the todo list write tool, which in its result reminds Claude to keep using the TODO list to keep track of its work and to now follow the next task on the list.

## System reminders
Claude Code attaches system reminders to the user message to keep the agent on track.
These system reminders are statically generated, depending on the tool called and the state of the TODO list.

E.g. at the beginning of the conversation it attaches:
```
<system-reminder>
As you answer the user's questions, you can use the following context:
# important-instruction-reminders
Do what has been asked; nothing more, nothing less.
NEVER create files unless they're absolutely necessary for achieving your goal.
ALWAYS prefer editing an existing file to creating a new one.
NEVER proactively create documentation files (*.md) or README files. Only create documentation files if explicitly requested by the User.

IMPORTANT: this context may or may not be relevant to your tasks. You should not respond to this context or otherwise consider it in your response unless it is highly relevant to your task. Most of the time, it is not relevant.
</system-reminder>
```

Then after the first user message:
```
<system-reminder>
This is a reminder that your todo list is currently empty. DO NOT mention this to the user explicitly because they are already aware. If you are working on tasks that would benefit from a todo list please use the TodoWrite tool to create one. If not, please feel free to ignore. Again do not mention this message to the user.
<system-reminder>
```

And finally, it attaches the TODO list after various steps:
```
<system-reminder>
Your todo list has changed. DO NOT mention this explicitly to the user. Here are the latest contents of your todo list:
[{class="text-green-class="text-purple-400">400">"content":class="text-green-class="text-purple-400">400">"Analyze current agent implementation to understand structure",class="text-green-class="text-purple-400">400">"status":class="text-green-class="text-purple-400">400">"pending",class="text-green-class="text-purple-400">400">"priority":class="text-green-class="text-purple-400">400">"high",class="text-green-class="text-purple-400">400">"id":class="text-green-class="text-purple-400">400">"class="text-purple-400">1"},{class="text-green-class="text-purple-400">400">"content":class="text-green-class="text-purple-400">400">"Add streaming methods to Agent class (run_stream_async and run_stream)",class="text-green-class="text-purple-400">400">"status":class="text-green-class="text-purple-400">400">"pending",class="text-green-class="text-purple-400">400">"priority":class="text-green-class="text-purple-400">400">"high",class="text-green-class="text-purple-400">400">"id":class="text-green-class="text-purple-400">400">"class="text-purple-400">2"},
...
]. Continue on with the tasks at hand if applicable.
</system-reminder>
```

These system reminders are clearly designed to solve the problem where the agent forgets its instructions or plan after many steps. Claude Code frequently takes hundreds of steps in one go, so periodically reminding it of the main control flow is clearly very important.

## Dispatching Sub-Agents
Claude Code can dispatch sub-agents to tackle individual tasks. The purpose of this is A: managing the context window and avoiding too long context and B: speed through parallelism.

The sub agents are another instance of Claude Code, with the only difference being that they themselves can't call more sub-agents (no agent-ception here). The system prompts provided to the sub agents seem to be the exact same as the main agent.

![Sub Agent Dispatch Block]({{ site.url }}/assets/claude-code-sub-agent-dispatch.png)

To dispatch the agent, Claude uses the `Task` tool, providing a description of the task, which us used for labeling the task in the UI, and a prompt, which is then passed to the sub-agent.

The sub agent receives a user prompt that is exactly what went into the prompt. It is not even informed that it is a sub-agent. It also receives the same system hints and system prompt, so it really is a new instance of Claude Code.

![Sub Agent Input]({{ site.url }}/assets/claude-code-sub-agent-input.png)

## Haiku For Security Checks
A final quite interesting find is that Claude Code sends commands which the main model is about to execute to Claude Haiku, Anthropic's smallest, fastest and cheapest model. Haiku responds with structured output. Helps Claude Code avoid bad consequences without slowing down the main loop too much. The fact that they are using Haiku means Anthropic very consciously traded off speed and accuracy here.

The human user needs to approve any bash command. But they can choose to "allow all similar", meaning these Haiku outputs are likely used to determine if user approval is needed.

System Prompt:
```
Extract any file paths that this command reads or modifies. For commands like "git diff" and "cat", include the paths of files being shown. Use paths verbatim -- don't add any slashes or try to resolve them. Do not try to infer paths that were not explicitly listed in the command output.
IMPORTANT: Commands that do not display the contents of the files should not return any filepaths. For eg. "ls", pwd", "find". Even more complicated commands that don't display the contents should not be considered: eg "find . -type f -exec ls -la {} + | sort -k5 -nr | head -5"
First, determine if the command displays the contents of the files. If it does, then <is_displaying_contents> tag should be true. If it does not, then <is_displaying_contents> tag should be false.
Format your response as:
<is_displaying_contents>
true
</is_displaying_contents>
<filepaths>
path/to/file1
path/to/file2
</filepaths>
If no files are read or modified, return empty filepaths tags:
<filepaths>
</filepaths>
Do not include any other text in your response.
```
User Input
```
Command: ls -la /Users/jannesklaas/code/jannesklaas.github.io/_posts/ | tail -10
Output: -rw-r--r-- 1 jannesklaas staff 340 Jul 20 13:01 2019-01-08-welcome-to-my-blog.markdown
-rw-r--r-- 1 jannesklaas staff 18649 Jul 20 13:01 2019-03-19-deep-reinforcement-learning-where-to-start.md
-rw-r--r-- 1 jannesklaas staff 16309 Jul 20 13:01 2019-03-19-false-discoveries-emp-bayes.md
-rw-r--r-- 1 jannesklaas staff 1211 Jul 20 13:01 2019-03-27-MFE-Core-Exam-Notes.md
-rw-r--r-- 1 jannesklaas staff 15857 Jul 20 13:01 2019-07-09-business-causal-inference.md
-rw-r--r-- 1 jannesklaas staff 8034 Jul 20 13:01 2019-08-07-signal-market.md
-rw-r--r-- 1 jannesklaas staff 7230 Jul 20 13:01 2019-11-03-xai-siren-song.md
-rw-r--r-- 1 jannesklaas staff 7038 Jul 20 13:01 2019-20-08-udacity-dend.md
-rw-r--r-- 1 jannesklaas staff 7462 Jul 20 13:01 2019-29-08-how-i-study.md
-rw-r--r-- 1 jannesklaas staff 7532 Jul 20 14:20 2025-20-07-claude-code-agent-design
```

Response:
```
"content": [
    {
      "type": "text",
      "text": "<is_displaying_contents>\nfalse\n</is_displaying_contents>\n\n<filepaths>\n</filepaths>"
    }
  ],
```

## Keeping Claude on Track
Most of these innovations are about keeping a single agent on track while peforming a long sequence of complex tasks. This allows keeping the main agent design simpler, with less need for complex scaffolding.

There is a lot I have learned from peeking into Claude Code that translates to other agentic designs I am working on.

Thanks for reading.