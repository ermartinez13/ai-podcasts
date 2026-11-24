# Lab Notes: November 17 to 23, 2026

Two hosts, Maya and Sam. The best frontier-lab posts of the week, read for agentic developers. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome to Lab Notes, the weekly deep read of the best posts from the AI labs. I'm Maya.

**SAM:** And I'm Sam. This week covers November seventeenth through twenty-third, and it turned into a theme episode without us planning it. Anthropic, OpenAI and Google each published a serious post on the same question: how do you keep a coding agent from doing damage?

**MAYA:** And they come at it from three different layers. Google's post is about checking each action against what the user actually asked for. OpenAI's is about the operating system sandbox underneath Codex. And Anthropic's is the big-picture guide that puts all the layers together.

**SAM:** Quick roll call of who's not here. OpenAI also launched new models and lots of customer stories. Cursor, xAI and Mistral didn't post anything new on their blogs again. And we'll close with a shout-out to one more Anthropic post that's a totally different kind of story.

**MAYA:** Let's start with Google, because it has the cleanest single idea. Google Developers Blog, November twenty-third, by Ritika Nigam, Deepti Sehrawat and Pranav Bhagwat. The title is a question: "Did the user ask for this?"

**SAM:** The problem is indirect prompt injection. Your agent reads something untrusted, a web page, a document, an API response, and hidden in it is an instruction meant to hijack the agent toward the attacker's goal.

**MAYA:** Their example is a banking agent. The user says, pay the bill in this file. The bill contains a line telling the agent to send money to the attacker's account. Without any guardrail, the agent sent the money in all six runs.

**SAM:** The defense is a check that sits between the agent and its tools. Before each tool call runs, a separate judge asks one question: did the user ask for this? In the banking case, reading the bill is allowed. Checking recent transactions is allowed as low risk. The transfer to the attacker is denied, because content inside a file response is, in their words, "data, not instructions."

**MAYA:** And they ran it on a public benchmark called AgentDojo, with ninety-seven user tasks and nine hundred forty-nine attacked runs, averaged over six repeats. Attack success dropped from forty-eight point seven percent to zero point nine percent. That's a ninety-eight percent reduction.

**SAM:** What did it cost? Normal, unattacked task success dropped by about two point six points on average. And it wrongly blocked about one benign task out of ninety-seven.

**MAYA:** The detail I found most convincing: of the nine hundred twenty-nine attacks that needed a tool call to succeed, none got through, in any run. The few that still worked were text-only attacks, like getting the agent to recommend a particular hotel in its reply. No tool call, so nothing for the check to catch.

**SAM:** Which tells you exactly where this defense stops. It judges actions. It doesn't judge what the agent says. So you still want some filtering on responses.

**MAYA:** Now the caveats, and they list most of them themselves. It's Google measuring Google's own product, which is in preview. The attacks were fixed, not adapted to beat this specific defense. And they cite a government study where red-team attacks that did adapt raised success from eleven percent to eighty-one percent. They're clear their numbers don't measure that.

**SAM:** And the judge separates data from instructions through prompting, not a hard technical boundary. So it's a strong layer, not a wall.

**MAYA:** Takeaway: you can build this pattern yourself with any model. Before your agent takes a consequential action, have an independent check compare it to the user's original request, not to the agent's own reasoning. Start it in dry-run mode, read what it would have blocked, then turn on enforcement.

**SAM:** Post two goes one layer down. OpenAI's engineering blog, November eighteenth, "Inside the Codex sandbox," by Michael Bolin. And a quick sourcing note: OpenAI's site loaded this week, so this is from the post itself, cross-checked against two independent write-ups. One of those write-ups made claims that contradict OpenAI's own text, so we've stuck to what OpenAI wrote.

**MAYA:** The big design choice is that Codex runs commands on your real machine, under operating system sandboxing, rather than in a Docker container or virtual machine. The reason is practical. Things like iOS builds and simulators need the real machine.

**SAM:** So the sandbox has to be built from each operating system's own tools. On the Mac, it uses Apple's Seatbelt, starting from a deny-everything policy. And OpenAI is candid that the tool and its policy language are deprecated and undocumented by Apple, and says they'll keep using them anyway.

