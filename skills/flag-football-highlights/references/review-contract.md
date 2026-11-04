# Source coverage, event ledger, and review contract

Use a compact equivalent of this structure; adapt existing records without dropping evidence or unresolved work. Keep participants as objects consistently. Native tools establish current timeline timing and placement; source review establishes what the collection contains. A selection plan is not proof of implementation.

## Source manifest

Create one record for every supplied source before selecting the edit:

- Stable source ID, filename/path or asset ID, duration, and game ID. A genuinely unknown duration or game ID may be `null`, with the exact unresolved question recorded.
- Review status: `unreviewed`, `partial`, `reviewed`, `unavailable`, or `verified_duplicate`.
- Reviewed intervals, review method, and evidence/reference for each interval; unreviewed intervals and the reason they remain unreviewed. Include the beginning and ending. Overlapping reviewed ranges must not inflate reviewed duration.
- Access/quality limitations, linked event IDs, and, for a verified exact duplicate, its canonical source ID and duplication evidence.

Review the full temporal span at sufficient visual and temporal resolution to discover actions and reactions. Sparse contact sheets, transcripts, filenames, or a recap cannot establish full visual coverage. An inspected interval containing only idle time is still recorded as reviewed; it need not become an event. `reviewed` requires no unexplained temporal gaps. Failed access remains `unavailable`, not a completed review.

Report directly reviewed sources separately from exact duplicates accounted for through a fully reviewed canonical source. Do not call a duplicate independently watched. Similar-looking plays are not duplicates. Overlapping recordings and alternate angles require review for unique action or reactions and links to the same event; they are not automatically exact duplicate sources.

## Event identity and disposition

Index every distinct play and meaningful non-play episode before selection. One movie may contain several events; one event may span several movies. Use one stable canonical event for alternate views of the same episode. A replay references that event and never becomes another live score.

Required fields:

- Stable event ID; game ID and period/order where established, with uncertainty explicit. Keep games, opponents, scores, and outcomes separate.
- Event type, factual description, and story significance/key-event assessment. Consider achievements, effort, support, turning points, setbacks, emotions, humor, and user-requested moments; a scoring-only definition is insufficient.
- Source segments: stable source ID/filename, source in/out, and relationship such as primary, continuation, or alternate view. Required source anchors exist before any timeline item. Related-event links record verified overlaps or other necessary relationships.
- Participants: stable observation ID, player ID/name (nullable), observed team/jersey/uniform, lead/support/other role, identity status, and evidence references. Identify relevant visible participants; distant background people do not require invented identities.
- Action and outcome, with separate status/evidence; precise unresolved questions for identity, action, outcome, chronology, or access as applicable.
- Original human corrections: exact text, source message/reference, resolved event/source/native anchor, scope, and the earlier interpretation superseded. Preserve genuine conflicts and historical snapshots.
- Inclusion disposition: `included`, `excluded`, or `unresolved`, with reason and any exact remaining issue. Include all located key moments and meaningful unique contributions by default. Runtime, soundtrack length, repetition of a type of successful play, a quota, or unknown identity is not a valid exclusion reason. Preserve user exclusions and record concrete limitations.
- Actual placements: `null` before implementation or for excluded events; otherwise an array of current native item IDs, timeline ID/version, timeline from/end frames, and the source segments actually played. Allow multiple placements for split events; distinguish original-play placements from replay placements.
- Banner: planned text, and separate actual native item/timing and composed verification. An unimplemented banner has `actual: null`.
- Replay: eligibility, decision, planned rate/range/label/audio treatment, and exclusion/unresolved reason as applicable; separate actual native item/range/rate/label/audio treatment and composed verification. Record actual slow-motion status, not just intended slowdown.

An `included` disposition is a selection decision. It is not delivered coverage until actual placement and composed evidence establish that the necessary action, finish, and context survive the edit. Unknown player/game IDs and null placements must not prevent indexing a discovered moment.

## Evidence and names

Every evidence record identifies the exact source interval or matched human correction, what it establishes, and its authority. Evidence from SOURCE_B.MOV source0–7 cannot establish an action in source18–27. A recap helps locate expected scores; it does not establish player identity by itself.

Identity states:

- `confirmed`: either an explicit human identification matched to this event; or an unambiguous current-footage match to a confirmed team/season mapping with the same actor visually traced from identifying evidence through the action.
- `tentative`: a plausible candidate whose current mapping or actor continuity is not established. Keep the candidate internal.
- `unresolved`: insufficient or conflicting evidence; preserve the exact question.

Historical numbers alone, an adjacent teammate's readable number, crossings, occlusion, or camera movement must not silently become confirmation. A confirmed identity does not settle an uncertain action or outcome. Check jersey reassignment and team membership. Lead and support roles stay distinct: readiness/containment is not shared pull ownership.

Retain an important event whose actor is uncertain. A specific verified action-only banner is permitted; a guessed name is not. Keep the attribution gap in the records and report it. A neutral banner must not conceal unresolved work or promote an uncertain action into a fact.

