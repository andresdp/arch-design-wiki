<p align="center"><img src="assets/icon.svg" alt="" width="120"></p>

# Architecture Design Wiki

Material for the paper **"Searching and Explaining Designs with a Design Space"**.

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
| `spaces/git-hosting-sample/` | The running example: a small Git-hosting space written by hand, with its explainers |
| `spaces/no-space/` | The explainers of the 12 sessions without a space, and of the running example without a space |
| `study/designing2027/` | The cases, the prompt, the session runner, the 24 rationale files and summaries, and `analyze.py`, which recomputes the paper's table |
| `examples/your-own/` | Templates for your own `PROBLEM.md` and `SOLUTION.md`, to try the skills |
| `examples/toy-git-hosting/` | The running example's run file, cases and recorded rationale files |
| `src/`, `pyproject.toml` | `ddspace`, with the search and explain skills (`src/delvedspace/templates/skills/`) |
| `USAGE.md` | Every `ddspace` command |

## Use the skills with your own coding agent

The search and explain skills are not tied to the study: you can install them for your own coding agent
(Claude Code or Codex) and try them on your own problem, with a design space or without one.

**1. Install `ddspace`** (Python 3.10 or later). `ddspace point` describes each design point with one LLM call, so
set an OpenAI key; without one, the descriptions are left empty and everything else works.

```bash
git clone https://github.com/andresdp/arch-design-wiki.git && cd arch-design-wiki
pip install -e .
export OPENAI_API_KEY=sk-...
```

The model that writes the descriptions is the space's `models.generation_llm` in `ddspace.yaml` (without a space,
`DDSPACE_POINT_MODEL`, e.g. `openai/gpt-4.1-mini`); change it if your key has no access to the one set there.

**2. Write the problem**, in a folder of your own: `PROBLEM.md` with the context and the requirements (functional,
quality-attribute scenarios, constraints), and, to explain an existing solution, `SOLUTION.md`. The templates are
in [`examples/your-own/`](examples/your-own/); [`examples/toy-git-hosting/cases/`](examples/toy-git-hosting/cases/)
has a complete example.

**3a. With a design space.** Work in a copy of a space (one of `spaces/`, or one you build with `ddspace`), so the
agent's choices are values of the space, checked against it:

```bash
cp -R spaces/git-hosting-sample ~/my-design && cd ~/my-design
ddspace agent setup --skills --claude --yes      # the skills for Claude Code (.claude/skills/) and Codex (.agents/skills/)
cp ~/my-problem/PROBLEM.md .                     # and SOLUTION.md, to explain
```

**3b. Without a space** (zero-shot: the agent names its own decisions and options), in any folder:

```bash
cd ~/my-problem
ddspace agent setup --skills --no-space --claude --yes
```

**4. Ask the agent**, in that folder:

```text
Use the ddspace-search skill. The problem is in PROBLEM.md.
```

or, to explain a solution:

```text
Use the ddspace-explain skill. The problem is in PROBLEM.md and the solution in SOLUTION.md.
```

The agent explores within a budget of design points, writes `rationale/<id>.json` and runs `ddspace rationale
check` until the file is clean. With Codex, allow the sandbox network access for the point descriptions
(`codex -c sandbox_workspace_write.network_access=true`).

**5. Open the explainer:**

```bash
ddspace rationale build rationale/<id>.json            # with a space: site/explainers/<id>.html, inside the wiki
ddspace rationale build rationale/<id>.json --out .    # without a space: explainers/<id>.html
```

### An example: Git hosting on the sample space

The sample space's search problem asks for a self-hosted Git service for 3,000 engineers (durability, one-minute
failover, 30-second CI fetches, read-after-push consistency, standard Git clients, a team of five):

```bash
cp -R spaces/git-hosting-sample ~/git-hosting && cd ~/git-hosting
ddspace agent setup --skills --claude --yes
cp ~/arch-design-wiki/examples/toy-git-hosting/cases/1-hosting-search/problem.md PROBLEM.md
claude "Use the ddspace-search skill. The problem is in PROBLEM.md."
ddspace rationale list                                  # the new file's id, next to the two recorded ones
ddspace rationale build rationale/<id>.json
open site/explainers/<id>.html                          # xdg-open on Linux
```

The result should resemble the [recorded search](https://andresdp.github.io/arch-design-wiki/spaces/git-hosting-sample/site/explainers/hosting-search.html):
two or three alternatives that differ where the requirements conflict (replicated Git repositories, or an
object-storage log as the source of truth), each step's trade-offs, and the requirements the space has no
dimension for. To explain a solution instead, also copy `cases/2-spokes-explain/solution.md` as `SOLUTION.md` and
use the explain skill.

## Reproduce

```bash
pip install -e ".[dev]"
python study/designing2027/analyze.py      # the paper's table, offline
```

[REPRODUCE.md](REPRODUCE.md) checks every rationale file, rebuilds the explainers, and reruns the 24 sessions.

## Cite

Until the paper is published, please cite this repository ([CITATION.cff](CITATION.cff)); GitHub's "Cite this
repository" button gives the reference in APA and BibTeX.

## Licence and credits

Code: MIT ([LICENSE](LICENSE)).

The expert space is derived from the decision model of S. J. Warnett and U. Zdun,
"Architectural Design Decisions for the Machine Learning Workflow", *IEEE Computer* 55(3), 2022
([doi:10.1109/MC.2021.3134800](https://doi.org/10.1109/MC.2021.3134800)); see
[spaces/ml-workflow-expert/ATTRIBUTION.md](spaces/ml-workflow-expert/ATTRIBUTION.md). The running example's
evidence cites public engineering descriptions of Git hosts, by title and passage id, without quoting them.
