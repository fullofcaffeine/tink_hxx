# tink_hxx fork

This fork keeps small fixes to tink_hxx that Cafetera needs, on top of a
pinned upstream commit. Each fix has a test. The upstream project is the
owner of tink_hxx; this fork only carries patches.

- Upstream: https://github.com/haxetink/tink_hxx
- Base commit: `75ef63c78851fcd7c1846d74959cbd4cea0b4ced` (haxelib.json version 0.25.1)
- Fork: https://github.com/fullofcaffeine/tink_hxx

## Branches and tags

- `maintained/<upstream version>`: the base commit plus the patches below.
  For this base, the branch is `maintained/0.25.1`.
- `master`: a mirror of upstream `master`. It moves only by fast-forward to
  an upstream commit and never carries fork patches.
- Tags: `v<upstream version>-foc.<n>`, for example `v0.25.1-foc.1`. A tag
  marks one exact patched commit that consumers can pin. The first tag for
  this base is `v0.25.1-foc.1`.
- The `upstream` remote has its push URL set to `DISABLED`. Never push to
  upstream from this clone.

`LICENSE` and `haxelib.json` stay the same as upstream.

The upstream GitHub Actions workflow runs on every push. In this fork it is
renamed to `.github/workflows/ci.yml.disabled`, so a push does not start
hosted CI. Run the tests locally instead.

## How to run the tests

With Lix and Haxe 4.3.7:

```bash
lix download
haxe dev.hxml
```

## Patches

| Commit | Reason | Cafetera task and bug | Test | Upstream status |
| --- | --- | --- | --- | --- |
| `56d1792` | `parseExpr` removed every `/* ... */` span before Haxe parsed a markup expression, so `{"a/*b*/c"}` became `ac`. Now the stripped copy only decides if the expression is empty; Haxe parses the unchanged text. | `cafetera-0jpj.145`, bug `cafetera-dtss.9` | `jsxCommentMarkersInStrings`, `jsxCommentOnlyChildIsEmpty`, `jsxCommentBetweenTokens`, and upstream `jsxComments` in `tests/RunTests.hx` | Not reported |

## Owner policy

- Keep each patch small, with a test, and record it in the table above.
- Rebase patches onto a new upstream base only on a new
  `maintained/<version>` branch; never rewrite a published branch or tag.
- Report a patch upstream only when the owner decides to. When upstream
  accepts an equal fix, drop the patch on the next base.
- Never force-push. Consumers pin an exact tag or commit, never a branch.
