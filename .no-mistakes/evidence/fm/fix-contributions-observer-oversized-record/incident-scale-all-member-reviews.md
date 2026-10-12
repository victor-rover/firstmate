# Worst case at the incident's scale: 246 reviews, every one from a member

The incident PR class (rovertown-web PR 240: 246 reviews, 1,455,134-byte record)
with the least favourable authorship - every review from an OWNER, so every one
also becomes a pending signal the captain must triage.

```
==============================================================
LIVE RUN: worst case at incident scale: 246 reviews, every one from a member
firstmate under test: /Users/rovervictor/.no-mistakes/worktrees/2c52265b777d/01M4PN11FRD2A3FMY1FDD3KJNX (bin/fm-contributions.sh 24f43c9)
forge payload: 246 reviews, raw reviews API response 1632566 bytes
==============================================================

--- captain registers the delivery's PR (fm-pr-check.sh) ---
  armed: state/delivery.check.sh

--- watcher runs the registered contributions check (poll #1) ---
  durable record: /var/folders/qs/2dvs7htn5858_b2jz3x8zyyw0000gn/T//fm-live-home.XJDfIm/data/delivery/contributions.json
  durable record size: 495141 bytes (read cap 1048576)
  reviews stored: 246, stored review keys: ["commit_id","id","state","submitted_at","user"]
  wake-queue lines after poll #1: 246

--- watcher polls again with nothing new on the forge (poll #2) ---
  wake-queue lines after poll #2: 246 (was 246)
  => already-notified signals did NOT re-fire

--- captain reads incoming maintainer signals (fm-contributions.sh pending) ---
  pending ok: 246 signal(s)
  {"type":"review","author":"maintainer","head":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","token":"review:1001:2026-09-16T06:00:10Z:APPROVED","source":"https://github.com/o/r/pull/8#pullrequestreview-1001"}
  {"type":"review","author":"maintainer","head":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","token":"review:1002:2026-09-16T06:00:20Z:APPROVED","source":"https://github.com/o/r/pull/8#pullrequestreview-1002"}

--- supervisor inspects coverage (fm-contributions.sh snapshot --all) ---
  {"unreadable_records":0,"known":1,"checked":1,"complete":true,"row":{"url":"https://github.com/o/r/pull/8","actor":"fleet","reason":"incoming maintainer signal needs triage","checked":true,"stale_verdicts":1,"reviews":[{"id":1244,"state":"APPROVED","submitted_at":"2026-09-16T06:40:40Z","commit_id":"bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb","user":{"login":"helper"},"freshness":"STALE"},{"id":1245,"state":"CHANGES_REQUESTED","submitted_at":"2026-09-16T06:40:50Z","commit_id":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","user":{"login":"maintainer"},"freshness":"current"}]}}

--- Bearings, the captain's own readout (fm-bearings-snapshot.sh --json) ---
  {"known":1,"checked":1,"unreadable_records":0,"counts":{"captain":0,"fleet":1,"maintainer":0,"nobody":0},"complete":true,"proven_clear":true}

--- captain acknowledges the newest maintainer review (ack) ---
  ack accepted for token review:1246:2026-09-16T06:41:00Z:COMMENTED
  pending now: 245 signal(s)

--- captain records a verdict on the judged head (verdict) ---
  verdict accepted; stored verdict: {"head":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","source":"https://github.com/o/r/pull/8#pullrequestreview-1245","actor":"fleet","summary":"address requested changes"}

--- cleanup ---
  disposable home removed: /var/folders/qs/2dvs7htn5858_b2jz3x8zyyw0000gn/T//fm-live-home.XJDfIm

```
