# .github

Shared GitHub defaults and workflows for the `jaylickfett-net` org. It is public because default
community health files must come from a public `.github` repo, and so that repos outside the org
(the `lickfett` account) can still call the workflow. It holds no secrets and no product code.

## Default PR template

[`.github/pull_request_template.md`](.github/pull_request_template.md) is the **default pull request
template for every `jaylickfett-net` repo** that has none of its own (GitHub's default community health
files, which is why this repo must stay public). It asks which docs the change makes untrue
(ADR-0007, layer 1). A repo with its own template, such as the architecture repo, uses that instead.

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
