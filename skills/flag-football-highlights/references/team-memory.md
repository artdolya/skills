# Team memory and retrieval

## Locate the football workspace on this device

Use the football workspace explicitly identified in the current task or local workspace instructions. Otherwise, inspect available project metadata for the user's football project and verify its accessible data location. Do not infer project membership from a directory name or the skill's installation path. If the workspace is ambiguous or inaccessible, ask for the precise location or access needed and continue resolved work; do not substitute a different team's records.

All workspace paths below are relative to that verified football workspace, not the skill folder. Resolve them with the target operating system's path conventions. The workspace may be a separately synchronized private checkout or folder; this skill does not synchronize it. Historical filenames and chat/project identifiers in private records are retrieval hints, not proof that those resources are available on the current device. Do not recreate an old laptop's absolute paths.

## Retrieve the current team and season

Identify the team, season, and current game from supplied facts and accessible workspace records. Read the matching shared identity record, conventionally `team-memory/<team-season>/roster.json`, then the current game's `review/current-roster.json`, event ledger, and original coach corrections. Follow an existing workspace layout when it differs; do not create a duplicate roster merely to match this convention.

The shared record is reusable identity evidence, not proof of current attendance, unchanged jersey assignment, or an achievement in another game. Do not carry identities into a new team or season without evidence. Reuse facts that remain applicable and verify current participation, jersey changes, and actor continuity.

If the shared record is absent, recover supported facts from current/prior game records and original human corrections where accessible. Keep private continuation details and source references in the game's [context record](game-context.md). Use available chat list/read tools when needed; read the original human message rather than treating an assistant's summary as confirmation. Print only relevant excerpts from large results. Do not ask the user to repeat accessible facts. If history is unavailable, retain event-specific current human confirmations, disclose the precise gap, and avoid inventing a broader roster mapping.

## Persistence and authority

- Keep one discoverable private record per team/season, with stable player IDs, display names, aliases, number/uniform history, status, original source, and verified game/date. Store real identities in workspace records, not in this reusable skill.
- Store identity facts separately from game attendance and event outcomes. Confirmation in one game is reusable evidence to check in the next game, not blanket confirmation for every game.
- Distinguish direct coach mapping, coach-attributed play plus readable jersey, visually corroborated mapping, and tentative history. Later matched coach corrections supersede earlier guesses. Original observations stay in history; the active interpretation must be internally consistent.
- Track number corrections and uniform exceptions explicitly. A historical number or known name alone cannot identify the actor in a new play; use current evidence and trace the same player through the action.
- A correction to one play's actor/action must not manufacture the same outcome in other plays. Reinspect relevant appearances and propagate identity only where the visual match is supported.
- Update private workspace data during ordinary game editing so future sessions can retrieve corrections. Update installed skill instructions/references only when the user asks to change the skill.
