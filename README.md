# arch-design-wiki

<img src="assets/icon.svg" alt="" width="56" align="right">

Material for the paper **"Searching and Explaining Designs with a Design Space"** (J. Andrés Díaz-Pace; under
review for the 4th International Workshop on Designing Software, Designing 2027).

A design space records the decisions of a domain, the alternatives for each, the relations between them and the
systems that adopted them. The paper studies how an architect can put a given space to work:

- **search**: from a system's context and requirements to a few alternative designs, each a point of the space;
- **explain**: from an existing solution back to the space's decisions, with what the space offered instead and what
  it does not cover.

Both write a **rationale file** (every design point examined, its assessment against each requirement, the
trade-offs it makes) that is checked against the space and rendered as a browsable **explainer** next to the
space's wiki. The initial implementation gives a coding agent two skills over `ddspace`, a command that serves a
design space to agents (query its dimensions and values, check and describe design points).

**Browse the design spaces and the explainers online: <https://andresdp.github.io/arch-design-wiki/>**. This
repository holds everything else: the study, the code, and how to reproduce it.

## The study

Six cases for ML-enabled systems: four search problems (card-fraud scoring, on-device visual inspection, retail
demand forecasting, large-scale document classification) and two solutions to explain (fraud, documents). Each
problem has functional requirements, quality-attribute scenarios and constraints. A coding agent (Codex CLI
0.165.0, `gpt-6-luna`, high reasoning effort) followed the search or explain skill in 24 sessions: each case with
the expert ML-workflow space (**E**) and without a space (**N**), two repetitions each. Point descriptions used
`gpt-5.6-luna` in both conditions.

| What | Where |
|---|---|
| The problems and the solutions to explain | [`study/designing2027/cases/`](study/designing2027/cases/) |
| The session prompt | [`study/designing2027/prompt.md`](study/designing2027/prompt.md) |
| The 24 rationale files and session summaries | [`study/designing2027/results-v2/`](study/designing2027/results-v2/) |
| The session runner and its controls | [`run_sessions.py`](study/designing2027/run_sessions.py), [`controls.py`](study/designing2027/controls.py) |
| The paper's table, recomputed | [`analyze.py`](study/designing2027/analyze.py) |
| The search and explain skills | [`src/delvedspace/templates/skills/`](src/delvedspace/templates/skills/) |

## Contents

| Path | What |
|---|---|
| `spaces/ml-workflow-expert/` | The expert ML-workflow design space (28 dimensions, 124 values) as a workspace and wiki, with the 12 explainers of the sessions that used it |
| `spaces/git-hosting-toy/` | The running example: a small Git-hosting space written by hand, with its explainers |
| `spaces/no-space/` | The explainers of the 12 sessions without a space, and of the running example without a space |
| `study/designing2027/` | The cases, the prompt, the session runner, the 24 rationale files and summaries, and `analyze.py`, which recomputes the paper's table |
| `examples/toy-git-hosting/` | The running example's run file, cases and recorded rationale files |
| `src/`, `pyproject.toml` | `ddspace`, with the search and explain skills (`src/delvedspace/templates/skills/`) |
| `USAGE.md` | Every `ddspace` command |

## Reproduce

```bash
pip install -e ".[dev]"
python study/designing2027/analyze.py      # the paper's table, offline
```

[REPRODUCE.md](REPRODUCE.md) checks every rationale file, rebuilds the explainers, and reruns the 24 sessions.

## Cite

The paper is under review for the 4th International Workshop on Designing Software (Designing 2027, co-located with
ICSE 2027). Until it is published, please cite this repository ([CITATION.cff](CITATION.cff)); GitHub's "Cite this
repository" button gives the reference in APA and BibTeX.

## Licence and credits

Code: MIT ([LICENSE](LICENSE)). The expert space is derived from the decision model of S. J. Warnett and U. Zdun,
"Architectural Design Decisions for the Machine Learning Workflow", *IEEE Computer* 55(3), 2022
([doi:10.1109/MC.2021.3134800](https://doi.org/10.1109/MC.2021.3134800)); see
[spaces/ml-workflow-expert/ATTRIBUTION.md](spaces/ml-workflow-expert/ATTRIBUTION.md). The running example's
evidence cites public engineering descriptions of Git hosts, by title and passage id, without quoting them.
