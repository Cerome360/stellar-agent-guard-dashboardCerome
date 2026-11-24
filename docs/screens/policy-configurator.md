# Policy Configurator (`/configure`)

Interactive no-code form for configuring smart account guardrails:

- **Policy Presets**: One-click archetypes (Strict Micro-Agent, Standard DeFi Bot, High-Throughput Arbitrage), each badged Conservative, Balanced or Permissive. Selecting one asks to confirm before replacing the current draft; placeholder addresses must be replaced before installing.
- **Per-Transaction Spend Cap**: Limits maximum tokens moved in a single call.
- **Rolling Window Cap & Duration**: Enforces spending limits over a rolling time window (seconds).
- **Asset Allowlists**: Enforces accepted SAC tokens.
- **Recipient Allowlists**: Default-deny recipient address list.
- **Protocol & Function Allowlists**: Configures approved contract IDs and method names for arbitrary Soroban calls.
- **Active Execution Windows**: Restricts execution to specific ledger timestamp intervals.
- **Pause Switch**: Global pause switch for routine maintenance.
- **Dead-Man Grace Window**: Configures maximum allowable inactivity period in seconds.
- **Effective Defaults**: Each optional field shows the contract-defined meaning of leaving it blank or off, linked to the [contracts SPEC](https://github.com/Stellar-Agent-Guard/stellar-agent-guard-contracts/blob/main/SPEC.md#validation-rules-and-accepted-but-inert-configurations). Examples: a blank cap encodes the zero/disabled sentinel, an empty asset or protocol list blocks that class of call, and blank active bounds impose no time restriction.
- **Validation Summary**: Before `Review`, every invalid field is listed with a link to its input. Selecting a link focuses the input, reveals the same inline message, and announces it through the live region. Imported policy JSON and presets pass through this same draft validation before any wallet prompt.
- **Change Review**: Before the wallet is prompted, a diff modal lists every field that actually changes —
  fields identical to the installed policy are not shown, and an entirely identical policy says so instead
  of rendering an empty table. Each row states its status in words (`added`, `removed`, `changed`) as well
  as by a `+` / `−` / `~` marker and a coloured edge, so the meaning survives a screen reader, a
  monochrome display and `prefers-contrast: more`. A one-line summary counts the changes first. Those
  markers are painted from the shared `--ok` / `--danger` / `--warn` / `--muted` tokens in
  [`app/globals.css`](../../app/globals.css) rather than a local palette; `npm test` measures each of them
  against the modal surface and fails below the WCAG 2.1 AA floor of 4.5:1. Warnings (a lower window cap,
  a shortened dead-man grace) reuse the same notice tier as the default-deny banner.
