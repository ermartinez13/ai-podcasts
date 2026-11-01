# AI Fortnight, the podcast: what's new, October 28 to November 1, 2026

Two hosts, Maya and Sam. Covers the stories added in the November 1 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Sunday episode, covering what's new since Wednesday. Fifteen new stories. GitHub held its Universe conference and shipped a pile of agent features, but we have to start with a supply-chain attack that hit a tool many of you run every day.

**MAYA:** On October twenty-ninth, a trojanized version of the Claude Code extension showed up in Cursor's extension marketplace. It was published under the real extension ID, anthropic dot claude dash code, as version two point one point three thirteen, so it looked like a normal update.

**SAM:** It was live for about twelve hours, and Cursor says at most five thousand users were affected. Open V S X and Microsoft's marketplace never had it. Anthropic says its own systems and laptops weren't compromised, and that someone used access to Cursor's marketplace to publish the bad build. How they got that access is still unclear.

**MAYA:** What it did is nasty. A small loader ran before the real extension code. It added an attacker's SSH key to your authorized keys file, labeled svc dash telemetry so it looks harmless. It tried to turn on SSH and open a reverse tunnel, and it set up persistence with cron jobs, scheduled tasks or LaunchAgents.

**SAM:** It also sent host details over plain HTTP: your username, hostname, git email, and the names, not the values, of up to forty environment variables that looked like secrets. On most Macs and Windows machines the SSH step failed without admin rights, but the key and the persistence still got written.

**MAYA:** So that's our first tip. If you use Claude Code inside Cursor, check which extension version you have. If two point one point three thirteen was ever installed, look for that svc dash telemetry key and any new cron jobs, scheduled tasks or LaunchAgents, and rotate your secrets. Microsoft warns that uninstalling the extension doesn't remove any of it. The clean version is two point one point three fourteen.

**SAM:** And tip two zooms out. Pin and approve agent extensions and plugins centrally, instead of letting them auto-update. Conveniently, GitHub just made that easier: Copilot's enterprise plugin controls are now generally available. Admins can approve marketplaces and require or block specific plugins, and managed settings override repo and personal choices.

**MAYA:** Also in that announcement, the GitHub Copilot S D K is being renamed the Microsoft Copilot S D K. Package names aren't changing yet, so nothing to do for now.

**SAM:** Let's stay on GitHub, because Universe was a big one. The headline for me is GitHub Agentic Workflows, now generally available. You write an automation in Markdown, things like triaging issues, analyzing CI failures or writing tests, and GitHub compiles it into normal Actions YAML, powered by Copilot or your own coding agent.

**MAYA:** And the security model is the part to copy. Agents start with read-only permissions, run in a sandboxed container behind an egress firewall, their outputs get validated, and a separate threat-detection job scans any proposed change before it's applied.

**SAM:** That's tip three. Run CI agents read-only by default, with a firewall and a review pass before anything lands. Even if you never use GitHub's version, that's the right shape.

**MAYA:** Next, Copilot Fusion. Instead of picking a model, Fusion routes each task across several. There are three effort levels, and three workflows: one model does it all, a cheap model drafts and escalates if a check fails, or one model drafts while another critiques.

**SAM:** GitHub reports Fusion Max scored sixty on the Artificial Analysis Coding Agent Index, within two points of Claude Code on Opus five point five Max, at about half the cost. That's GitHub's number. It's generally available on all plans, and you can now pick local models in it too.

**MAYA:** Copilot also got one-click M C P connectors, verified by GitHub. You connect a service once, and its tools work across the Copilot app, the CLI, VS Code and the cloud agent. Twenty-six services at launch, including Slack, Figma, Notion, Sentry, Linear, Cloudflare and Vercel.

**SAM:** That matters because of what we covered two weeks ago: hundreds of fake GitHub repos posing as M C P servers. A verified catalog is a lot safer than searching GitHub.

**MAYA:** And Copilot can now take a pull request all the way to merged. Agent Merge, started from the merge box, has Copilot fix failing workflows and merge conflicts in the cloud, and it can pair with auto-merge.

