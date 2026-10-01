# .github

Shared GitHub Actions workflows for the `jaylickfett-net` org and the `lickfett` account. It is
public because a private reusable workflow can only be called by repos with the same owner, and
these repos span two owners. It holds no secrets and no product code.

## `doc-impact.yml`

The layer-2 check from the architecture repo's ADR-0007 (keeping docs true). A pull request that
changes a **sensitive path** must also change the repo's service sheet (`docs/service-sheet.md`),
or carry the `no-doc-impact` label with the reason stated in the PR.

Callers pin a tag (`@v1`) and list their own sensitive paths. See the header of
[`.github/workflows/doc-impact.yml`](.github/workflows/doc-impact.yml) for the calling workflow.

| Input | Default | Meaning |
|---|---|---|
| `sensitive-paths` | required | Glob pathspecs, one per line, whose change usually makes the sheet untrue |
| `sheet-path` | `docs/service-sheet.md` | The sheet that must change with them |
| `skip-label` | `no-doc-impact` | A PR label that waives the check |

The check names each triggering file as an error annotation and writes a summary to the run page.
It needs `contents: read` only.
