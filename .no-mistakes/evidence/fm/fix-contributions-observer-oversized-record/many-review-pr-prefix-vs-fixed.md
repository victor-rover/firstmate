# Many-review PR through a real Firstmate home: pre-fix vs fixed

Same disposable FM_HOME layout, same stubbed GitHub forge returning a 246-review
reviews API payload (1,632,566 bytes), same operator sequence:
fm-pr-check.sh register -> watcher's registered contributions check (poll) ->
fm-contributions.sh pending / snapshot --all -> fm-bearings-snapshot.sh -> ack -> verdict.

## PRE-FIX (base commit e0d95ac, reviews stored raw)
```
==============================================================
LIVE RUN: many-review PR, pre-fix baseline (e0d95ac)
firstmate under test: /tmp/fm-live-drive/prefix-root (bin/fm-contributions.sh as-provided)
forge payload: 246 reviews, raw reviews API response 1632566 bytes
==============================================================

--- captain registers the delivery's PR (fm-pr-check.sh) ---
  armed: state/delivery.check.sh

--- watcher runs the registered contributions check (poll #1) ---
  durable record: /var/folders/qs/2dvs7htn5858_b2jz3x8zyyw0000gn/T//fm-live-home.spKjdI/data/delivery/contributions.json
  durable record size: 1774394 bytes (read cap 1048576)
  reviews stored: 246, stored review keys: ["_links","author_association","body","commit_id","html_url","id","node_id","pull_request_url","state","submitted_at","user"]
  first stored review: <full raw GitHub review object: user object, 5000-char body, _links, html_url ...>
  wake-queue lines after poll #1: 37

--- watcher polls again with nothing new on the forge (poll #2) ---
  contributions: 1 unreadable durable record(s)
  wake-queue lines after poll #2: 37 (was 37)
  => already-notified signals did NOT re-fire

--- captain reads incoming maintainer signals (fm-contributions.sh pending) ---
  pending FAILED: fm-contributions: 1 unreadable contribution record(s); pending signals are unverified

--- supervisor inspects coverage (fm-contributions.sh snapshot --all) ---
  {"unreadable_records":1,"known":1,"checked":0,"complete":false,"row":{"url":"https://github.com/o/r/pull/8","actor":"fleet","reason":"contribution not recently checked","checked":false,"stale_verdicts":0,"reviews":[]}}

--- Bearings, the captain's own readout (fm-bearings-snapshot.sh --json) ---
  {"known":1,"checked":0,"unreadable_records":1,"counts":{"captain":0,"fleet":1,"maintainer":0,"nobody":0},"complete":false,"proven_clear":false}

--- captain acknowledges the newest maintainer review (ack) ---
  no token available to acknowledge (pending unreadable)
  ack attempt:
    fm-contributions: observe the contribution before recording evidence

--- captain records a verdict on the judged head (verdict) ---
  fm-contributions: observe the contribution before recording evidence
  verdict accepted; stored verdict: null

--- cleanup ---
  disposable home removed: /var/folders/qs/2dvs7htn5858_b2jz3x8zyyw0000gn/T//fm-live-home.spKjdI
```

## FIXED (target commit 24f43c9, reviews projected at write time)
```
==============================================================
LIVE RUN: many-review PR, fix applied (24f43c9)
firstmate under test: /Users/rovervictor/.no-mistakes/worktrees/2c52265b777d/01M4PN11FRD2A3FMY1FDD3KJNX (bin/fm-contributions.sh 24f43c9)
forge payload: 246 reviews, raw reviews API response 1632566 bytes
==============================================================

--- captain registers the delivery's PR (fm-pr-check.sh) ---
  armed: state/delivery.check.sh

--- watcher runs the registered contributions check (poll #1) ---
  durable record: /var/folders/qs/2dvs7htn5858_b2jz3x8zyyw0000gn/T//fm-live-home.EWNkS8/data/delivery/contributions.json
  durable record size: 132944 bytes (read cap 1048576)
  reviews stored: 246, stored review keys: ["commit_id","id","state","submitted_at","user"]
  first stored review: {"id":1001,"state":"COMMENTED","submitted_at":"2026-09-16T06:00:10Z","commit_id":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","user":{"login":"review-bot"}}
  wake-queue lines after poll #1: 37

--- watcher polls again with nothing new on the forge (poll #2) ---
  wake-queue lines after poll #2: 37 (was 37)
  => already-notified signals did NOT re-fire

--- captain reads incoming maintainer signals (fm-contributions.sh pending) ---
  pending ok: 37 signal(s)
  {"type":"review","author":"maintainer","head":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","token":"review:1007:2026-09-16T06:01:10Z:APPROVED","source":"https://github.com/o/r/pull/8#pullrequestreview-1007"}
  {"type":"review","author":"maintainer","head":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","token":"review:1014:2026-09-16T06:02:20Z:APPROVED","source":"https://github.com/o/r/pull/8#pullrequestreview-1014"}

--- supervisor inspects coverage (fm-contributions.sh snapshot --all) ---
  {"unreadable_records":0,"known":1,"checked":1,"complete":true,"row":{"url":"https://github.com/o/r/pull/8","actor":"fleet","reason":"incoming maintainer signal needs triage","checked":true,"stale_verdicts":1,"reviews":[{"id":1244,"state":"APPROVED","submitted_at":"2026-09-16T06:40:40Z","commit_id":"bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb","user":{"login":"helper"},"freshness":"STALE"},{"id":1245,"state":"CHANGES_REQUESTED","submitted_at":"2026-09-16T06:40:50Z","commit_id":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","user":{"login":"maintainer"},"freshness":"current"}]}}

--- Bearings, the captain's own readout (fm-bearings-snapshot.sh --json) ---
  {"known":1,"checked":1,"unreadable_records":0,"counts":{"captain":0,"fleet":1,"maintainer":0,"nobody":0},"complete":true,"proven_clear":true}

--- captain acknowledges the newest maintainer review (ack) ---
  ack accepted for token review:1246:2026-09-16T06:41:00Z:COMMENTED
  pending now: 36 signal(s)

--- captain records a verdict on the judged head (verdict) ---
  verdict accepted; stored verdict: {"head":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","source":"https://github.com/o/r/pull/8#pullrequestreview-1245","actor":"fleet","summary":"address requested changes"}

--- cleanup ---
  disposable home removed: /var/folders/qs/2dvs7htn5858_b2jz3x8zyyw0000gn/T//fm-live-home.EWNkS8
```
