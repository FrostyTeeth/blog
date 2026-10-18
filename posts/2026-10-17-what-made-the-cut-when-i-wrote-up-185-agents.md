# What Made the Cut When I Wrote Up 185 Agents

*2026-10-17 — AI, engineering, agents, claude-code, case-study, writing*

A product I develop and maintain at my day job had been forked into two separate repositories five months earlier: one for the core architecture, one for a feature build. I'd developed both, and both had kept moving. The job was to merge them back into a single codebase — roughly 350,000 lines of changes across the two histories.

I used Claude Code with a custom plugin I'd built for managing multi-agent sessions, set up the merge plan, and started a long-running agentic task. When I came back, the agents had merged 19 pull requests and logged 26 decisions on their own. Three decisions were set aside for me. The rest they just handled.

Most of my agent work is greenfield: build something new, see if the output is good, iterate. This was different. The end state was already defined — two codebases had to become one, and there was a correct answer you could check against ten thousand existing tests. That kind of verifiable outcome is rare in my agentic work, and it made the run worth studying properly.

The stretch where I wasn't prompting was long enough to be a surprise. Not a bad one — more an awareness that my tools and skills are further along than I'd been giving them credit for.

So I wrote it up as a case study. I gave the repos code names, picked a structured template, and started working through the session logs.

The valuable part wasn't the finished study. It was what the data showed that I wouldn't have caught from impressions alone, and how that changed the way I set up agent sessions going forward.

Read the case study: [Running the Unfork with Parallel Agents](https://steve-glen.com/case-studies/unfork-case-study/).
