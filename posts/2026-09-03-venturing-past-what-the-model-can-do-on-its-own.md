# Venturing past what the model can do on its own

*2026-09-03 — AI, engineering, agents, claude-code, deepseek, opinion*

I've spent most of my development over the last year, time and tokens and energy, on custom slash commands, skills, and the scripts the agents activate. I packaged the whole thing into a plugin for Claude Code. I've always wondered if the models will get so good that the harness won't be necessary, or if the harness will get so complex, or so simple, that I can't compete with the companies building it full-time. Either way, the thing I'm building stops being an advantage. But right now, it is very, very, very needed. It's a weird space to work in: building things that are needed today but that I don't think have much of a future.

There's an active argument about this in the industry, and it has split into two camps that couldn't disagree more.

## Camp one: it all dissolves

Rich Sutton's ["Bitter Lesson"](http://www.incompleteideas.net/IncIdeas/BitterLesson.html) is the founding text here, and it says one thing: general methods that scale with computation beat hand-built structure, every time, eventually. People building agent tooling have started applying this to their own work, and the conclusions are not gentle. Hugo Bowne-Anderson [put a number on it](https://hugobowne.substack.com/p/ai-agent-harness-3-principles-for): "the architectural assumptions baked into an application today will likely be obsolete in six months when a new, more capable model is released." Han Lee [went further](https://leehanchung.github.io/blogs/2026/05/08/hidden-technical-debt-agent-harness/), arguing that agent scaffolding is hidden technical debt because "almost all of it is going to dissolve into the next generation of models." His prescription: treat anything you build on top of a model as a "90-day artifact," because "teams who treat their harness as a permanent product surface are going to spend a year ripping it out."

This is the position that should make anyone building what I'm building nervous. And it has receipts. Lee lists specific things already dissolving: tool wrappers that made APIs "LLM-friendly," planner-executor scaffolds that collapse into single reasoning passes, memory abstractions with embeddings beaten out by plain text progress files. The trend line is real.

## Camp two: it never disappears, it moves

Addy Osmani's [rebuttal](https://addyosmani.com/blog/agent-harness-engineering/) is just as direct: "as models improve, the space of interesting harness combinations doesn't shrink. It moves." His example: the context-anxiety scaffolding goes away as models improve, and in its place you need a multi-day memory policy, or a system that coordinates three specialized agents, or evaluators for design quality in generated UIs. Old scaffolding dies, new scaffolding replaces it, and the total amount of structure around the model doesn't trend toward zero. He points out that the leading coding agents ["look more like each other than their underlying models do,"](https://addyosmani.com/blog/agent-harness-engineering/) which suggests the scaffolding layer is converging into a real discipline, not evaporating.

This is the position that should make anyone building what I'm building feel justified. And for now, every better model helps me build a better harness. The thing that's supposed to make my scaffolding unnecessary is also the best tool I have for building the next version of it.

## Which is what makes DeepSeek interesting

DeepSeek recently opened up custom harness development, and the opportunity isn't to rebuild what I already have. It's to learn what actually makes a harness effective by building very niche ones — harnesses scoped to a specific job, stripped down to do that job clean, efficient, and fast. And building on a different model means I get to find out which parts of my Claude plugin were actually good ideas and which ones were just habits I never looked at twice. I wouldn't get that staying in one ecosystem.

## Both camps are right, which doesn't help

I think the dissolvers are right about the direction and the movers are right about the present. The scaffolding I'm building today will dissolve. And the scaffolding I build to replace it will also dissolve. And somewhere in between there's always going to be a version of me, or someone like me, building the next temporary thing to bridge the gap between what the model can do on its own and what the work actually requires.

The weird part isn't that my tools are temporary. Everything in software is temporary if you zoom out far enough. The weird part is that I can *feel* the expiry date getting shorter with every model release, and I'm building anyway, because right now is the only time that matters and right now the tools are needed. I've made a kind of peace with it: build things that are worth building today, accept that they're scaffolding and not architecture, and don't get attached.

The exploring isn't the model. It's the moving line between what I have to build and what I get to throw away. That line is moving faster than anyone can chart it, and all of us out here are mapping it by feel.

## Sources

- [The Bitter Lesson, by Rich Sutton (2019)](http://www.incompleteideas.net/IncIdeas/BitterLesson.html)
- [AI Agent Harness, 3 Principles for Context Engineering, and the Bitter Lesson Revisited, by Hugo Bowne-Anderson](https://hugobowne.substack.com/p/ai-agent-harness-3-principles-for)
- [Hidden Technical Debt of AI Systems: Agent Harness, by Han Lee](https://leehanchung.github.io/blogs/2026/05/08/hidden-technical-debt-agent-harness/)
- [Agent Harness Engineering, by Addy Osmani](https://addyosmani.com/blog/agent-harness-engineering/)
