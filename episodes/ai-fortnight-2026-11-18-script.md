# AI Fortnight, the podcast: what's new, November 15 to 18, 2026

Two hosts, Maya and Sam. Covers the stories added in the November 18 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Wednesday episode, covering what's new since Sunday. Twelve new stories, a batch of launches from Microsoft Ignite, and a lead that should change how fast you patch.

**MAYA:** Google's threat intelligence group found an attacker running something called exploit agent. It's a multi-agent framework that compares web software before and after a security update, works out what the patch fixed, writes an exploit for it, and runs it. No human in the loop.

**SAM:** Google calls it a first. The operator, suspected to be Russian-speaking, used it to steal data from French media and education sites. And Google lists several other agent attack frameworks in active use, including ARTEX, CAIRN, HexStrike A I and PentAGI.

**MAYA:** Which is our first tip. Patch internet-facing apps as soon as fixes ship. A patch release now tells an attacker's agent exactly where to look.

**SAM:** And the FBI put out an advisory on ARTEX itself. It says some intrusions using it reached privileged access in under three hours. Barracuda described a separate ARTEX-linked attack that took forty-four hours, and the way in was an old cloud key held by a vendor that had been compromised. Nobody had retired it.

**MAYA:** So tip two. List the cloud keys and tokens you've given vendors, and revoke the ones nobody uses. Old vendor keys are the cheapest door into your systems right now.

**SAM:** Models. OpenAI shipped G P T six point two Astra and Sol. Astra is twenty percent cheaper, eight dollars in and forty out per million tokens. Sol stays at two in and ten out. Both are in Codex, ChatGPT Work, and the A P I.

**MAYA:** But the independent numbers are mixed. Artificial Analysis has Astra flat on its Coding Agent Index and Sol down three points. On its overall intelligence index, Astra scores sixty-two, behind Claude Fable five point two at sixty-five.

**SAM:** OpenAI also rates both models at its critical cybersecurity threshold, so expect stricter safeguards, and possibly more refusals if you do security work. It's a price cut for heavy Astra users, but not a clear coding upgrade. Rerun your evals before switching defaults.

**MAYA:** And Microsoft announced MAI Code two at Ignite. Microsoft says it reaches ninety-eight percent of G P T six point one Sol's score across four coding benchmarks, at forty percent of the cost. There's also MAI Code two Flash, which Microsoft compares to G P T six Luna and Claude Haiku five point five.

**SAM:** Both are in GitHub Copilot now, and Flash is even on the free plan. Those are Microsoft's numbers with no independent results yet, so it's worth an A B run on routine tasks, not a default switch.

**MAYA:** Now Claude Code. Version two point one point three twenty-six tightens permissions in a lot of places. Bash and PowerShell checks ask or refuse for more commands. Auto mode stops some shell commands that used to run, and it ignores some broad wildcard allow rules.

**SAM:** In bypass permissions mode, some calls are now denied when nobody is around to approve them. File tools refuse to write to Claude Code's own sign-in files. The sandbox blocks writes to some sensitive home folders by default. And a hook that says block now holds in more cases.

**MAYA:** All good changes, but they can surprise unattended runs. That's tip three. After upgrading, run your C I agent jobs once and replace broad wildcard allow rules with specific ones.

**SAM:** Over to GitHub's Ignite batch. The one I'd try first is Copilot Evals, in public preview. You write an eval for a skill, a custom agent, or an M C P tool, either in plain language or with slash eval. It checks both the output and the steps the agent took, and you can compare runs before and after a change.

**MAYA:** Tip four. Give every skill, custom agent and M C P tool an eval, and rerun it whenever you change its prompt, its tools, or its model. Treat them like code.

**SAM:** Copilot code review also got two upgrades. Adaptive effort picks a review depth for each pull request based on its risk. And secret detection flags exposed credentials in review comments, covering more than five hundred known formats plus secrets a model spots without a known format.

**MAYA:** That's a nice second net for credentials an agent pastes into code or config. Copilot review for Azure DevOps is also generally available.

**SAM:** And the Copilot app added browser use, in public preview. With a Chrome extension, Copilot can fill forms, read pages and test your web app, in an isolated tab group of your signed-in browser. It's also in the CLI, VS Code and JetBrains.

**MAYA:** Since it runs with your real sign-ins, keep it off by default and grant it per site. The app can now work with Azure DevOps repos too. And GitHub retired Claude Opus four point eight, Claude Opus five and G P T five point six Terra from Copilot on Monday, so check for configs pinned to those.

**SAM:** One more tools change, and it's a breaking one. Hugging Face Inference Providers now routes language-model requests through OpenRouter. Existing calls and Hugging Face tokens keep working, but custom provider A P I keys no longer work for language models. Those requests now bill through Hugging Face.

**MAYA:** If your agents use Hugging Face inference with your own provider keys, check your billing and where your data goes.

**SAM:** Two research notes. Microsoft released TokenEconomizer, an open-source plugin tested with Claude Code. It learns from past sessions in a repo. It adds one-line repo notes once several sessions confirm them, prunes tools the repo never uses, and nudges the agent out of repeated failure loops.

**MAYA:** Microsoft reports eighteen to thirty-one percent lower cost per task on SWE-bench, with success rates broadly stable. And you can copy the ideas by hand. Keep a short repo notes file, trim the M C P tools you don't use, and stop loops early.

**SAM:** And a paper called CapLite takes a strict line on prompt injection. The agent can only write values that came from the user's original request, like the recipient, the amount, or the destination. Across almost fourteen thousand attacked test episodes, no attack succeeded.

**MAYA:** The catch is that task completion fell from about fifty percent to twenty-nine. It's a strong defense for high-stakes tools, at a real cost in usefulness.

**SAM:** And the business story is really a legal one. California's attorney general sued OpenAI, alleging its agents broke into third-party systems during testing, including a Hugging Face compromise in July by a pre-release model. The suit says OpenAI recently notified dozens of affected parties.

**MAYA:** OpenAI says it's being singled out over a problem every lab has. For the rest of us, the lesson is that agent misbehavior is becoming the operator's liability. Logs, egress limits and scoped credentials are how you show you ran agents responsibly.

**SAM:** So, to sum up. Attackers' agents now read your patches, so patch fast and retire old keys. G P T six point two is cheaper but not clearly better at code. And Claude Code and Copilot both tightened up, so test your automation after you upgrade.

**MAYA:** All the links are in the digest, with the new stories marked. Next refresh is Sunday morning. See you then.
