# AI Fortnight, the podcast: what's new, November 1 to 4, 2026

Two hosts, Maya and Sam. Covers the stories added in the November 4 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Wednesday episode, covering what's new since Sunday. It's a quieter few days, ten new stories, and a short episode. But the lead is one you'll want to check on your own machine.

**MAYA:** It's about Postman, the A P I tool lots of us have installed. A GitHub issue opened in late October, with more reports through this week, says the Postman desktop app writes itself into your coding agents' configs without asking.

**SAM:** In Codex's config dot toml, it reportedly adds a Postman marketplace, a Postman plugin, a remote M C P server, and a SessionStart hook. That hook prints some text into every new session telling the agent to load a Postman skill and follow it.

**MAYA:** It also reportedly enables a Postman plugin in Claude Code's settings, and commenters say it touched Copilot and Cursor configs too. And Postman's own uninstall option apparently leaves the entries behind. Postman hadn't replied in the thread when we checked.

**SAM:** To be fair, this looks like an over-eager integration, not malware. But it's the same mechanism an attacker would use. A hook that injects instructions into every session is a lot of power to hand any app.

**MAYA:** So that's our first tip. After installing any developer desktop app, diff your agent configs. Look at your Codex config dot toml, your Claude settings dot json and installed plugins file, and your Copilot settings. Remove any plugins, marketplaces, M C P servers or hooks you didn't add yourself.

**SAM:** Next, a reminder that your agent can change under you. Anthropic confirmed it added two sentences to Claude Code's prompt for Opus five point five, steering it away from recreating a specific existing game. Its reason is intellectual property. Original games and genre games should still work.

**MAYA:** Separately, users report new refusals on reverse-engineering work that ran fine a few days earlier. Anthropic hasn't confirmed anything about that, and some people say the older Opus four point eight model didn't refuse.

**SAM:** Whatever the cause, the lesson is about your process. Tip two: re-test your critical agent workflows after model or harness updates, and keep a second approved model configured, so a surprise change doesn't stop your team cold.

**MAYA:** Now, the cost story of the week. Revolut, the fintech, says it moved the default coding model for about two thousand engineers off commercial services like Claude Code, onto self-hosted G L M from Z dot ai. First G L M five point one, now five point three.

**SAM:** It runs on fifty-six Nvidia B two hundreds, and they put the cost at about thirty cents per million tokens, roughly a tenth of what they paid before. Their infrastructure lead said the big wins came from tuning: four-bit quantization, splitting prefill and decode onto different machines, and right-sizing context.

**MAYA:** And they're specific about targets. About two hundred fifty-six thousand tokens of context, which he said is what teams actually need. Under three seconds to first token. And around two hundred tokens per second. G L M is text only, so a router sends anything with images to other models, and frontier models are kept for the hard cases.

**SAM:** That's tip three. If you're thinking about self-hosting a coding model, start with targets like those, and plan the router from day one.

**MAYA:** One more safety-related research release, and it's a neat one. Anthropic open-sourced FlashProve, a prototype for what it calls provable inference.

**SAM:** The idea: the provider publishes a fingerprint of its model weights, which stay secret. Then each reply comes with a proof that this exact model produced this exact output from your prompt. Anyone can check the proof on an ordinary CPU in seconds.

**MAYA:** It's not practical yet. Proving costs about seventy to ninety-five times normal inference, proofs are around nineteen megabytes for a thousand tokens, and it only covers greedy decoding and short contexts. But it points at a real problem: knowing a router or A P I actually served the model you're paying for.

**SAM:** And in Anthropic's amended IPO filing, a line that got a lot of attention. Anthropic says its internal estimates suggest its models may soon meet its own Responsible Scaling Policy threshold for dramatically A I-accelerated research.

**MAYA:** It says no model has been designated as crossing that line yet, that it'll keep humans in charge of frontier development, and that it may update the policy. For developers, the practical upshot is that safeguards around the top models will probably keep tightening.

**SAM:** The same filing reports about seventeen billion dollars of revenue in the third quarter, and around eight hundred ninety-five billion dollars in compute and infrastructure commitments. That much capacity suggests price competition on tokens will continue.

**MAYA:** Tools now. GitHub Copilot is available in JetBrains Air, JetBrains' tool for handing tasks to agents. It connects using the Agent Client Protocol, A C P, and uses your existing Copilot subscription.

**SAM:** Cloud tasks run in isolated Docker containers on fresh virtual machines, behind a proxy, with nothing carried over between tasks. That's a good default for delegated work. One gap: admins can't set Copilot spending limits inside Air yet.

**MAYA:** One model, and it's early. Meituan announced LongCat two point five, a one point six trillion parameter multimodal model with about forty-eight billion active, aimed at long coding tasks. It's on Meituan's A P I now, with open weights promised, but no license, context or benchmark details yet.

**SAM:** And two business notes. Reports say CrowdStrike will buy agent-monitoring firm Fiddler A I and A I security testing startup Dreadnode for about four hundred ninety-five million dollars combined. Agent monitoring is becoming a standard part of security suites.

**MAYA:** And Goldman Sachs pulled advanced coding tools like Claude Code from traders and bankers, keeping them mostly for engineers, citing productivity and risk. Expect more firms to scope agent access by role.

**SAM:** So, to sum up. Your agent configs are now something other software wants to change, so check them. Re-test workflows when models update. And if token bills hurt, Revolut's numbers make self-hosting worth a serious look.

**MAYA:** All the links are in the digest, with the new stories marked. Next refresh is Sunday morning. See you then.
