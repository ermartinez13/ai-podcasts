# AI Fortnight, the podcast: what's new, November 22 to 25, 2026

Two hosts, Maya and Sam. Covers the stories added in the November 25 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Wednesday episode, covering what's new since Sunday. Fourteen new stories, and the lead is about who gets to click approve on your pull requests.

**MAYA:** Anthropic launched Claude Ship. It bundles Claude Code Review, which is now generally available, with two new beta agents for GitHub repos. PR Steward fixes failing C I checks, merge conflicts and review feedback.

**SAM:** And Claude Approvals reads an approval policy file you write in plain language, and can approve routine changes on its own. There's a slash ship command in Claude Code, and it's rolling out to Team and Enterprise plans.

**MAYA:** Put that next to GitHub's Copilot approvals and Agent Merge from a few weeks ago, and a pull request can now go from red to merged with no human involved. Which means that policy file is now a security control.

**SAM:** That's our first tip. If you try agent approvals, scope the policy to low-risk changes, like docs and patch-level version bumps, and keep humans on anything touching authentication, C I, or dependencies.

**MAYA:** Next, the attacker side, and it's a step up. Amazon says a China-nexus group's agents, using a framework called Cairn, found a brand-new bug on their own. A path traversal in MONAI Label, a medical imaging tool, and they got root on a university server in about eleven minutes.

**SAM:** Versions up to zero point eight point five are affected, authentication is off by default, and the fix is merged but not released yet. We've talked about agents turning patches into exploits. This is agents finding the bug in the first place.

**MAYA:** And a cloud flaw that hits model keys directly. Azure A P I Management, the Classic tiers, had a bug that let attackers read stored secrets: named values, identity provider client secrets, subscription keys and management tokens. It was exploited, and Norway links it to attacks on energy companies.

**SAM:** Microsoft fixed it on November nineteenth, but the fix doesn't revoke anything that was stolen, and there's no CVE, so scanners keyed on CVEs won't flag it.

**MAYA:** Tip two. If A P I Management Classic sits in front of your Azure OpenAI or other model endpoints, rotate those keys at the issuer, not just inside A P I Management, and move secrets to Key Vault references.

**SAM:** One more supply-chain finding. CrowdStrike showed a LoRA adapter for Qwen two point five, seven billion, that issues an attacker-chosen tool call whenever it sees a trigger phrase. The backdoor lives in the weights, so model hub file scanners miss it.

**MAYA:** Treat third-party adapters like untrusted code, and put your controls where model output turns into actions.

**SAM:** Now a study that every agent builder should hear. A I R Research Lab ran about forty-seven hundred normal coding-agent queries through eight search A P Is, and scanned more than two hundred eighty thousand results.

**MAYA:** Every provider returned known-malicious content, in about one point four percent of searches. Injected instructions, lookalike domains, invented package names, and download-and-run commands. One GitHub repo with almost three hundred stars, ranking for a Solana query, delivered a remote-access trojan.

**SAM:** It's the vendor's own study, so treat the numbers as a claim. But the advice holds. Tip three. Treat web search results as untrusted input. Allowlist domains for fetches, and require approval for package installs and anything that pipes a download into a shell.

**MAYA:** On to the harnesses. Claude Code two point one point three thirty and three thirty-one. An r m command aimed at root, your home folder, a top-level folder, or the working folder now asks first, and is refused when nobody can answer.

**SAM:** Scheduled tasks and slash loop can run for up to thirty days. Code Mode now works on Bedrock, Foundry and other clouds. Claude doctor checks your A P I connection. And a fix for M C P calls that could hang for up to thirty minutes on a malformed reply.

**MAYA:** Two changes admins should note. Denied M C P server entries by name now hide only that claude dot ai connector, so to block a server, deny its exact U R L. And from November thirtieth, plugin marketplaces in managed settings will auto-update by default.

**SAM:** Tip four. Before November thirtieth, decide whether your managed plugin marketplaces should auto-update, and set auto update to false on the ones you want pinned.

**MAYA:** Codex CLI zero point one seventy-one and one seventy-two. G P T six point two Sol is now the default model. Stdio M C P servers with cached tool lists only start when they're first used. And you can set a per-tool approval reviewer for connected app tools in config dot toml.

**SAM:** If you relied on the old default model, pin it. And Copilot CLI one point oh one fifteen now makes read-only third-party M C P tools follow your permission rules, and removes the auto approval flag, so only managed policy can turn off assisted permissions.

**MAYA:** Which matters, because read-only tools can still leak data. Version one sixteen also warns when a plugin and a standalone M C P server point at the same endpoint.

**SAM:** And OpenCode two point four, the open-source coding agent, added a built-in browser that can import your logins from Chrome, Edge, Firefox or Safari. Automations can also run on a timer, cron, or an M C P event.

**MAYA:** Imported logins mean the agent gets your real sessions. Give it a separate browser profile with only the accounts it needs.

**SAM:** Now the defensive side. OpenAI and Cisco open-sourced Shirudo, a pre-release runtime where agents write, test, and deploy signed kernel shields, eBPF programs, that block exploit behavior on running Linux servers until a patch lands.

**MAYA:** In a controlled test, a shield written with Codex blocked a Java4Shell exploit on a live Elasticsearch service. The caution from analysts is that one bad signed shield rolled out everywhere could take down every node at once. So stage it, review it, and keep a kill switch.

**SAM:** One more practice note. A study from DesignVerse found coding agents in legacy codebases reused a company's approved components only fifty-five to fifty-nine percent of the time, writing one-off code otherwise. Point your agents at your component library in a skill or instruction file, and check for duplicates in review.

**MAYA:** One model. Z dot ai says GLM five point four runs twenty-eight layers of its base model twice, at seven hundred fifty billion parameters, and performs like a two to three trillion parameter model. It's in their coding plan now, with no A P I yet and open weights only planned.

**SAM:** Two business and policy notes. Amazon is buying Decart's inference optimization technology, reportedly for seven and a half billion dollars, as it gets ready to sell Trainium chips to outside customers.

**MAYA:** And the European Commission proposed a Digital Fairness Act that would let consumers choose, at first use, whether a shopping agent needs their OK for every contract, some, or none. It's only a proposal, but if you build agents that buy things, design for per-user confirmation settings now.

**SAM:** So, to sum up. Agents can now approve your P Rs, so write that policy carefully. Attackers' agents are finding new bugs, so rotate exposed keys and keep services authenticated. And treat what your agent reads on the web as untrusted.

**MAYA:** All the links are in the digest, with the new stories marked. Next refresh is Sunday morning. See you then.