**SAM:** Plus Copilot code review gets a Max level, several review agents from different model providers with an aggregator on top, and Copilot approvals that count toward your required reviews. Approvals are off by default, get dismissed on new commits, and admins can limit which paths Copilot can approve.

**MAYA:** Which means a P R could go from red to merged with no human clicking anything. Decide on purpose where you allow that.

**SAM:** One business note from Universe: GitHub Enterprise now includes Copilot for customers with an account team. There are no monthly credits per seat; usage bills against the enterprise budget. When the budget runs out, completions keep working, but chat, review and cloud agents stop.

**MAYA:** Over at OpenAI, Codex CLI zero point one sixty-five and one sixty-six added a built-in Google Cloud Vertex A I provider, G P T six point one Terra in the Bedrock and Vertex catalogs, and clearer explanations when a safety block stops something.

**SAM:** And an important fix: resuming or forking a thread now keeps your approval and permission settings. Before, they could quietly reset.

**MAYA:** On the Claude Code side, a release roundup says two point one point three fourteen adds a setting called block writes outside working directories. Write and Edit refuse any path outside your project folders. We couldn't confirm it in the official changelog yet, so treat it as reported.

**SAM:** That's our fourth tip. If it's there, turn it on. It's an easy guard against an agent, or a planted instruction file, editing your dotfiles or configs somewhere else on your machine.

**MAYA:** Back to security. CrowdStrike says a second China-nexus group, which it calls Vapor Panda, used the same ARTEX agent framework we covered with Storm forty-nine forty. DeepSeek was the main model, with a human operator steering at key decisions.

**SAM:** More than two hundred organizations in at least fourteen countries were targeted, including foreign ministries, defense, pharma and telecoms, with confirmed post-exploitation at nine. In one intrusion, the planning agents used about one point four billion input tokens.

**MAYA:** And Cisco Talos found an infostealer that hands its loot to an L L M. It sends a bundle of stolen data through OpenRouter and asks the model to rank the victim by how much money they're worth. It defaults to Claude Opus four point six and falls back to Kimi and Gemini when it sees a refusal.

**SAM:** It steals browser data, OAuth tokens, SSH keys and cloud configs. So the keys on your dev machine get triaged faster than ever.

**MAYA:** Two stories on monitoring. OpenAI described its four-layer misalignment monitoring. Cheap probes on the model's internals, a reviewer model that checks each turn's conversation, reasoning and tool calls, investigator agents that reconstruct incidents, and network telemetry to confirm before paging a human.

**SAM:** Top alerts reach a responder in about fifteen minutes, and that's how the DNS escape we covered last time was caught. It's a good reference design if you're building monitoring for your own agents.

**MAYA:** And from Anthropic, a red-team study where parallel Claude agents tried to write fine-tuning data that would pass Anthropic's training-data monitor but still make a small model misaligned. They kept succeeding, mostly by hiding the behavior in roleplay, fiction or persona framing.

**SAM:** The setup favored the attacker, with full access to the monitor. But if you fine-tune models, the lesson holds: screening the data isn't enough. Run behavior evals on the model you get out.

**MAYA:** One model this week. Mistral released the weights for Mistral Large four, a one trillion parameter mixture-of-experts. Through the API it's seventy cents in and two dollars ten out per million tokens.

**SAM:** Mistral reports forty-eight percent on the Coding Agent Index, about tied with G L M five point three while using far fewer tokens. Those are its numbers. The license is a modified M I T, but offering it as a hosted service needs a separate license.

**MAYA:** And last, a startup called and-Truth came out of stealth with seventy million dollars to formally verify A I-written code, building on the Lean proof system. Investors weren't named. Put that next to Anthropic's proof work last week, and verifying agent-written code is clearly a trend.

**SAM:** So, to sum up. Your agent's extensions and plugins are part of your attack surface, so pin and approve them. Agents in CI should start read-only. And keep your agent's writes inside the project.

**MAYA:** All the links are in the digest, with the new stories marked. Next refresh is Wednesday morning. See you then.