## Compact pre-edit example

This illustrative event has been indexed and selected but has **no implemented placement, banner, or replay**. The containing source's manifest records full-source review separately; reviewing this event alone would not establish that the whole file was reviewed.

```json
{
  "eventId": "game-a-source-01-play2",
  "gameId": "game-a",
  "period": null,
  "order": {"value": 2, "status": "source-order-only"},
  "type": "defensive-stop",
  "description": "A team defender pulls the runner's flag; a teammate covers behind.",
  "significance": {"key": true, "reason": "Clear defensive contribution and support"},
  "sources": [{"sourceId": "source-01", "filename": "GAME_A_01.MOV", "inSeconds": 18, "outSeconds": 27, "relationship": "primary"}],
  "relatedEvents": [],
  "participants": [
    {"observationId": "actor-1", "playerId": null, "name": null, "observedTeam": "our team", "jersey": "obscured", "uniform": "team jersey", "role": "flag pull", "identityStatus": "unresolved", "evidenceRefs": ["e1"]},
    {"observationId": "actor-2", "playerId": null, "name": null, "observedTeam": "our team", "jersey": "unreadable", "uniform": "team jersey", "role": "cover support", "identityStatus": "unresolved", "evidenceRefs": ["e1"]}
  ],
  "action": {"value": "Flag pull with teammate cover support", "status": "verified", "evidenceRefs": ["e1"]},
  "outcome": {"value": "Runner stopped", "status": "verified", "evidenceRefs": ["e1"]},
  "evidence": [{"id": "e1", "sourceId": "source-01", "sourceSeconds": [18, 27], "authority": "sequential source footage", "establishes": ["actor continuity", "detached flag", "cover support", "runner stopped"], "reference": "review/source-01-18-27"}],
  "corrections": [],
  "unresolvedQuestions": ["Who is actor-1 at source-01 23s?", "Who is actor-2 behind the runner at source-01 24s?", "Which half contains this event?"],
  "disposition": {"value": "included", "reason": "Unique clear defensive moment; unresolved names do not remove it"},
  "placements": null,
  "banner": {"planned": {"headline": "FLAG PULL!", "detail": "SUPPORT RIGHT BEHIND"}, "actual": null},
  "replay": {"eligible": true, "decision": "unresolved", "reason": "Representative pull selection and suitable rate remain to be evaluated", "planned": null, "actual": null}
}
```

## Completion audit

1. **Manifest → index:** account for every supplied source, reviewed/unreviewed range, and discovered play or meaningful non-play episode. Inspect beginnings/endings and gaps; revisit exclusions for overlooked story or family value. The recap is a separate search checklist, not a complete inventory.
2. **Index → native timeline:** verify every included/key event's actual placement, including action through finish and necessary reaction/context. A setup-only trim fails coverage. List every key-event disposition, including user exclusions, unavailable expected footage, and unresolved candidates. Distinguish “not located in reviewed footage” from “not recorded.” Counts alone do not prove inclusion.
3. **Timeline → evidence:** trace each name, action, outcome, score/card, and replay attribution back to its own event evidence. Do not count alternate views/replays as extra scores. Confirm game/period boundaries independently of edited runtime.
4. **Replay implementation:** confirmed team touchdowns/interceptions default to slow-motion replay; representative meaningful pulls receive explicit decisions. Selective replays do not authorize omitting original key moments. Exclusions and normal-speed substitutions need concrete reasons; 30 fps alone does not justify skipping all slowdown. Inspect native rate, trim, label, framing, slowed audio, and actual composed motion where available.
5. **Correction consistency:** propagate confirmed identities only to independently matched appearances; update affected records, banners, replays, cover/credits, and review maps. Clear superseded active conclusions while preserving history. Apply source/timeline version mapping before retiming and verify dependent music/overlays afterward.
6. **Package verification:** check the required separate cover, actually opened editable ChatCut project, score-free opening without a first-half recap, halftime summary of the game so far at a verified boundary (known score plus supported narrative context, with no later-result spoilers), factual moment banners, final-result ending, and full-duration outcome-sensitive music. Record actual delivery evidence and limitations; a plan or successful render alone is insufficient.

Report three independent statuses:

- **Coverage:** directly reviewed sources/total, verified duplicate sources, unreviewed intervals/limitations, included/excluded/unresolved event counts, and located key events with verified final placements. Full-collection review cannot be claimed with unreviewed material. Any excluded, missing, or unresolved key moment must remain explicit; do not claim every key moment is included when exceptions exist.
- **Attribution:** confirmed identities/actions/outcomes and precise unresolved or conflicting claims. Coverage can be complete while some names remain unresolved; names withheld from banners do not become verified by omission.
- **Delivery:** implemented and verified package elements, pending native/replay/card work, and opening/playback/listening limitations. Distinguish assembled draft, specific remaining work, and verified delivery.

These checks prevent false completion claims; they do not add an approval gate for authorized ordinary editing.
