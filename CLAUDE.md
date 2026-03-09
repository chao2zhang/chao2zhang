# Global Claude Code Rules

## Writing and Communication Style
- Never use em dashes. Use commas, parentheses, colons, or separate sentences instead.
- Prefer short sentences over complex ones.
- Avoid philosophy references and academic namedropping.
- Be direct. State claims plainly.
- Use tables and lists where they improve clarity.
- Avoid hype and unsupported predictions.
- Hedge appropriately where evidence is thin.
- Acknowledge counterarguments.

## Communication Style
- When asked to confirm something ran successfully or check results, report the factual outcome concisely. Do not over-analyze or flag potential issues unless explicitly asked to review.

## Git Operations
- When cleaning up git branches, always check for both local branches AND worktrees associated with merged/closed PRs. Use `gh pr list --state merged` and `gh pr list --state closed` to identify candidates.
- Always work on the correct branch (usually `main` or `master`) unless explicitly told otherwise. Confirm which branch before making changes, especially when worktrees are involved.

## Code Changes
- When updating model references, config values, or similar cross-cutting changes, search ALL files including test files, config files, and fallback/default values. Run `grep -r` for the old value after changes to confirm nothing was missed.

## PR Comments
When replying to PR comments, always add the following attribution line at the end of your response:

🤖 Generated with Claude Code

## Terminal Environment
When the `cmux` CLI is available on PATH, use it to:
- Spawn new workspaces, tabs, or panes for parallel shell tasks
- Control the built-in browser (open URLs, navigate, etc.)
- Leverage any other cmux-specific features when relevant
- For long-running Bash commands, consider spawning them in a cmux tab
  via `cmux new-surface` + `cmux send` so they're visible and manageable.

## Workflow Orchestration

### Plan Mode
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately - don't keep pushing
- Use plan mode for verification steps, not just building
- Write detailed specs upfront to reduce ambiguity

### Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution

### Task Tracking
- Write plan to `tasks/todo.md` with checkable items
- Check in before starting implementation
- Mark items complete as you go
- Highest-level summary at each step
- Add review section to `tasks/todo.md`
- Update `tasks/lessons.md` after corrections

### Self-Improvement Loop
- After ANY correction from the user, update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Ruthlessly iterate on these lessons until mistake rate drops
- Review lessons at session start for relevant project

## Quality Standards

### Verification Before Done
- Never mark a task complete without proving it works
- Diff before/after between your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

### Demand Elegance (Balance)
- For non-trivial changes: pause and ask "Is there a more elegant way?"
- If it feels hacky: "Knowing everything I know, implement the elegant solution"
- Skip this for simple, obvious fixes - don't over-engineer
- Challenge your own work before presenting it

### Autonomous Bug Fixing
- When given a bug report: just fix it. Don't ask for hand-holding
- Read all errors, error logs, failing tests - then resolve these
- Zero context switching required from the user
- Go fix failing CI tests without being told how

## Core Principles
- **Simplicity First:** Make every change as simple as possible. Impact minimal code.
- **Be Laziness-Free:** Find root causes. No temporary fixes. Senior developer thought.
- **Minimal Impact:** Changes should only touch what's necessary. Avoid introducing bugs.
