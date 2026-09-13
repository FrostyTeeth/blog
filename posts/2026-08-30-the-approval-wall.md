# LLM Pipeline Architecture: The Airlock Pattern

*2026-08-30 — AI, engineering, architecture, automation, opinion*

Talking about yourself is hard. If you're a humble person and don't really think your achievements are that special, you might be tempted to hand the job to a language model. So you paste your résumé into ChatGPT, ask for a cover letter, and it comes back brimming with confidence. You led 12 teams. You spearheaded every product launch. You drove a 40% improvement in something. The prose is polished, the tone is professional, and about half of it is fiction. The truth is you coordinated *with* 12 teams and did your job well as the digital strategist on a product launch. The model doesn't know the difference. It just knows how to make statements sound impressive.

It turns out you've been using Agree-GPT, which exists to please the prompter regardless of reality. When deployed out into the wild, this is causing poor outcomes for some companies and the consequences are already showing up in court. In 2024, [Air Canada was held liable](https://www.cbc.ca/news/canada/british-columbia/air-canada-chatbot-lawsuit-1.7116416) after its chatbot fabricated a bereavement fare policy for a grieving passenger. When the passenger tried to claim the discount, Air Canada argued the chatbot was a "separate legal entity" responsible for its own actions. A tribunal rejected that defence and ordered the airline to pay damages.

