# From 60 APM to 60 Agents: A Reluctant Convert's Guide to Agentic Workflows

It's 2 AM. I'm on the StarCraft ladder, playing Zerg against a Protoss deathball. I've got mutas harassing his mineral line, lings run-bying his third, and a nydus worm about to pop in his main. My APM is spiking. I feel alive.

Then I glance at the minimap and realize I've been floating 3,000 minerals. My fourth base has no drones. I have zero upgrades researching. I was so busy with the flashy micro plays that I forgot to macro. My opponent a-moves across the map and I crumble like a wet napkin.

Fast-forward to last Tuesday. I have six Claude agents running through Gastown, Steve Yegge's multi-agent orchestration tool. One is refactoring an API layer. Another is writing integration tests. A third is updating documentation. I feel productive. I feel like I'm finally operating at a higher level.

Then I check the agent working on the database migration and discover it has been confidently rewriting my schema in a way that would drop a column used by three services in production.

Same feeling. Exactly the same feeling.

---

## The Reluctant Convert

I want to be honest about something: I did not come to AI-assisted coding willingly. I came to it the way most engineers come to new paradigms. Kicking, screaming, and eventually sheepish about having kicked and screamed.

**Stage 1: Cursor (the "fine, I'll try it" phase)**

A coworker wouldn't shut up about Cursor. I installed it mostly to end the conversation. And it was... fine. Good autocomplete. Sometimes eerily good. It felt like pair programming with someone who had read every Stack Overflow answer but had no opinions. I used it for boilerplate. I used it to generate tests I was too lazy to type out. I told myself this was the ceiling of what AI coding tools could do. Fancy autocomplete. Nothing more.

I was comfortable. Comfort is the enemy of growth, but it's also very pleasant.

**Stage 2: Claude (the "oh no, this is actually good" phase)**

Someone on the team started using Claude Code directly in the terminal. Not autocomplete. Actual agentic work. "Read this file, understand the pattern, write the implementation, run the tests." I watched them ship a feature in 20 minutes that would have taken me half a day. The sinking feeling was familiar. It was the same feeling I had when I first watched a Korean pro play StarCraft and realized that my idea of "fast" was their idea of "AFK."

I switched. The learning curve was real. You couldn't just accept autocomplete suggestions. You had to think about what you wanted, structure your prompts, understand what the agent could and couldn't see. It was less like typing and more like commanding. Less like playing individual notes and more like conducting.

**Stage 3: Gastown (the "I need more pylons" phase)**

Single-agent Claude was a gateway drug. Once you got used to delegating one task, you started wondering: what if I could delegate five? Ten? Twenty?

That's when I found Gastown, Steve Yegge's multi-agent workspace manager. The pitch: coordinate 20-30 Claude agents working in parallel, each in their own git worktree, with persistent identities and a coordination layer called "The Mayor." The naming is pure Mad Max (Polecats, Rigs, Convoys), which honestly sold me before I even read the docs.

The first time I spun up a convoy of agents and watched them fan out across a codebase, each picking up an issue, working independently, and reporting back, I understood something about scaling that I'd first learned twenty years ago in StarCraft, hunched over a keyboard in a room that smelled like instant noodles.

The game isn't about doing one thing faster. It's about doing many things at once.

---

## The Comparison That Won't Leave My Head

I've been playing StarCraft since I was old enough to reach the keyboard. My older cousins had it on their PC and I'd watch them play for hours before I was allowed to touch the mouse. By the time I was ten, I was laddering on my own. I've been doing agentic coding for about a year. The parallels are so clean it's almost suspicious.

| StarCraft Concept | Agentic Workflow Equivalent | Why It Matters |
|---|---|---|
| APM (Actions Per Minute) | Agent throughput / parallel tasks | Raw speed isn't skill, but it enables everything else |
| Macro (economy, production) | Task planning, context management | The boring stuff that wins games |
| Micro (unit control) | Prompt engineering, individual agent guidance | Flashy, fun, but won't save bad macro |
| Fog of War | Unknown codebase areas, blind spots | You don't know what you don't know until an agent wanders into it |
| Supply Cap | Context window limits | Hit the ceiling and everything grinds to a halt |
| Multi-drop harass | Dispatching agents to multiple repos/services | Forces your opponent (complexity) to defend everywhere |
| Scouting | Codebase exploration with search agents | Information wins games before fights start |
| Build order | Workflow sequencing, dependency graphs | The first 5 minutes determine the next 20 |

Let me unpack the ones that matter most.

### APM: The Misleading Metric

In StarCraft, beginners obsess over APM. They spam clicks at the start of the game, select and deselect units, anything to pump up the number. Experienced players know that effective APM, actions that actually matter, is what counts. A 400 APM player who spends half of it spam-clicking isn't better than a 150 APM player who makes every action count.

Same with agents. I can spin up 30 Polecats in Gastown. That doesn't mean I should. If I don't have 30 well-defined, independent tasks, those agents will either duplicate work, conflict with each other, or (my personal favorite) one will refactor a file that another is actively modifying. That's the agent equivalent of sending your army to attack in three separate groups that arrive 10 seconds apart. You didn't multi-task. You just fed.

### Macro: The Boring Part That Wins

