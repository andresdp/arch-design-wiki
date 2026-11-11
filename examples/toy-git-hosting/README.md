# The running example: Git hosting at scale

A small design space, written by hand from public engineering descriptions of large Git hosts: five dimensions
(where repository state lives, replication, reference updates, client data transfer, serving reads), each with three
or four values, the relations between them, and the systems the descriptions report, placed at their points. Each
value lists the passages of those descriptions that discuss it, by source title and passage id (the passages are
not quoted).

| Path | What |
|---|---|
| `toy-git-hosting_taxonomy_20261109_000000.json` | The space as a run file (dimensions, values, relations, evidence) |
| `cases/1-hosting-search/` | The search problem: a self-hosted Git service for 3,000 engineers |
| `cases/2-spokes-explain/` | The same problem, and a solution to explain: replicated Git file servers |
| `runs/space/`, `runs/no-space/` | The rationale files of the paper's running example, with and without the space |

The space's workspace and wiki are in `spaces/git-hosting-sample/` (open `site/index.html`); the explainers of the
runs are in `spaces/git-hosting-sample/site/explainers/` and `spaces/no-space/explainers/sample-*.html`.

To check a run against the space:

```bash
cd spaces/git-hosting-sample
ddspace rationale check ../../examples/toy-git-hosting/runs/space/hosting-search.json
```