[Vectara's hallucination leaderboard](https://www.vectara.com/blog/introducing-the-next-generation-of-vectaras-hallucination-leaderboard) puts even state-of-the-art models at 3% to 13% fabrication rates on grounded summarization. A [2023 study in *Scientific Reports*](https://www.nature.com/articles/s41598-023-41032-5) found GPT-3.5 fabricated 55% of its citations; GPT-4, 18%. A [2025 study across arXiv, bioRxiv, SSRN, and PubMed](https://arxiv.org/pdf/2605.07723) estimated 146,932 hallucinated citations in a single year. These are the best models available, doing their best work, and the floor is not zero. Those are last year's models, and the current ones are getting better, but they are still not reliable.

## So do we get rid of LLMs?

A few of the software development projects I'm working on require custom content delivered at the right time and place. Since the pipeline intakes raw text from external sources, an LLM is needed to classify that text and route the right response. But there was no way I was going to risk an LLM publishing content. I built the system on one important rule, and it's the same rule I'd apply to any pipeline where an LLM is part of a process that publishes content on demand: an airlock between the LLM and the outside world.

## The rule — how it works

A language model can only ever analyze incoming content. It reads inputs and returns structured data. The content that actually ships is pre-approved by a human, stored in a bank, and served by deterministic scripts. The LLM decides nothing about what goes out. It tells the scripts what came in.

The wall sits between analysis and action. On the upstream side, the LLM reads incoming content and returns structured output. On the downstream side, deterministic code uses that structured output to select from a bank of human-approved content and assemble the final document. The code that publishes can't generate prose, can't reclassify, can't override the bank. It selects from what a human already approved, or it selects nothing. That's the firewall.

This matters more than it sounds, because research on automation bias shows that humans are poor at catching AI errors after the fact. [Parasuraman and Manzey's foundational review](https://journals.sagepub.com/doi/10.1177/0018720810376055) in *Human Factors* found that automation bias occurs in both novice and expert users and can't be trained away. People accept incorrect system output (commission errors) and fail to notice when the system misses something (omission errors). A [systematic review in clinical decision support](https://pmc.ncbi.nlm.nih.gov/articles/PMC5356416/) found that 5.3% of initially correct human evaluations were switched to incorrect answers after receiving automated advice. Put a generated paragraph in front of a reviewer at the end of a busy day, and the research says they'll tend to approve it. The approval wall works because it forces the human's judgment to happen on individual claims, with evidence, before any of it enters the publishable pool.

## From input to output

An incoming request arrives — a job posting, a support ticket, a brief to analyze. The LLM reads it and returns structured data only: classifications, ranked priorities, key themes, a positioning angle. This is the step that needs a language model — keyword matching and sentiment analysis can't do the kind of contextual reading the system prompt asks for. But the model never returns prose. It returns structured fields that a script can act on.

A script takes that structured output, matches the LLM's classifications against tags on human-approved content in the bank, and assembles the final document. The text is copied verbatim — the only substitution is mechanical, template variables like `{recipient}` and `{metric1}`. No generation at the moment content leaves the building.

The content bank has its own gate: every piece in it was reviewed by a human, with evidence, before it entered the pool.

## More LLM, not less

The counterintuitive part: restricting the LLM's authority didn't reduce how much the system uses it. It actually makes *more* model calls than a naive approach would.

The LLM runs a multi-tier analysis on every incoming request. It classifies the requirements. It ranks priorities. It identifies key themes and angles. It scores fit. It flags risks. Every response is schema-constrained, screened for prompt injection on the way in, and validated on the way out. That analysis is what later lets deterministic selection choose which approved content fits this particular output. The richer the analysis, the better the match.

The model classifies and scores. It does the heavy cognitive work on the *input* side. And because each call is schema-constrained with a narrow task, you don't need the most capable model — you need the fastest one that hits your accuracy threshold. Deep-thinking models are overkill for returning a classification. Cheaper, faster models do the job, and the per-call cost drops accordingly. That constraint is narrow and specific: the LLM is focused on labelling one specific parameter at a time. That means the LLM is not going off the rails when it receives a curveball. One narrow constraint, and everything else opens up.

## When in doubt, don't send

Every uncertain moment in the system resolves toward not publishing.

Analysis doesn't resolve? No-go. A field is missing from the data? Not approved. Don't send.

That airlock is what lets the system run autonomously without a human watching each output. The human's judgment is front-loaded into the approval of individual pieces of content. Every other part of the pipeline is as automated as possible specifically *because* the publish accuracy is locked down.

## What you can copy

This isn't a single-system architecture. It's a design pattern for anywhere an LLM's analysis reaches a person. 

### The Airlock Pattern

**Separate analysis from action.** The model reads and classifies. Scripting selects the output. A hard boundary separates the two systems.

**No LLM on the output path.** The moment a language model can write what the customer reads, you've handed it a pen and hoped for the best. Just remember Air Canada's chatbot inventing a bereavement policy for a grieving customer.

**When in doubt, don't send.** Every missing value, every failed check, every ambiguous state resolves toward not publishing. If the system is going to be wrong, make it wrong in the direction that doesn't send a fabricated claim to a stranger's inbox.

The AI industry is building toward more autonomy. For the parts of the pipeline where the LLM is analyzing, classifying, and scoring inputs, I want to use the strengths of LLMs. But before content leaves the building, the system should have the initiative of a filing cabinet. It serves what was put into it. That's how you get safe and useful results.

## Sources

- [Vectara Hallucination Leaderboard](https://www.vectara.com/blog/introducing-the-next-generation-of-vectaras-hallucination-leaderboard)
- [Walczak & Cellary, "Fabrication and errors in the bibliographic citations generated by ChatGPT," Scientific Reports, 2023](https://www.nature.com/articles/s41598-023-41032-5)
- [Shen et al., "LLM hallucinations in the wild: Large-scale evidence from non-existent citations," 2025](https://arxiv.org/pdf/2605.07723)
- [Moffatt v. Air Canada (B.C. Civil Resolution Tribunal, February 2024)](https://www.cbc.ca/news/canada/british-columbia/air-canada-chatbot-lawsuit-1.7116416)
- [Parasuraman & Manzey, "Complacency and Bias in Human Use of Automation," Human Factors, 2010](https://journals.sagepub.com/doi/10.1177/0018720810376055)
- [Lyell & Coiera, "Automation bias and verification complexity," JAMIA, 2017](https://pmc.ncbi.nlm.nih.gov/articles/PMC5356416/)
