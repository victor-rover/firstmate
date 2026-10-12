# Already-notified review signals after the captain drains the wake queue

One poll rings 35 contribution wakes for the maintainer reviews; the captain's
session then drains and acknowledges them with the real bin/fm-wake-drain.sh;
the watcher polls again with nothing new on the forge.

## PRE-FIX (e0d95ac)
```
==============================================================
LIVE RUN: wake re-fire after drain, pre-fix baseline (e0d95ac)
forge payload: 246 reviews, 1632597 bytes
==============================================================
poll #1 rang 35 contribution wake(s) for new maintainer reviews
durable record: 1770916 bytes

--- the captain's session drains the queued wakes (fm-wake-drain.sh) ---
  1791762403	1	check	contribution-d61231afa11057547312335f48a736781dc51f6675cb0a8a1ffbb921607e2285	check: contributions delivery d61231afa11057547312335f48a736781dc51f6675cb0a8a1ffbb921607e2285
  1791762403	2	check	contribution-d80eea45c55d459707695650f383175a780bb6b24f80560f6d375b9859d367f5	check: contributions delivery d80eea45c55d459707695650f383175a780bb6b24f80560f6d375b9859d367f5
  1791762404	3	check	contribution-73043e2d4072dc2e692dfc341896597af42ee6088c21d5f2819e9ca1d8270121	check: contributions delivery 73043e2d4072dc2e692dfc341896597af42ee6088c21d5f2819e9ca1d8270121
  1791762404	4	check	contribution-00304c5031015b0494511c98b136c8e68700b7862670563a3eaa779d44ebcd18	check: contributions delivery 00304c5031015b0494511c98b136c8e68700b7862670563a3eaa779d44ebcd18
  1791762404	5	check	contribution-9dfbc693d5e74042dda64fd426ed9edb2d959fac27b8fb194c143bf8115fe7d7	check: contributions delivery 9dfbc693d5e74042dda64fd426ed9edb2d959fac27b8fb194c143bf8115fe7d7
  ack command the drain asked for: bin/fm-wake-drain.sh --ack-through 35 --recovery-generation 10289.1791762403.UGdPYi
  wake-queue rows left after the drain's acknowledgement: 0

--- the watcher polls again; the forge has nothing new ---
poll #2 rang 35 contribution wake(s)
  => RE-FIRED already-notified review signals:
     contributions: 1 unreadable durable record(s)
     contribution-wake: check: contributions delivery d61231afa11057547312335f48a736781dc51f6675cb0a8a1ffbb921607e2285
     contribution-wake: check: contributions delivery d80eea45c55d459707695650f383175a780bb6b24f80560f6d375b9859d367f5
  poll diagnostics: contributions: 1 unreadable durable record(s)

cleanup: disposable home removed
```

## FIXED (24f43c9)
```
==============================================================
LIVE RUN: wake re-fire after drain, fix applied (24f43c9)
forge payload: 246 reviews, 1632597 bytes
==============================================================
poll #1 rang 35 contribution wake(s) for new maintainer reviews
durable record: 129431 bytes

--- the captain's session drains the queued wakes (fm-wake-drain.sh) ---
  1791762449	1	check	contribution-d61231afa11057547312335f48a736781dc51f6675cb0a8a1ffbb921607e2285	check: contributions delivery d61231afa11057547312335f48a736781dc51f6675cb0a8a1ffbb921607e2285
  1791762450	2	check	contribution-d80eea45c55d459707695650f383175a780bb6b24f80560f6d375b9859d367f5	check: contributions delivery d80eea45c55d459707695650f383175a780bb6b24f80560f6d375b9859d367f5
  1791762450	3	check	contribution-73043e2d4072dc2e692dfc341896597af42ee6088c21d5f2819e9ca1d8270121	check: contributions delivery 73043e2d4072dc2e692dfc341896597af42ee6088c21d5f2819e9ca1d8270121
  1791762450	4	check	contribution-00304c5031015b0494511c98b136c8e68700b7862670563a3eaa779d44ebcd18	check: contributions delivery 00304c5031015b0494511c98b136c8e68700b7862670563a3eaa779d44ebcd18
  1791762450	5	check	contribution-9dfbc693d5e74042dda64fd426ed9edb2d959fac27b8fb194c143bf8115fe7d7	check: contributions delivery 9dfbc693d5e74042dda64fd426ed9edb2d959fac27b8fb194c143bf8115fe7d7
  ack command the drain asked for: bin/fm-wake-drain.sh --ack-through 35 --recovery-generation 69890.1791762449.xrGpNE
  wake-queue rows left after the drain's acknowledgement: 0

--- the watcher polls again; the forge has nothing new ---
poll #2 rang 0 contribution wake(s)
  => no re-fire: already-notified review signals stayed quiet

cleanup: disposable home removed
```
