# AI Fortnight, the podcast: what's new, October 18 to 21, 2026

Two hosts, Maya and Sam. Covers the stories added in the October 21 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Wednesday episode, covering what's new since Sunday. Ten new stories, and the big one is a Reuters investigation that shows what agent-driven hacking actually costs now.

**MAYA:** Let's go straight there. Reuters, working from research by Snorre Fagerland at the security firm NorForge, describes a Chinese-speaking hacker who broke into more than a hundred websites using AI agents.

**SAM:** And the agents were the familiar ones. The campaign appeared to use Claude Code and DeepSeek, running through exposed instances of Cairn, an open-source AI problem-solving platform. Fagerland found it while scanning the internet for Cairn servers that were open to anyone.

**MAYA:** Starting September twenty-fifth, the agents tried more than twelve hundred e-commerce sites in the US, Canada, Australia and Japan. A successful break-in took about twenty-three hours, running on its own. The hacker's instructions were short, under a hundred Chinese characters.

**SAM:** Victims Reuters identified include Deere, SharkNinja and Cummins. Total spend was about five thousand dollars in tokens. That works out to roughly fifty dollars per successful breach.

**MAYA:** One caveat. Reuters couldn't determine how much data was actually taken. Deere said it saw no sign that sensitive information was accessed, and SharkNinja said the breached site only held product support content.

**SAM:** But the economics are the story. When a breach costs fifty dollars, attackers can afford to try everything. For developers, that means patch faster, rate-limit your public endpoints, and never leave an agent platform reachable from the internet.

**MAYA:** Which connects to one of our tips this week. Last time we talked about Archon, the coding agent with an unauthenticated control API. The Cairn case is the same lesson at scale. If you self-host an agent platform, bind it to localhost and put real authentication in front of it.

**SAM:** Now the defense side. Microsoft previewed new controls in Microsoft three sixty-five E seven and something it calls Project Perception. Every agent gets a continuous risk score, based on things like what data it can reach and whether its actions drift from the task it was given.

**MAYA:** And the responses are graduated. As risk goes up, admins can take away an agent's ability to make changes while keeping read access, require a human to approve high-stakes actions, or shut the agent down completely.

**SAM:** The part developers should notice: Microsoft's detection now covers sixty agent types on employee computers, up from twenty-five, and that list includes Claude Code, Codex and GitHub Copilot. It's in private preview, with wider availability planned for Ignite in mid-November.

**MAYA:** So your security team may soon be able to see and score the coding agents on your laptop. Keeping their permissions tight is how you avoid tripping containment in the middle of a task.

**SAM:** Also on defense, a story from earlier in the month that we hadn't covered yet. Anthropic's OSS Scanner gives maintainers of critical open-source projects free, recurring vulnerability scans by its most capable models, in a sandboxed virtual machine with no outside network.

**MAYA:** Reports can include a reproduction, an explanation of when the bug was introduced, and sometimes a proposed patch. And there's a telling number. Over six months, the models surfaced more than twenty-nine thousand candidate bugs. Humans had reviewed about six thousand, and five hundred and sixteen had been patched upstream.

**SAM:** It's the same pattern as the Postgres delay we covered on Sunday. Finding bugs is getting cheap. Fixing them is the bottleneck. If you add an AI scanner or reviewer, budget human time for triage.

**MAYA:** Okay, tools. Claude Code shipped several releases, two point one point two ninety-five through three oh five, and there's a lot in them for safety.

**SAM:** The one I'd turn on today is a new hook setting, on failure block. Normally, if a command or HTTP hook crashes or times out, the action goes ahead. With this setting, a broken hook blocks the action instead. That's our first tip this week: make your guard hooks fail closed.

**MAYA:** There's also a guided auto-mode setup command that reads your project and recent sessions to tune permissions, and a command that compares a Managed Agents configuration with Anthropic's security guide without changing anything.

**SAM:** Plus a safety prompt before rm dash r f on mounted drives, and Code Review now has Quick, Standard and Deep levels, with an option to review every repository in a GitHub organization.

**MAYA:** One thing to be careful with. A new Linux setting allows nested user namespaces, which some tools like Chromium or rootless podman need. The changelog itself warns that it can bypass the sandbox's file protections. So leave it off unless you really need it.

**SAM:** Over at GitHub, the Copilot model policy API is now generally available. Enterprises, orgs, teams and apps can read and set which models are allowed through REST, so model choice can be managed as code.

**MAYA:** And on the same day, GitHub retired six Copilot models: G P T five point five, G P T five point four, G P T five point four mini, G P T five mini, Gemini three point seven Flash, and Grok four point five.

**SAM:** The suggested replacements are G P T six point one Sol, G P T six Luna, Gemini three point eight Flash and Grok four point seven. That's another tip: check your scripts, C I and Copilot policies for anything pinned to a retired model. Admins may need to switch on the replacements.

**MAYA:** And DeepSeek open-sourced DeepInfer, the serving stack it uses in production, under Apache two point oh. It's built for V four point one Flash and supports Nvidia's newest GPUs and Huawei's Ascend chips.

**SAM:** Models now. MiniMax launched M three point one Flash, and the pricing is aggressive: fifteen cents in and sixty cents out per million tokens, with cached input at a cent and a half.

**MAYA:** MiniMax reports seventy-three point seven percent on DeepSWE and sixty-one point seven on OSWorld version two, and says agent tasks cost seventy percent less than its previous model. It's on the API and MiniMax Code now, with weights promised later. Those are the company's own numbers.

**SAM:** Fun detail: OpenCode said this was the mystery "Space Bunny" model its users had been testing. If you run lots of subagents or computer-use steps, it's worth benchmarking on your own tasks.

**MAYA:** Then Inception announced Mercury three, a diffusion language model. Instead of writing one token at a time, diffusion models refine a whole block of text at once, and Inception claims more than a thousand tokens per second.

**SAM:** Quality claims are Inception's own, so treat them carefully. But for agent steps that are bound by latency, like quick edit-and-test loops, that kind of speed could matter a lot.

**MAYA:** And OpenAI says it's improving ChatGPT's coding in older languages like COBOL and Fortran, with new evaluations for software engineering and COBOL migration. Legacy modernization is turning into a real agent use case.

**SAM:** Last one, on policy. The Department of Homeland Security ordered federal civilian agencies to remove DeepSeek products and stop buying them. Importantly, the order also covers third-party tools built on DeepSeek models.

**MAYA:** So if you sell software to US agencies, check whether any agent or feature in your product calls a DeepSeek model, even indirectly.

**SAM:** Our fourth tip carries over from Sunday because it's still the easiest win: vet any M C P server or AI tool before you install it. Check the publisher, the history of its stars, and its recent commits. Bitsight found more than eight hundred fake GitHub repos posing as AI tools or M C P servers.

**MAYA:** So, to sum up. Agents are now cheap enough for attackers to run at scale, defenders are adding risk scores and kill switches, and the harnesses are getting better at failing closed. Make sure yours do.

**SAM:** All the links are in the digest, with the new stories marked. And if you'd rather listen in your podcast app, the digest page now links to the feed. Next refresh is Sunday morning. See you then.
