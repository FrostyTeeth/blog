# I Can't Tell Which of My Own Tools Are Helping Anymore

*2026-10-11 — AI, engineering, agents, claude-code, opinion*

I wrote custom commands, instructions, and agentic rules to prevent problems commonly caused by dumb agents. But now the agents are much better, and I probably don't need those instructions anymore.

Testing, removing them, and taking the chance that something breaks is not worth it, even though those instructions and hooks cost me tokens and time. So for now, they will stay in my Claude Code agentic workflow.

One of those tools was a brilliant (I think) idea I had a couple months ago: an agent that watches what the primary agent is doing and makes note of loose ends. I found agents were often really good at writing modules, but would frequently forget to wire them together, for example. Or they would write something important in the transcript that would get buried in scroll off page in VScode before I read them. I needed an agent to recognize those gaps and make suggestions. I called it "Sentinel".

With all the amazing possibilities of agentic coding, though, I have too many projects going on. I kind of forgot about it and assumed it was wired in, when in reality it actually wasn't. (Isn't that ironic: the tool meant to catch forgotten loose ends was itself a forgotten loose end.)

So I finally wired it in last week.

And the next day, Claude Code launched "You Should Know," an agent that does exactly the same as my Sentinel harness mod.

Now there is an official version of the thing that I made. Normally, I would use the official version. But I'm still curious to see if my design turned out good, because I like the work of designing and improving.

So I'm going to use my custom version, and I won't know if it's better or worse than the official version.

## Sources

- [cc-plugin-you-should-know: what this Claude Code mod does, by Kristina Meister (Fixter)](https://fixter.dev/blog/cc-plugin-you-should-know)
