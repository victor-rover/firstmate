# Adversarial scale: a 2000-review PR after the fix

Eight times the incident PR's review history (2000 reviews, 13,274,865-byte raw
reviews payload, 288 of them from members so each also becomes an event).

```
==============================================================
LIVE RUN: adversarial scale: 2000-review PR, fix applied
firstmate under test: /Users/rovervictor/.no-mistakes/worktrees/2c52265b777d/01M4PN11FRD2A3FMY1FDD3KJNX (bin/fm-contributions.sh 24f43c9)
forge payload: 2000 reviews, raw reviews API response 13274865 bytes
==============================================================

--- captain registers the delivery's PR (fm-pr-check.sh) ---
  armed: state/delivery.check.sh

--- watcher runs the registered contributions check (poll #1) ---
  durable record: /var/folders/qs/2dvs7htn5858_b2jz3x8zyyw0000gn/T//fm-live-home.dSVnYS/data/delivery/contributions.json
  durable record size: 1052031 bytes (read cap 1048576)
  {"unreadable_records":1,"known":1,"checked":0,"complete":false,"row":{"url":"https://github.com/o/r/pull/8","actor":"fleet","reason":"contribution not recently checked","checked":false,"stale_verdicts":0,"reviews":[]}}
  {"known":1,"checked":0,"unreadable_records":1,"counts":{"captain":0,"fleet":1,"maintainer":0,"nobody":0},"complete":false,"proven_clear":false}
```

Field breakdown of that record (compact JSON character counts):
```json
{
  "reviews": 2000,
  "reviews_bytes": 309719,
  "events": 288,
  "events_bytes": 206215,
  "pending": 288,
  "pending_bytes": 206215
}
```

The projected reviews field holds 2000 reviews in ~310 KB, so the review history
itself stays well inside the 1 MiB read cap. The record still crosses the cap at
this scale because observation.events and the unacknowledged pending list each
carry one 500-char-body entry per member review (~206 KB each) - the unbounded
events axis raised and declined in review round 1, not the reviews field this
change projects.
