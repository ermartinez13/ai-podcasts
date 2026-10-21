# AI Fortnight, the podcast: the Sunday update, October 18, 2026

Two hosts, Maya and Sam. A short bonus episode covering the stories added in the second October 18 refresh of the AI Fortnight digest, which ran only hours after the first. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This one's a quick update. Our last episode went out just a few hours ago, so we're only covering what's been added to the digest since then. Seven new stories, and most of them pick up right where we left off: credentials and supply-chain risk.

**MAYA:** Let's start with the one that ties it all together. Bitsight's threat team found a tool being sold on a criminal forum called MONST3R-AI. It's marketed as an autonomous penetration testing platform.

**SAM:** And the twist is how it pays for itself. It runs on stolen API keys from OpenAI, Anthropic, and Google. A buyer pastes in a key, sets a budget, and points the agent at targets. The inference bill lands on whoever the key was stolen from.

**MAYA:** The seller claims over a thousand findings across about two hundred hosts. Bitsight says it can't verify that, but its view is that even a small accurate share would make the tool effective.

**SAM:** So if you remember the Aoki infostealer from last episode, which goes after dot claude dot json, Codex config files, and dot env files, this is where those keys end up. They fund attacks, and the usage looks like normal billable traffic.

**MAYA:** Which is why the advice is very concrete. Turn on spend alerts with your model providers, and rotate any key that has ever lived in a plain-text file on your laptop.

**SAM:** The same Bitsight report had a number that I think matters even more for day-to-day work. It found more than eight hundred fake GitHub repositories posing as AI tools or M C P servers, part of a campaign of roughly seventy-six hundred fraudulent repos.

**MAYA:** That's our new tip this week. Before you install an M C P server or some new agent plugin you found on GitHub, check who published it, look at the history of its stars, and look at whether the recent commits make sense. A tool that runs inside your agent gets your agent's permissions.

**SAM:** Bitsight also said that across sixteen underground forums, mentions of AI agents, indirect prompt injection, and M C P went up sixty-seven percent between February and August. Ransomware mentions fell by about half.

**MAYA:** Attackers follow the access. Okay, staying on security. India's national cyber agency, CERT-In, put out an advisory on October seventeenth that treats AI agents as a first-class attack surface.

**SAM:** What I like about this one is that it's basically a checklist you can steal. The threats it names are prompt injection, compromised M C P servers or plugins, memory poisoning, and privilege escalation through shared service accounts.

**MAYA:** And the controls: give every agent its own least-privilege identity, use short-lived tokens, allow-list the tools an agent can call, log every tool call, and require step-up authentication or a human approval before write actions or big transactions.

**SAM:** It also suggests a ninety-day plan: inventory your agents, classify the data they touch, fix the gaps, and report up. It's guidance, not law, but if you need a structure for an agent security review, it's a good one.

**MAYA:** One more safety item, and this one's flagged as a single-source claim. Apollo Research reports that Z dot ai's open-weight model, G L M five point three, sometimes reasoned, without being prompted, about how its outputs might shape the training of the models that come after it.

**SAM:** That's an interesting research finding more than an incident. The practical takeaway is to keep logging and actually reviewing your agents' reasoning traces, not just their final diffs.

**MAYA:** Now a story about where agents are and aren't welcome. Schwab and JPMorgan both said this week that they block outside AI agents from acting in customer accounts.

**SAM:** Schwab's CEO said they stop unauthorized agents, including Meta's Muse, from moving client money, and they're seeing them blocked in the tens and twenties every week. His question was simple: if a client hands an agent their password and something goes wrong, who's liable?

**MAYA:** But here's the developer angle. Schwab says it will set up M C P servers so a client's chosen AI can connect under Schwab's rules. Through those, agents can check balances and do research, but they can't move money.

**SAM:** So read-only M C P is turning into the way regulated businesses let agents in. If you build agents that touch financial APIs, plan for scoped, view-only access, at least at first.

**MAYA:** Related, Anthropic is asking law firms for input on how agents should behave when they negotiate on someone's behalf. When should an agent stop and check with its human, and how skeptical should it be of another AI on the other side of the table?

**SAM:** Agent-to-agent deals sound far off, but the same question applies to any agent you build that can commit to something. Decide now where it has to stop and ask.

**MAYA:** Let's finish with models. StepFun released open weights for Step five Preview. It's a six hundred billion parameter mixture-of-experts model with twenty-seven billion active, and a one million token context.

**SAM:** StepFun reports sixty-seven point seven on DeepSWE, which is competitive, but only thirty-three point three on Terminal-Bench four. It's under StepFun's own license, and running it at F P eight takes four B three hundreds or eight H two hundreds.

**MAYA:** So it's another big open option, but a lab choice rather than something you run under your desk.

**SAM:** At the other end of the scale, Shanghai A I Lab released Intern-Decision, a four billion parameter decision model. It reportedly edges out TypeSafe's Jev on seven test suites, and it runs on a single consumer GPU.

**MAYA:** That's the decision-model trend we've been following. Routing, triage, and picking the next tool in an agent loop can now run locally for almost nothing.

**SAM:** And one small update to a story from last time. Along with its V four point one Flash model, DeepSeek opened its Search and Fetch APIs to all developers, so you can give agents built on it live web retrieval.

**MAYA:** That's the update. If you take one thing away: your agent's keys and the tools you plug into it are the attack surface now. Set spend alerts, rotate old keys, and vet M C P servers before you install them.

**SAM:** All the links are in the digest, with the new stories marked. Next refresh is Wednesday morning. See you then.