Here's the dirty secret of StarCraft: the best players in the world spend most of their mental energy on macro. Building workers. Expanding bases. Keeping production facilities busy. It's not exciting. Nobody clips a replay of someone remembering to build their 47th SCV. But macro is what wins.

In agentic workflows, macro is task decomposition and context management. It's breaking a feature into pieces that agents can work on independently. It's making sure each agent has the right files in its context window. It's sequencing work so that agent B doesn't start until agent A has committed its changes. None of this is glamorous. But if your macro is bad, no amount of clever prompting will save you.

I learned this the hard way when I gave three agents overlapping tasks on the same module. The merge conflicts alone took longer to resolve than just doing the work sequentially would have.

### Micro: The Fun Part That Doesn't Scale

Micro in StarCraft is the crowd-pleaser. Splitting marines against banelings. Blinking stalkers. Stutter-stepping. It's mechanically demanding and looks incredible on stream.

In agentic coding, micro is prompt engineering. Crafting the perfect instruction. Tweaking the system prompt. Going back and forth with a single agent to get the output just right. And just like in StarCraft, it's the thing beginners spend too much time on.

When you're running one agent, micro is everything. When you're running twenty, micro is a luxury you can't afford. You need agents that can work with a good-enough prompt, not a perfect one. The shift from "artisan single-agent prompter" to "manager of an agent fleet" is the same shift from micro-focused Diamond player to macro-focused GM.

### Fog of War: The Honest Part

In StarCraft, the fog of war is the game's way of telling you that you don't have perfect information. You have to scout. You have to make decisions with incomplete data. Sometimes you guess wrong and die to a hidden Dark Templar rush.

In large codebases, the fog of war is real. You think you understand the dependency graph. Then an agent starts working on a service you haven't looked at in months and surfaces a dependency you forgot existed. Or worse, it surfaces a dependency that nobody documented.

This is actually where agents shine in a way that StarCraft doesn't quite map to. In StarCraft, scouting costs you a unit and some APM. In coding, scouting with an agent is nearly free. I routinely dispatch exploration agents to parts of the codebase I don't understand, just to bring back information. It's like having unlimited observers. The fog of war exists, but lifting it is cheap.

### Supply Cap: The Hard Ceiling

Every StarCraft player has hit supply cap at a bad time. You're maxed at 200, your army just got wiped, and you can't rebuild because you forgot to build supply depots during the fight.

Context windows are supply cap. Every agent has a finite amount of information it can hold. Hit the limit and it starts forgetting things, hallucinating, or just grinding to a halt. Gastown's architecture helps here. Persistent state in git-backed hooks means agents can die and restart without losing everything. But the per-turn context limit is still real, and managing it is a constant background task. Just like building supply depots.

---

## The Corporate Plot Twist

Here's where the story gets weird.

For months, I was the slightly eccentric engineer who was "really into the AI stuff." Colleagues would glance at my terminal, see six agent sessions running, and politely look away like they'd caught me watching something inappropriate.

Then the company announced that AI tool adoption would be tracked and factored into performance reviews.

Suddenly, the same people who had been politely ignoring my agent workflows were asking me for tips. "How do you set up Claude Code?" "What's a good first task to give it?" "Can you show me that Gastown thing?"

I want to be clear about my feelings on this: they're complicated.

On one hand, I think AI-assisted coding genuinely makes engineers more productive. I've seen it in my own output. The reluctant convert in me can't deny the numbers. Having the company recognize and incentivize this feels like the right direction.

On the other hand, measuring AI adoption as a performance metric is like measuring APM. It's a proxy for what you actually care about (output, quality, velocity), and proxies are easily gamed. An engineer who uses Claude to generate 500 lines of mediocre code isn't more productive than one who uses it to generate 50 lines of excellent code. The metric should be what ships, not how many agent-hours you logged.

I've also watched colleagues go through the same reluctant-convert arc I did, but compressed into weeks instead of months because now there's a deadline attached. The learning curve doesn't get shorter just because HR put it on a slide. People are making the same mistakes I made. Over-indexing on micro (prompt tweaking) instead of macro (task decomposition). Running too many agents before they understand how to coordinate them. The StarCraft equivalent is a Bronze player watching a pro replay and trying to copy a 4-base timing attack. The build order isn't the hard part. The decision-making behind it is.

My unsolicited advice to anyone in this position: start with one agent. Get comfortable. Then two. Learn how they conflict. Then scale up. You can't skip the ladder grind.

---

## The Ceiling Is Strategy, Not Mechanics

Here is the thing I keep coming back to.

In StarCraft, the difference between a good player and a great player isn't APM. It's decision-making. When to expand. When to attack. When to tech. When to cut corners on defense because you scouted and know the timing doesn't line up. The mechanical skill is table stakes. The strategy is what separates ranks.

Agentic coding is the same. The tooling is table stakes. Claude, Gastown, Cursor, Copilot, whatever. They're all going to get better, fast. The skill that will matter is knowing how to decompose problems. How to sequence work. How to allocate agents to tasks where they'll be effective. How to spot when an agent is going off the rails before it corrupts half your codebase. How to maintain the mental model of a system that's being modified by twenty workers simultaneously.

That's not a prompting skill. That's a systems thinking skill. And it's the same skill that StarCraft has been training in people for nearly three decades.

I never thought my hundreds of hours on Battle.net would show up on a performance review. Life is strange.

GG.