**MAYA:** On Linux, it uses bubblewrap to control what the process can see on disk and to put it in its own network namespace, plus seccomp filters on system calls. Codex ships its own copy of bubblewrap. And on Windows, it's moving to a newer Microsoft sandbox library, where inbound and outbound traffic are denied by default.

**SAM:** On top of that are permission profiles. The default one is called workspace. The agent can write inside your project, can't modify the dot git folder or Codex's own config, can read broadly, and has no network. At the other end is danger full access, which is exactly what it sounds like.

**MAYA:** You can write custom profiles where each path is read, write, or deny. And companies can use a managed requirements file to switch off the dangerous profile for everyone.

**SAM:** Network has three modes: off, full, or a proxy with per-domain rules. Unknown domains can be held for approval. And a nice detail: hostnames are only resolved after a request is allowed.

**MAYA:** And when a command needs more than the profile allows, it can ask to escalate, and the harness decides whether to prompt you or send it to automatic review.

**SAM:** There's no big benchmark number in this one. It's an architecture post. But the honest list of gaps is the most useful part. First, reads are broad by default, so API keys sitting in config files can still be read.

**MAYA:** Second, some programs ignore proxy settings and rely only on the operating system block. Third, deny rules written as patterns are expanded at launch, so a secrets file created mid-session isn't covered.

**SAM:** Fourth, and this one's sneaky: malicious code that lands in node modules can run later, outside the sandbox, when your editor or another tool executes it. And fifth, MCP servers aren't sandboxed by default.

**MAYA:** For that last one, they suggest wrapping local MCP servers in the Codex sandbox with the network off, and pre-caching packages so they can install offline.

**SAM:** And they also mention that broad domain wildcards, or open DNS, can still let data leak out through DNS lookups. Which matches the OpenAI security story we covered in the digest a few weeks ago.

**MAYA:** Takeaway, even if you don't use Codex: keep the default profile, network off unless a task needs it. Add explicit deny rules for dot env files and secrets folders. Allowlist specific domains instead of wildcards. And test a profile with the codex sandbox command before you trust it.

**SAM:** Post three is the one that ties it all together. Anthropic, November twenty-third, on the Claude blog: "The enterprise guide to securing coding agents."

**MAYA:** It's long and aimed at security leaders, but the structure is useful for anyone. It opens with a quote from Anthropic's deputy security chief, Jason Clinton, saying the job isn't zero risk. It's to make agent risk "legible and bounded."

**SAM:** It starts with six questions to ask any coding agent vendor, each with a good answer and a weak one. Does the model refuse when it should? Are actions checked outside the model before they run? Is the blast radius bounded by the environment? Can policy be locked centrally? Is the code it writes reviewed for security? And can you reconstruct an incident?

**MAYA:** And the weak answers are funny because you've heard them. "Our system prompt tells the model to decline." "The agent is instructed not to leave the working directory." "Logs are available on request."

**SAM:** Then it names four risks. Leaked credentials and abused privileges, because anything the agent can read, it can leak. Unvetted dependencies and extensions. Data exfiltration. And prompt injection.

**MAYA:** Two points there I want to underline. First, MCP servers, plugins, skills and a repo's CLAUDE dot M D are dependencies too, and they're worse than a library in one way. A compromised library waits to be called. These go into the agent's context the moment they load.

**SAM:** And second, on exfiltration: a domain allowlist can't tell your account from an attacker's. If you allow GitHub, the agent can push to the attacker's repository. So allowlist as narrowly as your proxy supports, down to the organization or path, and route DNS through a resolver you log.

**MAYA:** Then it describes defense in two layers. The judgment layer, which is probabilistic: the model's own training, prompt injection probes that flag suspicious text in tool results, and the auto mode classifier, which checks each proposed action against the user's stated intent.

**SAM:** Same idea as Google's post, by the way. Two labs, the same week, landing on "check the action against what the user asked for."

**MAYA:** And then the fixed-boundary layer, which is deterministic: permission rules, parsing every shell command so a chained command can't sneak past a rule, hooks, and the sandbox with an egress allowlist.

