# Regression test: fails before the fix, passes after

tests/fm-contributions.test.sh::test_many_reviews_stay_readable, run against a
throwaway copy of this branch whose bin/fm-contributions.sh is swapped between the
base-commit and target-commit versions.

```
$ bash tests/fm-contributions.onlymany.test.sh   # bin/fm-contributions.sh @ e0d95ac (pre-fix)
not ok - a many-review observation wrote a 1888237-byte record
not ok - 1 contribution regressions
exit=1

$ bash tests/fm-contributions.onlymany.test.sh   # bin/fm-contributions.sh @ 24f43c9 (fixed)
ok - a many-review PR stores only classified review fields and stays readable
exit=0
```

Full targeted file on the branch as committed (51 tests, 3m51s):
```
ok - a late owner settled beside a retired final record stays unretired and known
ok - retire is idempotent and refuses non-captain, unknown, malformed and signal-bearing pairs
ok - a many-review PR stores only classified review fields and stays readable
bash tests/fm-contributions.test.sh  38.31s user 49.81s system 38% cpu 3:50.61 total
```
