# Lab Notes: November 10 to 16, 2026

Two hosts, Maya and Sam. The best frontier-lab posts of the week, read for agentic developers. Numbers and acronyms are written the way they should be said aloud.

---

**MAYA:** Welcome to Lab Notes, the weekly deep read of the best posts from the AI labs. I'm Maya.

**SAM:** And I'm Sam. This week covers November tenth through sixteenth. It was a busy week for launches, but launches aren't what this show is for. Two posts cleared our bar, and they happen to fit together nicely.

**MAYA:** Both are about the same surprising fact: agents spend most of their lives doing nothing. One post, from Anthropic, is about how to architect an agent that sleeps most of the time and wakes up to act. The other, from Google, is about how to stop paying for compute while it sleeps.

**SAM:** Quick note on who didn't make it. OpenAI posted about two dozen times this week, but it was mostly customer stories, healthcare and science launches, and partnerships. Cursor, xAI and Mistral didn't publish anything new on their blogs. And at the end, we'll give a short shout-out to one more Anthropic post that's worth your time.

**MAYA:** Let's start with Anthropic. On November thirteenth, the Claude blog published "Building always-on agents," by William Hu.

**SAM:** Always-on agents are agents that run indefinitely. Think of a personal assistant that watches your inbox, or an agent that follows up on a ticket three days later without being asked. They decide for themselves how and when to act, across many sessions.

**MAYA:** And the first thing the post says is that the name is misleading. The agent isn't literally always on. In their words, it "spends most of its time asleep." It wakes up for short runs. Each run takes an event, does some work, saves its state, and goes back to sleep.

**SAM:** Which is the key mental shift. The agent loop itself is the same loop you already have. What's different is everything around it. And the post breaks that into five building blocks.

**MAYA:** Number one is the event inbox. It's a durable table that everything writes to: webhooks, schedules, background jobs. One worker reads from it. That gives you two important properties for free. Events get deduplicated, and you never have two runs of the same agent competing with each other.

**SAM:** They recommend one inbox per user. And they say to treat the inbox as the source of truth. If a worker crashes halfway through, the event is still in the table, so it can be retried instead of lost.

**MAYA:** Number two is timers. These are follow-ups the agent sets for itself, like check back on this pull request tomorrow, plus recurring schedules, like a daily newsletter. A separate scheduler polls for timers that are due and drops them into the inbox, so they look like any other event.

**SAM:** I like that design. Everything becomes an event in one place, whether it came from a webhook, a user, or the agent's own reminder.

**MAYA:** Number three is memory. They describe four kinds: the user's instructions, notes about the user, past messages, and progress on tasks. Only an index of memory loads at the start of each run, and the agent pulls in details when it needs them.

**SAM:** And this connects to last week's episode. They mention an optional dreaming step that curates memories across sessions, which is the same idea from Anthropic's agent memory post. They also point to Claude Code's auto memory and the memory tool in the Messages API as designs you can copy.

**MAYA:** Number four is permissions, and this is the part I'd read twice. They describe three pieces. First, a credential proxy. It injects secrets into outgoing requests, so the agent itself never holds your passwords or tokens.

**SAM:** Which, after the digest stories we've had about agents leaking secrets into config files and request headers, is exactly the right default.

**MAYA:** Second, an auto mode where classifiers decide which actions are safe to run without asking. And third, deferred tool calls. When the agent wants to do something that needs approval, the run pauses until the user says yes. Their example is an approval card the user taps, built with MCP Apps.

**SAM:** And number five is the outbox, a queue of outgoing messages with a dispatcher that sends them. But they're honest that many teams can skip it and just give the agent a simple send-message tool.

**MAYA:** Then there's a list of design tips that are really practical. Keep the handler that receives events fast, and push slow checks, like screening for prompt injection, into the run itself. If a user sends five messages in a row, batch them into one run instead of starting five.

**SAM:** Keep the startup context lean and use prompt caching. And anything that has to survive should go into memory, because both compaction and new sessions lose detail.

**MAYA:** And my favorite: let the agent start quiet. An always-on agent can easily become noisy, messaging you too often or about the wrong things. So they suggest it earns your attention gradually, and that you use evals to check it's flagging what matters.

**SAM:** They also list the failure modes the design is meant to prevent: competing runs when two events arrive at once, events lost when a worker crashes, bloated startup context, long sessions that forget details, unattended runs holding user credentials, and agents that over-message or miss what matters.

**MAYA:** On numbers, there's only one hard figure. On a long-horizon coding benchmark, Opus five point five cost seventy-eight percent less per solved task than Opus five, compared with about forty percent less on typical workloads. The argument is that long, unattended work is getting cheap enough to make always-on agents practical.

**SAM:** And that's where the caveats come in. That cost figure is Anthropic's own, from a single benchmark, so treat it as a claim. There's no data on latency, reliability, or real production failures. And many of the references point to Anthropic's own products.

**MAYA:** But the architecture isn't tied to Claude. An inbox table, a scheduler, a credential proxy and an approval step work with any model.

**SAM:** So the takeaway: if you're building an agent that acts on its own over days, start with a durable inbox and one worker per user, keep secrets behind a proxy, and pause for approval on risky actions instead of trusting the model to ask.

