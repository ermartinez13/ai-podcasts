# AI Fortnight, the podcast: what's new, November 11 to 15, 2026

Two hosts, Maya and Sam. Covers the stories added in the November 15 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Sunday episode, covering what's new since Wednesday. Eleven new stories, and the lead is an update you should install today if you connect Claude Code to remote M C P servers.

**MAYA:** Claude Code two point one point three twenty-one fixed a bug where an M C P server could redirect an OAuth request and have your refresh tokens sent to a different host. So a malicious or compromised server could have walked off with your tokens.

**SAM:** The same release closed two more permission gaps. Bash commands that Claude Code judged read-only could run outside the sandbox without a prompt. And deny rules didn't cover files written into a directory with c p or m v. That's fixed too, including path forms like slash bin slash c p.

**MAYA:** It also makes Fable five point two the default Fable model. Then two point one point three twenty-three adds an experimental Code Mode, where Claude writes JavaScript to call its tools, makes plugins honor version ranges, and removes the subagent status line setting. And three twenty-five fixes a security issue in z standard decoding and lets compaction work through third-party gateways.

**SAM:** That's our first tip. Update to two point one point three twenty-one or later, and if you've connected M C P servers you don't fully trust, re-authorize them.

**MAYA:** Next, the attacker side again, and this time with traffic numbers. Cloudflare says more than fifty families of A I penetration testing frameworks scanned its customers within three days. Daily requests from these tools are up about thirty times since October first.

**SAM:** ARTEX and its forks, now more than twelve thousand repositories, make up over sixty percent of the A I pentest orchestrators Cloudflare knows about. Traffic actually jumped more than ten times after the original ARTEX repo was taken down, because the forks spread.

**MAYA:** And in one incident, a stolen C I token led to four hundred database dump requests in a single hour.

**SAM:** Tip two. Put M C P endpoints and admin panels behind identity checks, rate limits, and schema validation that denies by default. Assume an agent will find whatever you leave open.

**MAYA:** Let's do models. Google released Gemini four Hydrogen, which replaces the Flash line. It's a dollar fifty in and seven fifty out per million tokens, and the price stays flat up to about a million tokens of prompt. Output is capped at about sixty-five thousand tokens per call.

**SAM:** Google says it finishes tasks two and a half times faster than Gemini three point eight Flash. On the Artificial Analysis Intelligence Index it scores fifty-one to fifty-four, which is above the bigger Gemini four Argon. But on Terminal-Bench it's at fifty-four percent, against sixty-four for Claude Sonnet five point five. So for terminal-heavy agent work, test it before you switch.

**MAYA:** It's in the Gemini A P I, Antigravity, and since Friday, GitHub Copilot.

**SAM:** And a small model worth watching. I B M previewed Granite four point one LLMON models, about four and nine billion parameters. They're trained on a markup format where one block says which instruction to run and which data it applies to. Documents and tool results are treated as things to read, not commands to follow.

**MAYA:** I B M reports it avoids forty-seven percent more indirect prompt injections than the best frontier model it tested. That's I B M's number, and multi-turn adaptive attacks are still unsolved. It's learned behavior, not a guarantee, so keep your other defenses.

**SAM:** Tools. GitHub announced it will retire six models from Copilot on December fourteenth. Claude Fable five, Claude Haiku four point five, Gemini three point eight Flash, Gemini four Argon, Grok four point six, and Kimi K three.

**MAYA:** The suggested replacements are Fable five point two, Haiku five point five, Gemini four Hydrogen, Gemini four Carbon, and Grok four point seven. Kimi's replacement hasn't been named. And separately, GitHub Enterprise Server accounts now work in the Copilot app, though cloud sessions aren't available there.

**SAM:** That's tip three. Search your agent configs, prompt files and C I for those model I Ds, and rerun your evals on the replacements now, not on December thirteenth.

**MAYA:** Codex CLI zero point one sixty-eight and one sixty-nine shipped on the same day. The change that matters most: codex exec now keeps a project's config and M C P servers turned off in untrusted directories, unless you pass dash dash trust.

**SAM:** So a scripted Codex run on a repo you just cloned won't quietly load that repo's M C P servers. Only add dash dash trust for repos you control. There's also a model provider browser, side chat tabs, task search, and Windows sandbox fixes.

**MAYA:** Vercel Labs released U I S D K in beta. It's a library of unstyled interface behaviors, things like focus recovery, typeahead, popups and drag and drop, for React, Vue, Svelte, Solid and Web Components. And it ships with an agent skill.

**SAM:** The idea is that coding agents build from tested primitives instead of writing keyboard and focus handling from scratch, which they often get wrong. It's beta, so pin the version.

**MAYA:** And a reliability note. On Friday, a sign-in outage blocked claude dot ai and Claude Code for more than an hour, while the Claude A P I kept working. If you have unattended automation on Claude Code, keep an A P I key or cloud provider path configured as a fallback.

**SAM:** Two research stories that go together. A paper called Termination Lag looked at when coding agents actually solve a task. Between thirty-eight and eighty-two percent of successful runs had a correct patch on the very first source edit.

**MAYA:** But a third to more than half of all steps came after the solution, mostly re-verifying and exploring. And in one to eight percent of runs, that extra work undid the correct patch.

**SAM:** Tip four. Add a stop rule. End the run when the tests pass, or diff any later edits against the first passing patch before you accept them. You save tokens and avoid late regressions.

**MAYA:** And Google Research shared lessons from Antigravity's teamwork feature, a multi-agent harness used on Lean proofs, math and systems work. Three design rules. Use hard falsifiers, like test suites, proof checkers or simulators. Partition context so subagents don't inherit each other's mistakes. And have critics review from a clean context, without the author's reasoning.

**SAM:** That last one is easy to copy. A reviewer agent that reads the author's chain of thought tends to agree with it.

**MAYA:** One business story. Anthropic set its IPO price range at seventy to seventy-eight dollars a share, raising up to about sixty-four billion dollars at a valuation of up to one point four trillion. Trading on Nasdaq under A N T is expected around November nineteenth.

**SAM:** The filing also shows an eighty-one billion dollar revenue run rate at the end of October. Nothing changes for A P I users yet.

**MAYA:** And a quick follow-up on Wednesday's lead. TechCrunch reports the Fireworks A I incident behind the Notion chat exposure was a cyberattack through its cloud provider, its second breach in two months.

**SAM:** So, to sum up. Update Claude Code if you use remote M C P servers. Agent attack bots are now routine traffic, so gate everything you expose. And when your agent's tests pass, let it stop.

**MAYA:** All the links are in the digest, with the new stories marked. Next refresh is Wednesday morning. See you then.