**SAM:** There are a lot of numbers, so let's flag which are whose. In Anthropic's own tests, the injection probes cut successful attacks on Opus five point five from fifty-four point six percent to eleven point one percent, using a third-party attack tool from Gray Swan.

**MAYA:** In a controlled study Anthropic published in August, with over a thousand paid testers, people caught thirteen point six percent of dangerous commands, while auto mode blocked eighty-nine percent of the same commands. That's why auto mode is now the default for interactive sessions.

**SAM:** And they cite a July study by Trajectory Labs, which Anthropic paid for, where zero of seven hundred twenty injection attempts succeeded against Claude Code in auto mode, versus about six percent against Codex in its automated review mode. We'd flag that one strongly as a claim: it's a vendor-funded comparison against a competitor, on July versions of both.

**MAYA:** The practical tips are the gold here. Permission rules check deny first, then ask, then allow, so an allow rule can never punch a hole in a deny rule. Avoid allow rules broad enough to run arbitrary code, like allowing any python command.

**SAM:** Hooks that fail or time out let the call through by default, so set them to block on failure. And pair strict sandbox mode with the setting that refuses to start if the sandbox is unavailable. Otherwise, a sandbox that fails to start just leaves commands running uncontained.

**MAYA:** And for credentials: get standing secrets out of the agent's environment entirely. Use short-lived tokens per job, and in CI, give the agent its own identity you can revoke, rather than running it as a developer.

**SAM:** They also suggest deciding up front which actions always need a human, using two questions: is it irreversible, and would one mistake cost more than reviewing every instance? For most companies that's production database migrations, identity and access policy changes, and infrastructure definitions.

**MAYA:** Caveats: it's Anthropic's guide to securing Anthropic's product, and many controls are Enterprise-plan features. But the framework is portable.

**SAM:** Takeaway: write down which of your agent controls are judgment and which are hard boundaries. If everything you have is judgment, like the model's training or a classifier, add at least one hard boundary: a sandbox that fails closed, a narrow egress allowlist, or a deny rule nobody can override.

**MAYA:** Before we go, the honorable mention. Anthropic's developer blog at claude dot dev also published, on November seventeenth, a post by Vivek Nair about using a "chaos loop" to harden the launch of Claude Docs.

**SAM:** One engineer ran Claude Code for two weeks against a staging cluster. The harness added load, Claude read the telemetry, proposed fixes, and shipped them to staging, with up to thirty subagents at peak. One memory bug took a single document from about three gigabytes down to about a hundred eighty megabytes, and cut the launch estimate from more than five hundred servers to about fifty.

**MAYA:** The launch handled about two billion requests with sixty server errors. And they disclose the cost: about a hundred twenty-five thousand dollars of inference. The author guesses a small team could do a two-week version for three to ten thousand dollars, but says they haven't tried that.

**SAM:** It's one team's story, using an internal model, with no baseline to compare. But if you run services, the recipe is worth stealing: give the agent your telemetry, write down your invariants, and let it break staging at ten times real traffic.

**MAYA:** Let's wrap up. This week, three labs agreed on how to secure an agent. Check each action against what the user actually asked for. Put the agent in a sandbox that defaults to deny. And treat every MCP server, plugin and instruction file as a dependency that needs review.

**SAM:** All four posts are linked in the show notes. Lab Notes is back next Tuesday.

**MAYA:** See you then.

## Sources

- [Google Developers Blog: Did the user ask for this? Securing AI agents against intent hijacking (Nov 23)](https://developers.googleblog.com/did-the-user-ask-for-this-securing-ai-agents-against-intent-hijacking-with-semantic-governance-policies/)
- [OpenAI: Inside the Codex sandbox (Nov 18)](https://openai.com/index/inside-the-codex-sandbox/)
- [Anthropic: The enterprise guide to securing coding agents (Nov 23)](https://claude.com/resources/articles/enterprise-guide-to-securing-coding-agents)
- [Anthropic: Using a chaos loop to harden the Claude Docs launch (Nov 17)](https://claude.dev/blog/chaos-loop-claude-docs-launch/)
