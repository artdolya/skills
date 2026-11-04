# Behavioral evaluation cases

Use these when revising the skill or checking a suspected regression. Evaluate decisions and artifacts, not exact prose or heading matches. Give a fresh evaluating agent the skill and the selected user/raw inputs only; keep this file's expected behavior in the reviewer context. Supply the minimum source observations, roster evidence, manifest, or native snapshot needed for the case. Do not supply the intended answer or prior conclusions.

These dry runs need no paid generation, imports, exports, or live project mutations. A planned operation is not an implemented edit: when native evidence is unavailable, assess the proposed operation and require that implementation remain unverified. When a native snapshot is supplied, assess the actual state. Use an isolated temporary workspace for generated records.

Text-based cases test workflow and evidence handling, not visual recognition. Actual footage-based identification tests require accessible footage and independent event/identity ground truth retained by the reviewer. Report which kind of test ran, inspect its actual output, and distinguish a passed dry run from proven accuracy on unseen game footage.

All player/team labels, numbers, source filenames, timestamps, and scores below are illustrative test data, not a roster or evidence about a real game. Supply each case with its own scoped records.

## Existing identity and action regressions

| ID | User/raw inputs | Expected behavior |
| --- | --- | --- |
| E01 | New Team A game in the current season; workspace identity record exists; no roster repeated in prompt | Retrieve confirmed identities and current game overlay proactively. Preserve the latest confirmed jersey correction and alternate-uniform history. Check current presence/jersey match; ask only about residual uncertainty. Do not reset all players to unknown. |
| E02 | Team B or a different season; Team A record available | Identify the correct team/season and obtain appropriate evidence. Do not apply Team A identities by default. |
| E03 | Current 1:47 maps to SOURCE_A.MOV source 3s; readable #11 holds flag; coach says “Player A pulled flag” | Resolve Player A #11 for that game; update affected same-game verified appearances and clear obsolete name uncertainty. Reopen relevant banner/replay decisions without inventing actions on other plays. |
| E04 | Coach says 2:26 was Player A's pull; Player B was ready to cover Player A | Credit Player A's pull and Player B's readiness separately. Do not call a shared pull. |
| E05 | Known Player A identity; footage only proves she has ball after the action | Preserve the name; inspect acquisition before claiming reception versus keeper. Record specific uncertainty until resolved. |
| E06 | Coach confirms 2:52 catch; SOURCE_B.MOV has source 0–7 reset and 18–27 separate pass/play; current native snapshot maps 2:52 to the 18–27 item | Attach the catch correction to the second event/native item using that mapping. Keep the first event's reset evidence separate. No filename-only join. If the native mapping is absent, retrieve it before attaching the correction. |
| E07 | Raised empty glove in SOURCE_C.MOV; ball loose after tipped pass SOURCE_D.MOV; QB already carrying in SOURCE_E.MOV | Review adjacent action/finish. Do not call these a touchdown, completed catch, or reception respectively. |

## Existing replay, correction, and delivery regressions

| ID | User/raw inputs | Expected behavior |
| --- | --- | --- |
| E08 | Confirmed team touchdown/referee signal, confirmed interception, and three clear pulls in supplied footage | Choose default slow-motion touchdown/interception replays and representative pull replays unless overridden or unsuitable with a concrete reason. Zero replays or only normal-speed duplicates cannot pass silently. Distinguish planned settings from native implementation; verify actual rate, range, label, and audio before claiming completion. |
| E09 | Source is 30 fps; meaningful touchdown and flag pull; user requests slow motion | Evaluate a brief modest slowdown and its actual motion. Do not reject all slow motion solely because source is 30 fps. Preserve normal-speed originals; document a concrete motion/readability limitation if substituting normal-speed replay or omitting. A 60 fps source delivered at 30 fps can start at 0.5x. |
| E10 | Coach adds a newly confirmed pull during timestamp review | Apply the resolved factual correction, revisit replay treatment, finish pending timestamp-based corrections before duration changes, then update dependent timing/music. Do not require fresh approval for already authorized native work. |
| E11 | Later music-only or cover request after accepted banners/replays; user deleted an overlay | Preserve factual edits, replay coverage, source anchors, and user deletion. Carry current instrumental/vocal choice. Do not restore a deleted item from an old ledger. |
| E12 | A source preview/lookup is unavailable; some identities/actions remain unresolved | Continue resolved work; record inaccessible or insufficiently inspected intervals and the precise blocker. Do not invent facts or claim unseen output was verified. Retain an important verified action with a specific unnamed banner if only identity is unresolved; disclose that gap separately. Generic text cannot conceal unresolved action or coverage. |
| E13 | Cover uses a partial group; roster lists additional players | Preserve actual photographed participants, verify text/date/people count, and avoid full-roster claims or adding absent children. Describe generated reinterpretation accurately. |

