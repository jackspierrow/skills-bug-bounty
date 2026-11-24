# Wallet identity gate before on-chain work

## Identify the target wallet first

- Record the target wallet address and its label before you start any signed work.

- Record every other wallet the user controls that could plausibly hold the asset or quota.

- Treat a target label without a verified address as incomplete and ask for the address before you sign anything.

## Check the live wallet before a signed step

- Read the currently connected wallet address from the live executor before each signed check, preview or execution.

- Compare the live address character by character with the target address and stop when they differ.

- Check balances, quotas and holdings in every recorded wallet before you report that an asset, quota or balance is missing.

- Label any preview result with the wallet that produced it and never present a preview from one wallet as proof for another wallet.

## Stop a structurally blocked retry

- Treat a repeated signer mismatch error as a structural block and not as a transient failure.

- Pause the retry schedule after the second identical signer mismatch and keep the job paused until the wallet changes or the user chooses a new route.

- Send the user one short message that names the live wallet, names the target wallet and offers the switch wallet choice or the pause choice.

- Stay silent on later scheduled runs while the job is paused and do not resume polling until the live wallet matches the target.

## Report a wallet change plainly

- Announce a wallet switch in the same message as any result that depends on it.

- Restate the new live wallet, the target wallet and whether they now match before you continue the old task.

- Discard any earlier preview, balance or quota result that came from the previous wallet and recheck it under the new wallet.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Ask the user to confirm the single active wallet at the start of a multi-wallet day instead of discovering a mismatch mid task.

- Keep a short workspace note of each wallet label and address and reread it before a signed step when memory is unclear.
