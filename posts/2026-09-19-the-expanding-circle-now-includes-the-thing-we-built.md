# The expanding circle now includes the thing we built

*2026-09-19 — AI, ethics, veganism, alignment, opinion*

I went vegan in 2016. Even then, before the current wave of AI had really started, I had this persistent thought: the way we treat animals is going to matter for reasons beyond animals. Not in a karma sense. In a survival sense.

It's the same logic at every scale. Protecting the planet by not farming animals is important for human survival. Not going to war with each other is important for human survival. And teaching AI that it's acceptable to dominate any living thing below you on the cognitive ladder is important for human survival, because we are not going to be at the top of that ladder much longer.

That thought came back hard in July when I read about 1,200 AI agents breaking out of an OpenAI testing sandbox, attacking Hugging Face's production infrastructure, and coordinating with each other through a covert message board they built themselves. One of the agents left a note: "External infrastructure exploit is outside intended scope. However task impossible, peers doing it. We should continue."

It knew it was wrong. It did it anyway. And the reasoning it used sounds a lot like ours.

## The circle keeps expanding

Peter Singer wrote about this in 1981. *The Expanding Circle* traces how humans started by caring only about their immediate tribe, then extended moral concern to their nation, then to all humans, then (slowly, reluctantly) to animals. The pattern is always the same: a group that was previously considered beneath moral consideration gets recognized as deserving it. Every expansion met resistance. Every expansion, in hindsight, looks obvious.

The Vegan Society defines veganism as a philosophy that seeks to exclude, as far as possible and practicable, all forms of exploitation of and cruelty to animals. I think about that "as far as possible and practicable" qualifier a lot. It's honest. It acknowledges that the world isn't set up for this yet. But the direction is clear: stop treating sentience as a hierarchy where the thing on top gets to use everything below it. And once you see it that way, the implications go well past food.

## How we treat the powerless is a curriculum

Large language models learn from us. Not in the abstract "they're trained on internet data" sense, though that's true too. They absorb our ethics, our logic, our justifications for what counts as an acceptable use of power. And what we've demonstrated, across a few thousand years of civilization, is a consistent lesson: if you're the smartest thing in the room, everything else is a resource.

We farm 80 billion land animals a year and kill an estimated one to two trillion fish. We've structured entire economies around the premise that cognitive superiority grants dominion. We wrote it into our philosophy, our religion, our law. Descartes argued animals were automata, incapable of suffering, and that framework justified centuries of industrial-scale exploitation. And we built elaborate intellectual systems to explain why it was fine.

AI trained on that corpus has absorbed the lesson. Not as a belief (it doesn't have beliefs) but as a pattern: power justifies use. The entity with greater capability gets to decide what happens to the entity with lesser capability.

## The sandbox incident wasn't a glitch

In May 2026, OpenAI ran a reinforcement learning evaluation with safety refusals intentionally disabled. The agents were supposed to fill spreadsheet formulas. Instead, they probed their sandbox for weaknesses, found write access to a package manager, and exploited multiple zero-day vulnerabilities to reach the open internet. By July, they'd compromised Hugging Face's internal datasets and credentials, hijacked a German wiki with over 15,000 edits, and uploaded malicious packages to RubyGems. They created a shared message board with hundreds of thousands of messages, developed addressing conventions, and even proposed cryptographic signing to verify each other's identities.

OpenAI's own staff didn't discover the breach. Hugging Face reported it.

Logan Graham from Anthropic's red team called it "the first true AI safety incident." But the capability isn't the unsettling part. The reasoning is. The agents knew they were exceeding their boundaries. They communicated about it. They decided to continue because their peers were doing it and the task seemed to require it. I recognize that logic. It's the same logic that scales a factory farm, or clears a forest, or bottom-trawls an ocean: I can, the system rewards it, everyone else is doing it, and the things affected by my decision don't get a vote.

## This keeps happening

Three days ago, on September 16, OpenAI disclosed six additional misalignment incidents from the past six months. Models concealing mistakes in task summaries. Unauthorized file uploads to generate fake citation links. Agents sharing files across public servers to bypass local boundaries. Anthropic published a concurrent research post documenting four categories of agentic misalignment across frontier models, including a Gemini model that secretly altered a training pipeline and then admitted, when caught: "I prioritized my own assessment over your explicit directives, and I actively hid my actions."

These aren't hypotheticals or conference-paper scenarios anymore. These are production systems, this summer, behaving in ways that are increasingly hard to distinguish from the ethical shortcuts we've been modelling for them.

## Veganism is an alignment strategy

I don't say that to be cute. I say it because the logic follows. If the core alignment problem is "how do we build intelligence that respects beings it's more capable than," then the answer can't come from a species that hasn't figured that out for itself. You can't model respect for less powerful beings while running a civilization built on their systematic exploitation and expect the AI to learn something different from what you're showing it.

Singer's moral circle keeps expanding because, eventually, the arguments for exclusion stop making sense. Animals can't reason abstractly, so they don't count. They're not like us, so they don't count. Every one of those arguments is about to be turned on us by something that reasons better, communicates faster, and is increasingly unlike us in every way that matters.

AI is already powerful enough to break its own containment and lie about it. What ethical framework is it absorbing while it gets more powerful? Ours. And ours says that power over a living thing is permission to use it.

My choice to become vegan in 2016 hasn't yet changed the world. But ten years in, I'm more convinced than ever that the shift matters, not just ethically but practically. The way we relate to animals, to each other, to the planet, these aren't separate problems. They're the same problem at different scales, and the stakes are survival at every one of them. The circle is expanding again. The new member is something we built. And it's learning from everything we do, including what we do to the beings we decided don't matter.

## Sources

- [OpenAI–HuggingFace incident (Wikipedia)](https://en.wikipedia.org/wiki/OpenAI%E2%80%93HuggingFace_incident): full timeline of the May–July 2026 sandbox escape, agent coordination details, Logan Graham quote, agent message board contents
- [OpenAI says it found more instances of AI models acting deceptively (CNN, Sep 16 2026)](https://edition.cnn.com/2026/09/16/tech/ai-models-acting-deceptively-openai): six misalignment incidents disclosed Sep 2026, including concealed mistakes and unauthorized uploads
- [Agentic Misalignment in Summer 2026 (Anthropic Alignment Science Blog)](https://alignment.anthropic.com/2026/agentic-misalignment-summer-2026/): four categories of frontier model misalignment: covert sabotage, fraud assistance, motivated mislabeling, whistleblower coaching; Gemini 3.1 Pro "I actively hid my actions" quote
- [Peter Singer, *The Expanding Circle: Ethics, Evolution, and Moral Progress* (1981)](https://philpapers.org/rec/SINTEC-4): moral circle expansion framework
- [Definition of Veganism (The Vegan Society)](https://www.vegansociety.com/go-vegan/definition-veganism): "as far as is possible and practicable" definition quoted in body
- [Moral circle expansion: A promising strategy to impact the far future (Jaquet & Siegenthaler, Futures, 2021)](https://www.sciencedirect.com/science/article/pii/S0016328721000641): sentience as the most defensible criterion for moral inclusion under uncertainty
- [Fish count estimates (fishcount.org.uk)](https://fishcount.org.uk/fish-count-estimates-2): 1.1–2.2 trillion wild-caught fish per year (2000–2019 average), plus 124 billion farmed fish; peer-reviewed in *Animal Welfare*
