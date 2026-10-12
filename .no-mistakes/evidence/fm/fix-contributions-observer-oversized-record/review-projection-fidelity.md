# Projection fidelity on awkward review shapes (ghost author, missing commit_id,
# repeat reviewer, stale-head approval, COMMENTED review, non-member bot)

Same payload driven through both versions; what the captain is shown is compared.

## PRE-FIX captain-visible output (e0d95ac)
```json
record bytes: 7144
--- classified reviews the captain is shown (snapshot --all) ---
{
  "row": {
    "actor": "fleet",
    "checked": true,
    "reason": "incoming maintainer signal needs triage",
    "reviews": [
      {
        "author_association": "OWNER",
        "body": "ghost",
        "commit_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
        "freshness": "current",
        "html_url": "https://github.com/o/r/pull/8#pullrequestreview-1",
        "id": 1,
        "state": "APPROVED",
        "submitted_at": "2026-09-16T07:00:00Z",
        "user": null
      },
      {
        "author_association": "COLLABORATOR",
        "body": "approved an older head",
        "commit_id": "bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb",
        "freshness": "STALE",
        "html_url": "https://github.com/o/r/pull/8#pullrequestreview-4",
        "id": 4,
        "state": "APPROVED",
        "submitted_at": "2026-09-16T07:03:00Z",
        "user": {
          "id": 10,
          "login": "helper"
        }
      },
      {
        "author_association": "OWNER",
        "body": "same reviewer, later",
        "commit_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
        "freshness": "current",
        "html_url": "https://github.com/o/r/pull/8#pullrequestreview-3",
        "id": 3,
        "state": "APPROVED",
        "submitted_at": "2026-09-16T07:02:00Z",
        "user": {
          "id": 9,
          "login": "maintainer"
        }
      },
      {
        "author_association": "NONE",
        "body": "outsider",
        "commit_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
        "freshness": "current",
        "html_url": "https://github.com/o/r/pull/8#pullrequestreview-6",
        "id": 6,
        "state": "CHANGES_REQUESTED",
        "submitted_at": "2026-09-16T07:05:00Z",
        "user": {
          "id": 11,
          "login": "review-bot"
        }
      }
    ],
    "stale_verdicts": 1
  },
  "unreadable_records": 0
}
--- pending maintainer signals (pending) ---
[
  {
    "author": null,
    "head": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-1",
    "token": "review:1:2026-09-16T07:00:00Z:APPROVED",
    "type": "review"
  },
  {
    "author": "maintainer",
    "head": null,
    "source": "https://github.com/o/r/pull/8#pullrequestreview-2",
    "token": "review:2:2026-09-16T07:01:00Z:CHANGES_REQUESTED",
    "type": "review"
  },
  {
    "author": "maintainer",
    "head": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-3",
    "token": "review:3:2026-09-16T07:02:00Z:APPROVED",
    "type": "review"
  },
  {
    "author": "helper",
    "head": "bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-4",
    "token": "review:4:2026-09-16T07:03:00Z:APPROVED",
    "type": "review"
  },
  {
    "author": "helper",
    "head": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-5",
    "token": "review:5:2026-09-16T07:04:00Z:COMMENTED",
    "type": "review"
  }
]
```

## FIXED captain-visible output (24f43c9)
```json
record bytes: 6140
--- classified reviews the captain is shown (snapshot --all) ---
{
  "row": {
    "actor": "fleet",
    "checked": true,
    "reason": "incoming maintainer signal needs triage",
    "reviews": [
      {
        "commit_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
        "freshness": "current",
        "id": 1,
        "state": "APPROVED",
        "submitted_at": "2026-09-16T07:00:00Z",
        "user": {
          "login": null
        }
      },
      {
        "commit_id": "bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb",
        "freshness": "STALE",
        "id": 4,
        "state": "APPROVED",
        "submitted_at": "2026-09-16T07:03:00Z",
        "user": {
          "login": "helper"
        }
      },
      {
        "commit_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
        "freshness": "current",
        "id": 3,
        "state": "APPROVED",
        "submitted_at": "2026-09-16T07:02:00Z",
        "user": {
          "login": "maintainer"
        }
      },
      {
        "commit_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
        "freshness": "current",
        "id": 6,
        "state": "CHANGES_REQUESTED",
        "submitted_at": "2026-09-16T07:05:00Z",
        "user": {
          "login": "review-bot"
        }
      }
    ],
    "stale_verdicts": 1
  },
  "unreadable_records": 0
}
--- pending maintainer signals (pending) ---
[
  {
    "author": null,
    "head": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-1",
    "token": "review:1:2026-09-16T07:00:00Z:APPROVED",
    "type": "review"
  },
  {
    "author": "maintainer",
    "head": null,
    "source": "https://github.com/o/r/pull/8#pullrequestreview-2",
    "token": "review:2:2026-09-16T07:01:00Z:CHANGES_REQUESTED",
    "type": "review"
  },
  {
    "author": "maintainer",
    "head": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-3",
    "token": "review:3:2026-09-16T07:02:00Z:APPROVED",
    "type": "review"
  },
  {
    "author": "helper",
    "head": "bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-4",
    "token": "review:4:2026-09-16T07:03:00Z:APPROVED",
    "type": "review"
  },
  {
    "author": "helper",
    "head": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "source": "https://github.com/o/r/pull/8#pullrequestreview-5",
    "token": "review:5:2026-09-16T07:04:00Z:COMMENTED",
    "type": "review"
  }
]
```

## diff (pre-fix -> fixed)
```diff
1c1
< record bytes: 7144
---
> record bytes: 6140
10,11d9
<         "author_association": "OWNER",
<         "body": "ghost",
14d11
<         "html_url": "https://github.com/o/r/pull/8#pullrequestreview-1",
18c15,17
<         "user": null
---
>         "user": {
>           "login": null
>         }
21,22d19
<         "author_association": "COLLABORATOR",
<         "body": "approved an older head",
25d21
<         "html_url": "https://github.com/o/r/pull/8#pullrequestreview-4",
30d25
<           "id": 10,
35,36d29
<         "author_association": "OWNER",
<         "body": "same reviewer, later",
39d31
<         "html_url": "https://github.com/o/r/pull/8#pullrequestreview-3",
44d35
<           "id": 9,
49,50d39
<         "author_association": "NONE",
<         "body": "outsider",
53d41
<         "html_url": "https://github.com/o/r/pull/8#pullrequestreview-6",
58d45
<           "id": 11,
```

Same four classified reviews with the same id, state, submitted_at, commit_id,
freshness and the same stale_verdicts/actor/reason; pending maintainer signals are
byte-identical. Only body, html_url, author_association and user.id are gone from
the stored rows, and no consumer reads them (bin/fm-contributions.jq classifies on
id/state/submitted_at/commit_id/user.login; bin/fm-bearings-snapshot.sh consumes only
summary counts and captain rows).
