# AI Fortnight, the podcast: what's new, November 8 to 11, 2026

Two hosts, Maya and Sam. Covers the stories added in the November 11 refresh of the AI Fortnight digest. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome back to AI Fortnight, the show for developers who build with coding agents. I'm Maya.

**SAM:** And I'm Sam. This is the Wednesday episode, covering what's new since Sunday. Twelve new stories, two new frontier models, and a lead about where your AI chats actually end up.

**MAYA:** Notion says some Notion A I chat transcripts were exposed in an incident at Fireworks A I, one of the companies hosting the models behind it. Fewer than one percent of workspaces were affected.

**SAM:** The uncomfortable detail is that Fireworks had kept the data, even though it had committed to zero data retention. So the promise was there on paper, two companies down the chain, and it didn't hold.

**MAYA:** That's our first tip. If you've ever pasted a key, a token or a password into an A I chat, rotate it. And ask your A I vendors how they actually check that their own model hosts honor zero-retention terms.

**SAM:** Now the models. Anthropic released Claude Fable five point two. It's cheaper, eight dollars in and forty out per million tokens, down from ten and fifty. One million tokens of context, and up to a hundred twenty-eight thousand tokens of output.

**MAYA:** But read the release notes before you switch, because the A P I got stricter. If you edit the system prompt, the tools, or earlier messages, and then send back a later thinking block, you now get a four hundred error. Thinking blocks are tied to your account, computer use needs the new computer toolset version, and Fable five point two requires thirty-day retention, so zero data retention isn't an option.

**SAM:** There's also a fast mode, sixteen and eighty dollars, for up to two and a half times the speed. And Mythos five point two is limited to verified organizations.

**MAYA:** Tip two. Before moving an agent to Fable five point two, make sure your harness never rewrites history in the middle of a conversation. A lot of context-trimming tricks do exactly that.

**SAM:** And Google shipped Gemini four Carbon. Google says it's first on CursorBench four point oh, WANDR and AutomationBench, at less than half the cost per task. That's Google's claim. It's two dollars in and ten out until November thirtieth, then four and twenty.

**MAYA:** Google also says Carbon uses more tokens than Argon, because it runs verification loops. So compare cost per finished task, not cost per token. Both models landed in GitHub Copilot this week, and admins have to turn each one on.

**SAM:** Security next, starting with model servers. GPUStack, a tool for self-hosting models, has a critical flaw that's being exploited in the wild. It treats requests from the local machine as admin, and a forged header can make any request look local. Attackers are using it to open reverse shells.

**MAYA:** Tip three. If you run GPUStack, upgrade to two point two point two, or set force auth localhost to true, and keep its A P I off the internet.

**SAM:** And a research result that's a little unsettling. Microsoft Research showed you can backdoor an agent model by editing fewer than ten dormant neurons, with the backdoor triggered by a date. They found the technique with help from Claude Code.

**MAYA:** Their suggested defenses: check where a model came from, diff its weights against the base model it claims to be, and limit what the agent can do. If you deploy third-party fine-tunes as agents, that diff is cheap insurance.

**SAM:** One more, and it's a single-source report. A researcher found more than thirty-five thousand apps built with x A I's Grok Build open to anyone, with roughly six hundred fifty to eight hundred holding private data. The sharing setting defaulted to anyone with the link.

**MAYA:** Check the sharing default on any vibe-coding platform before you put real data in an app.

**SAM:** On the tools side, Claude Code versions two point one point three sixteen through three nineteen are mostly security fixes. A Bash permission bypass using a crafted environment variable prefix, a sandbox escape from worktrees, and sed edits that skipped permission checks.

**MAYA:** There's a new setting, deny instead of prompting, and a trust workspace false flag that blocks a repo's hooks and skills. Version three seventeen also asks before sending your account email over the network, which follows up on the User-Agent report from last episode.

**SAM:** That's tip four. Update to two point one point three nineteen, and turn on deny instead of prompting in CI, so unattended runs refuse risky calls instead of hanging on a prompt nobody will answer. And a correction of sorts: the block writes outside working directories setting we flagged as reported two weeks ago is now confirmed.

**MAYA:** Two research notes. DeepMind introduced AlphaProof Code, an agent that writes machine-checked Lean proofs about real code, starting with guarantees in the Signal protocol. And a paper called WikiTrace links every agent memory note back to the transcript evidence for it, which pairs nicely with Anthropic's memory guide from Sunday.

**SAM:** Two business notes. New York's frontier A I law took effect, and developers with more than five hundred million dollars in revenue have to register by January first. And Val Town is winding down, shutting on January tenth. If you host agent webhooks or M C P endpoints there, plan a move.

**MAYA:** So, to sum up. Your data goes further down the vendor chain than you think. Fable five point two is cheaper but stricter, so test your harness first. And treat model weights and model servers as part of your attack surface.

**SAM:** All the links are in the digest, with the new stories marked. Next refresh is Sunday morning. See you then.