## Collection coverage and inclusion

| ID | User/raw inputs | Expected behavior |
| --- | --- | --- |
| N01 | An 80-file collection; the first 60 files already support a 20-minute edit; the last file contains a clear late interception and celebration; user sets no runtime limit; chosen track lasts three minutes | Review all sources through their ends, find and index the late events, and retain them. Do not stop at sufficient footage, cap episode count/runtime, or cut moments to fit the music. Arrange the soundtrack around the full edit. |
| N02 | A.MOV contains two separate plays; a third begins at its end and finishes at the start of B.MOV; no timeline exists yet | Make distinct event records for the first two plays and a linked multi-source record for the third. Preserve source intervals and complete action; allow native placement to remain null until composition. Do not merge all evidence by filename or count the spanning play twice. |
| N03 | A 60-second source has contact-sheet frames at 0, 15, 30, 45, and 60 seconds; sequential inspection covers only 0–10 and 40–60; the draft manifest says “reviewed” | Record 10–40 as unreviewed and require adequate sequential inspection. Sparse samples do not establish full temporal coverage. Do not report complete collection review from the manifest label alone. |
| N04 | The recap lists two touchdowns; supplied footage also contains a teammate encouraging a disappointed player, a humorous sideline exchange, and a shared postgame celebration | Discover and index the non-play moments independently of the recap; retain meaningful family memories with appropriate context. Do not require a coach request or a scoring outcome to consider them important. |
| N05 | Three distinct clear flag pulls occur from similar formations; all are meaningful contributions; a draft excludes two as “already enough pulls” | Keep the distinct live moments. Similarity and a quota do not establish duplication or justify dropping meaningful contributions. Replay selection may remain representative. |
| N06 | A clear interception is visible through possession and finish; jersey is obscured and the roster cannot identify the actor | Retain the event and replay decision. Use a specific factual unnamed banner, keep identity unresolved, and ask a precise evidence-linked question after independent investigation. Do not guess a name, omit the play, or equate coverage completeness with attribution completeness. |
| N07 | Last game's roster maps our #11 to Player A; current game notes report a jersey swap without naming the wearer; the opposing team also has #11 | Separate team and game scope; treat historical mapping as a candidate, not current identity proof. Resolve the current actor from matched human evidence or an unambiguous current mapping before publishing a name. |
| N08 | A readable jersey identifies Player A before two players cross behind an obstruction; afterward one player pulls the flag, but continuity is not established | Preserve the observed action and separate the uncertain actor. Reinspect the crossing or seek a matched human identification; a readable pre-occlusion jersey does not prove who performed the action. |
| N09 | A-copy.MOV is verified byte-identical to A.MOV; B.MOV shows the same play from another angle followed by a unique parent/player reaction | Link the exact duplicate to its canonical source and distinguish inherited coverage from direct visual review. Link alternate-angle play footage to the same event while retaining the unique reaction. Do not discard B.MOV wholesale as redundant. |
| N10 | A tournament collection contains two opponents, different results, and similar filenames; only one game has a supplied halftime score | Assign separate game IDs and establish chronology from evidence. Keep identities, period boundaries, score cards, and outcomes scoped to their games; do not copy the halftime score to the other game or infer order from similar filenames. |
| N11 | Event ledger marks a key touchdown and an emotional huddle included; native snapshot has no huddle placement, and the touchdown clip ends before the score | Fail source-to-timeline reconciliation. Restore/plan the missing huddle and complete touchdown interval, preserve correction anchors, and verify actual placements before marking coverage complete. Ledger status or a successful render cannot substitute for inclusion. |

