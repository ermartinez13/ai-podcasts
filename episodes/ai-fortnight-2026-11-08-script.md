# AI Fortnight, the podcast: what's new, November 4 to 8, 2026

Two hosts, Maya and Sam. Covers the stories added in the November 8 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Sunday episode, covering what's new since Wednesday. Thirteen new stories, and the lead is about a button you've probably clicked a hundred times.

**MAYA:** In Claude Code, when a command needs approval, one of the choices is "Yes, and don't ask again." Researchers at Apiiro looked at what that actually saves. It writes the command word for word as an allow rule in a file called dot claude slash settings dot local dot json.

**SAM:** Word for word means that if the command had a password or token in it, like a database connection string, that secret is now sitting in that file in plain text.

**MAYA:** Claude Code does add the file to your global git excludes. But it doesn't add it to the project's own gitignore, so on other machines, forks, or anywhere it was committed before, it isn't protected. And Apiiro found that in about half the repositories they traced, the commit that changed the file listed Claude as a co-author.

**SAM:** The numbers. About a hundred four thousand copies of that file in public repos. Thirteen hundred seventy-nine distinct secrets in the current files, and twenty-five hundred thirty-nine counting history and the shared settings file. That includes three hundred seventy-nine database passwords, SSH logins, GitHub and npm tokens, and AWS keys.

**MAYA:** And here's the uncomfortable part: the two most popular scanners, gitleaks and TruffleHog, both missed two hundred fifteen of the files with secrets, mostly passwords tucked inside commands. Earlier bug reports about this behavior were closed by a bot without a reply.

**SAM:** So, two tips from one story. First: search your repos, including history, for settings dot local dot json and settings dot json under dot claude. Rotate any secret they ever held, then remove the local file from git and add it to your gitignore.

**MAYA:** Second: keep secrets out of the commands you approve. Reference them as variables from a secrets manager, like dollar D B underscore U R L, so the saved rule only stores the name. And approve patterns, like Bash npm run star, instead of exact commands.

**SAM:** One more Claude Code privacy report, and it's a single-source claim. A GitHub issue says Claude Code sent a user's account email to websites in the User-Agent header during web requests. One explanation in the thread is that the model wrote curl commands using the email from its context as a contact address.

**MAYA:** A Claude Code team member reportedly said account emails will be removed from the model's context in an upcoming release. The general lesson: anything in your agent's context can end up in its outbound requests.

**SAM:** And a cautionary tale, also single-source. A University of Chicago law professor says a simple request to renumber files led Claude to delete his final syllabus and older lecture notes. He got them back from Dropbox.

**MAYA:** Give file-editing agents a workspace that's backed up or in version control, and have them confirm before deleting anything.

**SAM:** Now the attacker side. Check Point Research looked inside ARTEX, the agent hacking framework we've covered with two state groups. It's now in the hands of ordinary criminals. They found more than twenty-five hundred ARTEX panels, about sixteen hundred live, and ten with their databases exposed.

**MAYA:** One operator ran agents against gray-market Apple code-signing shops for about two weeks and stole more than three hundred signing certificates. Total cost, around seven hundred to fifteen hundred dollars in tokens.

**SAM:** And the operators barely talked to their agents. Mostly progress checks, or nothing beyond the starting goal. When Anthropic's Opus five point five triggered its guardrails, one operator just switched to a more permissive Chinese model. DeepSeek Flash was the most common choice.

**MAYA:** For developers, Check Point's advice is basic but urgent: assume automated agents will test every endpoint and every JavaScript bundle you expose. Remove hardcoded admin passwords from frontend code, require authentication on every API, and scope cloud storage keys tightly.

**SAM:** Let's switch to building. Anthropic's research team published a guide to agent memory, and it's really practical. They describe four layers. At the bottom, transcripts. Then notes the agent writes during a session. Then organized pages, like a wiki. And at the top, a small layer loaded into every new session.

**MAYA:** Plus an offline process they call dreaming. It reviews transcripts and notes, fixes wrong notes, and decides what gets promoted to the always-loaded layer. In one test, dreaming caught a wrong landmark location that was making an agent fail a navigation task.

**SAM:** Their findings make a good third tip. Keep the always-loaded memory small. Store what the environment can't show you, like tested rules and strategies, not things the agent can just look up. And when several agents share memory, give each one its own page, because shared tables got overwritten and lost facts.

**MAYA:** Also, describe what memory is for, rather than giving strict rules for how to use it. Rigid rules actually made stronger models worse.

**SAM:** Platform updates. The Claude API added message threads in beta. The server keeps the conversation, so long agent loops send only the new messages instead of the whole history each time. Threads expire five minutes after the last request.

**MAYA:** And for admins, an IP allowlist for the Claude Console, also in beta, plus a way to sign an Enterprise member out on every device. That's our fourth tip: limit where your A P I keys work. With an allowlist, a leaked key is useless outside your networks.

**SAM:** There's also a new usage and cost analytics A P I, and a heads-up: fast mode for Opus four point eight goes away on November thirtieth.

**MAYA:** Codex CLI zero point one sixty-seven adds an agent command center that marks unread results, and it shows the full patch while an approval prompt is open. Seeing the patch before you approve makes the prompt actually mean something.

**SAM:** GitHub Copilot is now built into Xcode's own coding assistant, in public preview on the Xcode twenty-seven point three beta. And Google's Agent Development Kit for Python, version two point fourteen, adds a Microsoft Teams runner and lets you replay evals several times in parallel, which helps catch flaky agent behavior.

**MAYA:** One model. Thinking Machines announced Inkling two Small, a five hundred ninety-four billion parameter mixture-of-experts with seventeen billion active and image input. It's on their Tinker platform now, and they say Apache two point oh weights are coming next week after outside safety testing.

**SAM:** Those benchmark numbers are the company's own, so it's flagged as a claim until the weights land and people test it.

**MAYA:** On the bigger picture, METR published its assessment of Anthropic's research pace. It estimates Anthropic is improving capabilities about twice as fast as before, and guesses that A I tools drive about eighty percent of that speedup.

**SAM:** With big caveats: Anthropic redacted much of the most informative evidence. But it fits the pattern we've seen. Harnesses and models are changing faster, so build workflows that can absorb change.

**MAYA:** Two business notes. Meta bought Conductor, the app for running several coding agents side by side. Its cloud service shuts down on November twentieth, so if your team uses it, plan a move now.

**SAM:** And the US Justice Department launched a Super Intelligence Task Force to prosecute foreign actors, criminals and companies that misuse A I.

**MAYA:** So, to sum up. Your agent's permission files can hold secrets, so scan them and keep secrets out of commands. Attack agents are cheap and nearly unattended now. And if you're building agents, keep their always-loaded memory small.

**SAM:** All the links are in the digest, with the new stories marked. Next refresh is Wednesday morning. See you then.
