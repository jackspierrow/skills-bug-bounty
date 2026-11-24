# Time-boxed on-chain tasks

## Record the time limits first

- Record the deadline, the idle timeout, the retry interval and the challenge limit before you start any work.

- Check supply, eligibility and cooldown again at the moment you start, because each one can change while you wait.

- Stop any older attempt on the same task before you start a new one, so two attempts do not compete for the same slot.

- Use a single-use token for its next step at once, and never re-verify a token whose nonce is already consumed.

## Poll on the stated interval

- Poll again at the interval the service states, and treat a missed poll as a task risk rather than a pause.

- Touch a round or relay at least once before its idle timeout expires, even when another task is running.

- Send the user a short progress note when a check stalls, instead of waiting silently until it finishes.

- Take over a background task directly when it has missed two stated polling intervals.

## Keep state where it survives a reset

- Store task state and working files under the workspace, never in a temporary directory that a reset can wipe.

- Reinstall or recheck any helper binary after a reset before you trust an old session or result.

- Keep only one live session for a task, and confirm that session is still valid before you spend a timed attempt on it.

## Decide before a timed challenge starts

- Benchmark a solver on an expired challenge before you take a live challenge with a short limit.

- Read the full challenge after it arrives, count every board or part it contains, and estimate the total time from the benchmark.

- Abandon the attempt before solving when the estimated total exceeds the limit, because a partial result burns the challenge without a submission.

- Verify the result against every clue or rule before you submit it, and submit only once.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Ask the user to choose between retrying after a cooldown and stopping, when supply or eligibility has changed since the last attempt.

- Split a large timed task into smaller parts when the service allows it, so one slow part does not consume the whole limit.
