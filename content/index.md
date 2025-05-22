---
title: knowledge go brrr
tags:
  - AI
  - notes
  - gpus
  - program-synthesis
  - PL
---

## why i’m into PL + AI (and why u might wanna be too)
alright so here’s the thing.
most ppl see “programming languages” and go “ugh, compilers, formal methods, dry af.”
and then they see AI and it’s all “neural nets go brrr.”
but when u actually look closer — these two fields? they’re on a collision course, and it’s gonna be wild.

PL is not just about compilers (but also yes, compilers are cool)
when you study programming languages, you're not just learning how Python or Rust works under the hood — you're learning how we think about code.
like, how do you make sure code is correct before it runs?
how do you design a language that makes it hard to write bugs?
how do you make your computer do what you mean, not just what you said?

basically: PL is the part of CS where math nerds meet system hackers.

### AI is cool, but also lowkey unhinged
AI is obviously everywhere now — chatbots, image gen, auto-coding tools like Copilot.
but like... it’s a black box a lot of the time. it works, until it doesn’t.
and that’s a problem when you're building stuff that can’t afford to break — like aircraft software, or compilers, or even just stuff that touches real-world data.

sooo what if we took the logic brain of PL and the pattern brain of AI and mashed them together?

### enter: proof automation + program synthesis 🔥
proof automation
imagine you’re trying to prove your code is 100% correct (yeah, like math proof level correct).
before, that meant spending 47 hours in a proof assistant like Coq or Lean manually writing tactics like a monk.
but now? with a lil AI help, the assistant can actually guess what steps you might take.
it’s like autocorrect, but for theorems.

“oh you wanna prove this invariant? here’s 3 lemmas that might help, bestie.”

suddenly formal verification goes from “only for PhD types” to “yeah maybe i’ll throw that in my CI pipeline.”

### program synthesis
this is basically: “write a few rules or give an example, and i’ll write the code for you.”
like... you write down what you want, and the computer writes the how.
sometimes that’s powered by machine learning (think: Copilot, AlphaCode), sometimes it’s more logic-based (like sketching out code with constraints).

either way, it's making dev life wayyy easier — esp for boilerplate, tricky edge cases, or even learning new APIs.

### so why care now?
bc we’re at this really fun crossroads.
PL has all the rigor and safety, AI has all the scale and vibes.
and when they meet? we get tools that write better code, faster — and maybe even prove it’s right while they’re at it.

if you’re into building cool tools, automating your future self’s pain away, or just vibing at the intersection of math, code, and intelligence —
PL + AI is the move.

### why i am writing and building a digital garden ?
most of the knolwedge is generally siloed ie very discretely studied and not known about the relationships between them. while it helps in building intuition and understanding the concepts , this really harms the way in which we can truly build knowledge graphs and develop an high level graphical view of the knowledge.

another thing is the building a digital garden is beneficial in training your local LLM model to understand the base knowledge and the relationships between them to understand the underlying changes and relationships between them.