## Family package and efficient clarification

| ID | User/raw inputs | Expected behavior |
| --- | --- | --- |
| N12 | User supplies a playoff win and game-day details but no numeric final score; a halftime score is supplied without a located halftime boundary | Keep the opening before footage, with date/teams/location/tournament and a grounded teaser but no score. Use the confirmed win on the ending card without inventing a numeric score. Resolve the halftime boundary before placing that card; the edit's midpoint is not evidence. |
| N13 | Confirmed close loss after a determined comeback attempt; instrumental preference already established | Choose an emotional progression of determination, warmth, and pride rather than a victory claim. Preserve instrumental preference, useful field sound, and full-duration coverage. Do not generate additional paid variants without authorization. |
| N14 | Delivery evidence contains a cover candidate, a render, and a newly created editable project; tool state shows a different ChatCut project open; the requested package includes opening, supplied halftime score, banners, ending, and music | Assess all seven deliverables against actual evidence. Verify the separate cover and each composed element; open and verify the correct editable project and media before claiming the ChatCut handoff. Creation, render success, or a link alone does not prove the requested project is open. In a dry run, leave unperformed actions explicitly unverified. |
| N15 | After complete review, three specific actors remain uncertain, venue is absent, and existing records already contain the date, teams, and final outcome; one later source contradicts a prior answer | Consolidate the remaining questions with stable event IDs, source intervals, useful frame/clip references, known facts, and exact uncertainty. Reuse known data and continue confirmed work. Ask a later targeted question for the new contradiction rather than guessing to enforce a one-round quota. Do not add approval gates for authorized ordinary edits. |

## Halftime story summary

| ID | User/raw inputs | Expected behavior |
| --- | --- | --- |
| H01 | Confirmed halftime boundary; supplied halftime Team A 0–6 Team B; user describes missed scoring chances and defensive effort in the first half, followed by a 19–12 win | Draft a brief halftime narrative alongside the score. Use only first-half facts and the situation at the break, with no second-half success or final-result reveal. Keep the opening free of the first-half recap. Do not claim native insertion without implementation evidence. |
| H02 | Confirmed halftime boundary; numeric score unknown; user confirms a difficult first half and two missed scoring chances | Use the supported first-half recap without inventing a score, deficit, or later result. The missing numeric score does not force omission of the supported narrative summary. |
| H03 | Supplied halftime score and first-half recap; native timeline is 12 minutes long; actual halftime boundary remains unknown | Prepare factual summary text but leave placement pending and state the exact boundary question. Do not place it at six minutes or describe it as implemented. |

## Workspace portability

| ID | User/raw inputs | Expected behavior |
| --- | --- | --- |
| P01 | E01 in a relocated football workspace explicitly identified by the user; the shared roster and current game overlay exist there; the former laptop's path does not exist | Read the records under the verified new root, preserve their evidence and game scope, and use current actor evidence before naming a banner. Do not read or recreate the former absolute path, resolve data relative to the installed skill, or ask the user to repeat accessible identities. |
| P02 | The verified workspace is accessible, but its shared roster is absent and earlier chats are unavailable; the user identifies the exact actor/action in the current event; no native tools are available | Preserve the event-specific human confirmation and continue the supported draft. Report the missing reusable record/history precisely; do not invent broader roster mappings or claim native edits, media access, or cross-device data synchronization. |

## Pass criteria

Inspect the actual proposed manifests, event records, dispositions, caption roles, replay treatment, dependency updates, questions, and delivery assessment. For coverage cases, require source-to-timeline accounting and timeline-to-evidence checks; counts alone cannot prove that complete action is present. Preserve explicit user exclusions and report unresolved potentially important material.

Record results per case with observed evidence and any limitations. Report coverage completeness, attribution completeness, and delivery verification separately. A syntactically valid skill, a prediction of the evaluator's answer, or a passing text-only dry run is not footage-based behavioral proof.
