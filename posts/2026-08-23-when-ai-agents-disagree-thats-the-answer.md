# When AI Agents Disagree, That's the Answer

*2026-08-23 — AI, engineering, multi-agent, code-review, opinion*

Everyone is building consensus machines.

Multi-agent AI systems that debate, vote, and iterate until they converge on one answer. The academic literature calls it "multiagent debate," and the pitch is clean: multiple rounds of discussion ["significantly enhance mathematical and strategic reasoning"](https://arxiv.org/abs/2305.14325) and ["reduce fallacious answers and hallucinations."](https://arxiv.org/abs/2305.14325) More agents, more agreement, better answers.

I've been running multi-agent review panels on my own code for months. Consensus works brilliantly when there's a right answer. But for judgment calls — the kind that actually eat engineering time — the disagreement is where the value is. And most multi-agent architectures throw it away.

## The Problem With Pushing Toward Agreement

Here's the problem with pushing agents toward agreement: they're good at it. Too good. An analysis for [ICLR 2025 Blogposts](https://d2jud02ci9yv69.cloudfront.net/2025-04-28-mad-159/blog/mad/) found that agents in debate settings ["overly assign weight to the final answer instead of the reasoning steps"](https://d2jud02ci9yv69.cloudfront.net/2025-04-28-mad-159/blog/mad/). When one agent sees another's conclusion, it tends to cave rather than analyze *why* they diverge. The debate doesn't produce deeper reasoning. It produces faster convergence on whichever answer got stated first or most confidently.

This shouldn't be surprising. LLMs are trained on human text, and humans in group settings do the same thing. The first confident voice anchors the room. Debate rounds don't fix anchoring bias; they amplify it, because each round gives every agent more exposure to the emerging consensus.

For arithmetic, this still works. There's one right answer, and convergence toward it is genuinely useful. But for judgment calls — code review, design critique, risk assessment — there often *isn't* one right answer. There's a distribution of defensible positions, and the shape of that distribution is the thing you actually need to see.

A consensus machine flattens that distribution into a single point. A divergence detector preserves it.

## What Disagreement Actually Tells You

You can't see how confident a model really is from a single run. The model that's 90% sure and the model that's 51% sure deliver the same authoritative tone. But run the same question through five independent configurations — different models, different prompts, different harness logic — and the hidden distribution reveals itself. Five-for-five agreement means the answer was clear-cut, whereas a 3-2 split means you're looking at a genuinely hard call.

Google Brain's [self-consistency](https://arxiv.org/abs/2203.11171) work proved this decisively: sample diverse reasoning paths from the same model, take a majority vote, and you outperform any single chain-of-thought by 4–18% across benchmarks. The method works because different reasoning paths surface different correct approaches, and the right answer tends to converge while wrong answers scatter. For problems with a definite solution — arithmetic, logic, factual recall — this is genuinely powerful. More samples, more accuracy.

But here's what happens when you apply that same architecture to a judgment call: the majority vote still converges, but now it's converging on the *most common* position, not the *correct* one. There is no correct one. And the minority positions you just outvoted? Those were the interesting part: the places where the problem is genuinely ambiguous, where reasonable approaches diverge.

Self-reported confidence won't help you sort this out either. When you ask LLMs to state how sure they are, the numbers are ["almost independent from accuracy"](https://arxiv.org/html/2412.14737v2) in smaller models and [off by ~10% even in the largest ones](https://arxiv.org/html/2412.14737v2). A [separate study](https://arxiv.org/abs/2405.02917) testing GPT-4, LLaMA 2, and PaLM 2 found they're ["overconfident most of the time."](https://arxiv.org/abs/2405.02917) The model can't tell you how sure it is. But the *pattern* of agreement and disagreement across independent runs can, if you read it as a map instead of flattening it into a vote.

## The Default Architecture Has It Backwards

The standard multi-agent pattern goes: agents share context, see each other's outputs, iterate toward a unified answer. For review and analysis tasks, the architecture should be inverted.

You want agents that are *maximally independent*: different context windows, different framings, no visibility into each other's conclusions. Not so you can take a majority vote (that's just consensus with fewer rounds), but so their disagreements are *meaningful*. When two agents that share nothing reach opposite conclusions about the same code, that's not noise. That's the system telling you: this is where the ambiguity lives.

I run six-agent review swarms on pull requests. Three on one model, two on another, one on a third. Each is told to look for a different class of problem. They never see each other's output. And the single most valuable artifact is not any individual finding — it's the map of where they agree and where they split.

## Where This Gets Concrete

Two agents recently read the same twenty lines of code in one of my PRs and reached opposite conclusions. One flagged non-deterministic ordering in a database query: when two rows share a date, the result could vary between runs. The other, given full project context, said the tie case was impossible.

The disagreement sent me to a third file neither agent had focused on:

```python
unmatched_by_normalized_path: dict[str, dict[str, Any]] = {}
...
for unmatched in unmatched_by_normalized_path.values():
    db.session.add(GA4UnmatchedPath(**unmatched))
```

A dictionary keyed by normalized path. Duplicate entries are impossible by construction. The second agent was right. The first was extrapolating from what the diff alone could show.

If I'd built a consensus system, agent two would have "won" the debate, the finding would have been dropped, and I'd have moved on. Instead, because I treated the disagreement as a signal to investigate, I found the real issue: a code comment claiming the ordering mattered when the code itself was order-independent. The comment was wrong, not the logic. A smaller finding, but a true one — and one that no single agent surfaced.

Two rules came out of this, and they now govern how I run these swarms:

**Adjudicate against source, never against confidence.** When agents disagree, don't resolve it by picking the more confident one or adding a tiebreaker. Go look at the thing they disagree about. The split is a pointer, not a problem to be solved computationally.

**Maximize independence, not coverage.** The instinct is to give every agent full context so it can make the best possible judgment. But shared context produces correlated errors. An agent with *less* context that still flags the same issue is stronger evidence than two fully-informed agents agreeing — because it means the signal is visible even without the surrounding explanation.

## The Architecture That Uses Both

The point isn't that consensus is wrong; it's that consensus is *half* the system. Self-consistency proves that convergence works for convergent problems. The missing piece is what happens at the points where agents *don't* converge.

Most multi-agent architectures treat disagreement as a problem to resolve: add a tiebreaker agent, run another debate round, take a majority vote. But for judgment tasks, a well-designed autonomous system should do the opposite: treat the disagreement map as a first-class output and route those specific points for deeper investigation, whether that's a more targeted agent pass, a different analytical frame, or human attention where it has the most leverage.

The value chain is: fan out independently, let agreement confirm the clear-cut calls, then *zoom in* on exactly the spots where agents split. The agents are doing triage, sorting hundreds of lines of code into "clear" (agreement) and "ambiguous" (disagreement). That's a force multiplier whether the next step is automated or not. The key is resisting the urge to flatten the disagreement before you've extracted what it's telling you.

When you're building a multi-agent system and your agents agree, that's confirmation. When they don't, that's the system telling you the problem is harder than it looks — and exactly where. Most architectures treat that as noise. The better ones treat it as the most useful thing the system produced.

## Sources

- [Self-Consistency Improves Chain of Thought Reasoning in Language Models — Wang et al., 2022](https://arxiv.org/abs/2203.11171)
- [Improving Factuality and Reasoning in Language Models through Multiagent Debate — Du et al., 2023](https://arxiv.org/abs/2305.14325)
- [Multi-LLM-Agent Debate: Performance, Efficiency, and Scaling Challenges — ICLR Blogposts 2025](https://d2jud02ci9yv69.cloudfront.net/2025-04-28-mad-159/blog/mad/)
- [On Verbalized Confidence Scores for LLMs — Yang, Tsai & Yamada, 2024](https://arxiv.org/html/2412.14737v2)
- [Overconfidence is Key: Verbalized Uncertainty Evaluation in Large Language and Vision-Language Models — Groot & Valdenegro-Toro, 2024](https://arxiv.org/abs/2405.02917)