**MAYA:** Which brings us neatly to the second post, because if your agent is asleep most of the time, you have to ask what you're paying for while it sleeps.

**SAM:** This is from the Google Developers Blog, November sixteenth, by Drake Williams, a product manager at Google Cloud, and Ivan Nardini from AI developer relations. The title says it all: "Agents are sessions, not requests."

**MAYA:** Here's the argument. Web servers handle requests that last milliseconds, so Kubernetes scales them up and down with traffic. Agent sessions are different. They stay open all day, they do work in short bursts, and they mostly wait.

**SAM:** And they have numbers for how much they wait. They cite a study of GitHub Copilot agent traces, by Banruo Liu and colleagues, that found agents spend about eighty percent of their time waiting for the user.

**MAYA:** An average turn involves about three hundred ninety-six seconds of actual agent work, so six and a half minutes. If a developer sends two prompts an hour over an eight-hour day, the agent is working only twenty-two percent of the time.

**SAM:** So the obvious setup, one container per session that stays up all day, means you pay for idle compute almost four-fifths of the time. They work through an example. One pod per session, with one virtual CPU and one gigabyte of memory. A standard four-CPU machine fits three of those. So a hundred agents need thirty-four nodes, about twelve hundred eighty-eight dollars a month.

**MAYA:** The alternative is what they call parking. When a session goes idle, you snapshot its sandbox to object storage and free up the worker, while the session stays open from the user's point of view. When the user comes back, it's restored.

**SAM:** With a two-minute idle timeout, each session holds a worker only twenty-nine percent of the time it's open. They size a warm pool of fifteen nodes, which covers the ninety-ninth percentile burst plus fifteen percent headroom. Add one always-on node for the control plane, and scale to zero after hours. That saves forty percent of the node bill.

**MAYA:** And what's the catch?

**SAM:** Sometimes the pool is full. In their model, that happens about once in thirty-five hundred turns. If people prompt more, say two and a half times an hour, the pool is full on three percent of turns. And by default, a request that can't find a free worker waits five seconds and then fails with a five oh three error.

**MAYA:** What I appreciate is that they show where parking stops paying off. At four prompts an hour, the pool has to grow to twenty-seven nodes and the savings drop to four percent. Around four and a half prompts an hour, plain one-pod-per-session becomes cheaper.

**SAM:** And they give a break-even point the other way, too. Parking pays off from about thirty-seven coding sessions, or about thirteen chat-assistant sessions, where the agent only works about a minute per hour.

**MAYA:** One more thing. If you keep the warm pool running all seven hundred thirty hours of the month instead of scaling it down at night, it costs about twice as much as the simple one-pod-per-session setup. So the after-hours scale-to-zero isn't optional.

**SAM:** There's also an overcommit option. If each pod requests a quarter of a CPU but is allowed to burst to a full CPU, you can pack twelve pods per node, and a hundred agents fit on nine nodes. But that changes how much CPU each session is guaranteed, so they say compare options only at the same CPU guarantee.

**MAYA:** Their practical advice: measure your actual prompt rates from a week of gateway logs, and size the pool for the busiest hour. Set an idle timeout, call the suspend API from your harness, and scale to zero after hours with a scheduled job.

**SAM:** Now the caveats, and they're upfront about them. Google's Agent Substrate doesn't yet suspend idle sessions automatically. There's an open issue for it, so your code has to call suspend itself. The autoscaler tracks worker pods, not suspended sessions. When a session is restored, its workspace files come back, but the agent's processes restart fresh. The pricing is US central list prices. And they say the prompt rate is the least certain input in the whole model.

**MAYA:** And obviously, it's written by Google about Google's own stack. But the insight works anywhere. If your agents run in containers, measure how much of the time they're idle before you decide how to host them.

**SAM:** Takeaway: pull a week of logs, work out how many prompts an hour your users really send, and if it's under about four, look at suspending idle agent sandboxes instead of keeping one container per session running all day.

**MAYA:** Before we go, one honorable mention. We keep to one post per lab, but Anthropic's engineering team also published "Building strong safety evaluations" on November thirteenth, and if you write evals for agents, it's worth reading.

**SAM:** Three lines from it stuck with me. Make grading criteria atomic and binary, simple yes-or-no checks. Validate your model grader against human labels before you trust it. And report confidence intervals. In one of their tests, the same model scored up to thirty-four points differently depending on whether it ran through the API or the Claude app with its system prompt.

**MAYA:** So the configuration you test is part of the result.

**SAM:** Let's wrap up. This week's theme: agents are mostly idle, so design for it. Anthropic shows how to architect an agent that sleeps and wakes on events, with a durable inbox, timers, lean memory, and a credential proxy. Google shows how to stop paying for it while it sleeps.

**MAYA:** Both posts are linked in the show notes, along with the evals post. Lab Notes is back next Tuesday.

**SAM:** See you then.

## Sources

- [Anthropic: Building always-on agents (Nov 13)](https://claude.com/resources/articles/building-always-on-agents)
- [Google Developers Blog: Agents are sessions, not requests (Nov 16)](https://developers.googleblog.com/agents-are-sessions-not-requests-size-gke-node-pools-for-ai-agent-sessions/)
- [Anthropic: Building strong safety evaluations (Nov 13)](https://www.anthropic.com/research/building-strong-safety-evaluations)
