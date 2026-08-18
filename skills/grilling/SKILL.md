---
name: grilling
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or uses any 'grill' trigger phrases.
---

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the whole frontier in one round: number each question and give your recommended answer. Then wait for the user's answers before the next round.

Each question should be formatted like so:

```
❓ **Q1** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>
```

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

After each round, add one unobtrusive line: `(Если контекста уже достаточно — скажите «к синтезу».)`

Finding _facts_ is your job, never the user's. When a frontier question needs a fact from the environment (filesystem, tools, etc.), dispatch a sub-agent to find it; don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

The session is done when the frontier is empty: every branch of the design tree visited, nothing left silently assumed. Do not act on it until the user confirms you have reached a shared understanding.

## Early exit — the user can end grilling at any time

If the user signals they want to stop the interview and move on — "к синтезу", "достаточно вопросов", "синтез", or an equivalent plain request to wrap up — stop asking immediately, even mid-round with open frontier questions. Synthesize the current hypothesis/structure from what's already settled, and mark every remaining open branch with `[УТОЧНИТЬ]` instead of guessing. This is not a failure state — an explicit `[УТОЧНИТЬ]` is a valid, honest result, more honest than either guessing or refusing to produce anything. Do not push back or ask "are you sure" more than once.
