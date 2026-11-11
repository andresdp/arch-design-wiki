# Reproducing the study

The paper reports 24 sessions: six cases (four search problems and two solutions to explain), each run with the
expert design space (**E**) and without a space (**N**), two repetitions each. This guide has three parts:

1. [Set up](#1-set-up) the `ddspace` command.
2. [Offline checks](#2-offline-checks-no-api-key): recompute the paper's table, check every rationale file, rebuild
   the explainers. Minutes, no API key.
3. [A full rerun](#3-a-full-rerun) of the 24 sessions with Codex CLI. About three hours and an OpenAI key; the agent
   is not deterministic, so expect different rationale files with similar counts.

## 1. Set up

Python 3.10 or later:

```bash
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
ddspace --version
pytest -q tests/unit_tests          # the tests of the study code and the rationale checker (no network)
```

## 2. Offline checks (no API key)

**The paper's numbers.** Table 1 and the counts the text quotes, from the kept rationale files and summaries:

```bash
python study/designing2027/analyze.py               # add --json for machine-readable output
```

**Check every rationale file.** E files are checked against the expert space (every id must exist, every trade-off
must name values of its point, ...); N files have no space, so only their structure is checked:

```bash
cd spaces/ml-workflow-expert
for f in ../../study/designing2027/results-v2/rationale/*-E-r*.json; do ddspace rationale check "$f" | head -3; done
cd ../..
for f in study/designing2027/results-v2/rationale/*-N-r*.json; do ddspace rationale check "$f" | head -3; done
```

Each prints `"ok": true` and the space's fingerprint (`graph_sha256`), which is the one the E files record. One file,
`forecast-search-E-r2.json`, also carries a warning (`early_stop`: the agent stopped after one round, with 3 of its
12 points); its session summary records the same warning.

**Rebuild an explainer.** The explainers in `spaces/` were rendered from these files; to render one again, into a
folder of your own:

```bash
cd spaces/ml-workflow-expert
ddspace rationale build ../../study/designing2027/results-v2/rationale/fraud-search-E-r1.json --out my-explainers
open my-explainers/explainers/fraud-search.html        # xdg-open on Linux
```

**Browse the spaces.** `spaces/ml-workflow-expert/site/index.html` and `spaces/git-hosting-toy/site/index.html`
open in a browser from disk, or online from the [landing page](https://andresdp.github.io/arch-design-wiki/).
`ddspace query` reads a space from the command line, as the agent did:

```bash
cd spaces/ml-workflow-expert
ddspace query dimensions --table
ddspace query values "How to serve model predictions or scores?" --table
ddspace point v:5.1 v:19.1 v:22.1 --no-llm        # check a combination of values (no description)
```

## 3. A full rerun

You need [Codex CLI](https://github.com/openai/codex) (the study used `codex-cli 0.165.0`), logged in, and an
OpenAI API key with a low spending limit for the point descriptions (`ddspace point` calls `gpt-5.6-luna` once per
new design point). The sessions run outside this repository: the runner refuses work folders inside it.

```bash
WORK=~/arch-design-wiki-rerun
mkdir -p $WORK/workspaces/N $WORK/scratch
cp -R spaces/ml-workflow-expert $WORK/workspaces/E     # the study's own E space (same fingerprint)
export STUDY_OPENAI_API_KEY=sk-...                     # passed to the sessions as OPENAI_API_KEY

# one session first, to check the setup
python study/designing2027/run_sessions.py --workspaces $WORK/workspaces --scratch $WORK/scratch \
  --model gpt-6-luna --effort high --timeout 3600 --results results-smoke --cases fraud-search --conditions E --reps 1

# the 24 sessions (about three hours); a stopped run resumes where it left off
python study/designing2027/run_sessions.py --workspaces $WORK/workspaces --scratch $WORK/scratch \
  --model gpt-6-luna --effort high --timeout 3600 --results results-rerun

python study/designing2027/analyze.py --results results-rerun
```

`study/designing2027/build_workspace.py --out $WORK/workspaces` builds the E space from the decision model in
`study/designing2027/inputs/` instead of copying it. The ids are the same, but the space gets a new run id, so its
fingerprint differs and `ddspace rationale check` warns `graph_changed` on the study's E files.

What each session gets:

- a fresh copy of its workspace (E) or an empty folder (N), with `PROBLEM.md` and, for explain, `SOLUTION.md`;
- the skill (`.agents/skills/ddspace-search` or `ddspace-explain`), and for E the space's reference;
- the prompt of `study/designing2027/prompt.md` (its SHA-256 is recorded in every summary);
- a private Codex home with only your login, an empty home folder, web search off, and network access for the point
  descriptions only (any other network use is counted in the summary).

The runner keeps, under `study/designing2027/<results>/`, each session's rationale file, an allow-listed summary
(commands, `ddspace` calls, design points, the final check, tokens, time) and its explainer.

## What is where

| Path | Contents |
|---|---|
| `study/designing2027/cases/` | The six cases: `problem.md` (context, requirements R/Q/C), `solution.md` for explain |
| `study/designing2027/prompt.md` | The session prompt (a search and an explain section; one sentence differs between E and N) |
| `study/designing2027/results-v2/` | The 24 rationale files and session summaries the paper reports |
| `study/designing2027/inputs/` | The expert decision model the E space is built from, and its manifest |
| `src/delvedspace/templates/skills/` | The search and explain skills |
| `spaces/ml-workflow-expert/` | The E workspace: `site/` (the wiki, with the E explainers), `raw/graph.json`, `AGENTS.md` |
| `spaces/git-hosting-toy/` | The running example's workspace and its explainers |
| `spaces/no-space/explainers/` | The N explainers and the running example's runs without a space |
| `examples/toy-git-hosting/` | The running example's run file, cases and recorded rationale files |
