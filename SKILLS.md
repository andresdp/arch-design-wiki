# Using the search and explain skills

Two agent skills, independent of the study in this repository:

- **`ddspace-search`**: from a problem (context and requirements) to two to four alternative designs, each a
  combination of decisions, with every design examined on the way, its assessment against each requirement, and
  the trade-offs it makes.
- **`ddspace-explain`**: from a problem and an existing solution to the solution's decisions, which ones the
  requirements force, the alternatives it did not take, and what it gives up.

Both write their result as one rationale file, `rationale/<id>.json`. They work with any coding agent that loads
skills (Claude Code, Codex, ...), with or without a design space.

- [1. Install the skills](#1-install-the-skills)
- [2. Give the problem](#2-give-the-problem-a-file-or-text)
- [3. Two ways to run them](#3-two-ways-to-run-them)
- [4. Define your own design space](#4-define-your-own-design-space)
- [5. An example from start to end](#5-an-example-from-start-to-end)

## 1. Install the skills

Copy the two folders of [`skills/`](skills/) where your agent looks for skills, like any other skill:

```bash
git clone https://github.com/andresdp/arch-design-wiki.git
cp -R arch-design-wiki/skills/* ~/.claude/skills/      # Claude Code, every project
cp -R arch-design-wiki/skills/* ~/.agents/skills/      # Codex, every project
```

To install them for one project only, copy them into its `.claude/skills/` or `.agents/skills/` instead. Each
skill is a `SKILL.md` and a `references/design-space.md`, which the skill reads only when it works on a design
space.

## 2. Give the problem: a file or text

Name the skill and give the problem, either as a file:

```text
Use the ddspace-search skill. The problem is in PROBLEM.md.
```

or as text, in the request itself:

```text
Use the ddspace-search skill on this problem: an online shop with 2 million visits a day wants product
recommendations on every page. Recommendations must appear within 100 ms, a new product must be recommended
within a day, and the team of four has no ML platform; everything runs on the company's AWS account.
```

To explain a solution, give the solution the same way (a file such as `SOLUTION.md`, or text):

```text
Use the ddspace-explain skill. The problem is in PROBLEM.md and the solution in SOLUTION.md.
```

When the request names no file and gives no text, the skill looks for `PROBLEM.md` (and `SOLUTION.md`) in the
working folder, and asks when there is none. A problem works best with its requirements labelled: functional
(R1, R2, ...), quality attributes as scenarios (Q1, ...: a stimulus and a measurable response) and constraints
(C1, ...). The templates are in [`examples/your-own/`](examples/your-own/); without labels, the skill takes the
requirements from the text and says how it read them.

## 3. Two ways to run them

| | What you install | What the agent works with | What you get |
|---|---|---|---|
| **Zero-shot** | the skills only | its own knowledge: it names the decisions and options itself | the rationale file |
| **With a design space** | the skills, `ddspace` and a space (a wiki) | the space: every decision is a dimension of the space, every option one of its values | the rationale file, checked against the space, and an explainer page inside the space's wiki |

**Zero-shot.** Nothing else is needed. The agent checks the file against the shape the skill gives, and says that
`ddspace` did not check it.

**With a design space.** Install `ddspace` from this repository (Python 3.10 or later) and run the agent inside the
space's folder: one of this repository's [`spaces/`](spaces/) (copy it first), a space you define (section 4), or
one you import.

```bash
pip install -e arch-design-wiki
export OPENAI_API_KEY=sk-...                      # ddspace describes each design point with one LLM call
```

The skill finds the space in the folder and works on it. The point descriptions use the space's
`models.generation_llm` in `ddspace.yaml`; set a model your key can use. With Codex, allow the sandbox network
access for them: `codex -c sandbox_workspace_write.network_access=true`. To see the result in the space's wiki:

```bash
ddspace rationale build rationale/<id>.json             # site/explainers/<id>.html
```

**A missing space is an error.** `ddspace` always goes with a design space. If `ddspace` is installed but the agent
runs in a folder without a space, the skill warns ("Warning: `ddspace` is installed, but no design space was found
in this folder; I continue zero-shot. To use a space, run me in its folder.") and falls back to zero-shot, so the
work is not lost. To use the space, run the agent again in the space's folder.

## 4. Define your own design space

A design space can be written by hand, in YAML (or the same structure in JSON): a name, the question it answers,
its dimensions (the decisions) with their values (the options), and the relations between dimensions.
[`examples/your-own/design-space.yaml`](examples/your-own/design-space.yaml) is the Git-hosting sample in this
form:

```yaml
name: git-hosting
question: Which decisions does hosting Git for a large engineering organization involve?
dimensions:
  - id: storage                                   # optional: relations can use the id or the name
    name: Source of truth for repository state
    description: Where the authoritative copy of each repository's objects and references lives.
    values:
      - name: Repository files on server disks
        description: Plain Git repositories on the servers' local disks are the authoritative state.
      - Write-ahead log in object storage          # a value can be just its name
  - id: replication
    name: Replication for durability
    values: [Three Git replicas with majority writes, Durability delegated to object storage]
relations:                                        # requires, constrains, affects or co_occurs_with
  - {from: replication, to: storage, type: requires, note: What is replicated follows from where state lives.}
```

Turn it into a wiki:

```bash
ddspace init my-space --yes && cd my-space
ddspace import ../design-space.yaml --kind space --yes
ddspace wiki build --yes
open site/index.html                                    # xdg-open on Linux
```

The wiki has a page per dimension and value, the relations, and a graph view; it says the space was written by
hand. Run the agent in `my-space/`. The import reports what is wrong with a file (a dimension without
values, a relation to an unknown dimension, an unknown relation type), and `ddspace import --help` shows the format.
To change the space, edit the file and import it again.

## 5. An example from start to end

The Git-hosting problem asks for a self-hosted Git service for 3,000 engineers: durability, one-minute failover,
30-second CI fetches, read-after-push consistency, standard Git clients, and a team of five.

```bash
cp -R arch-design-wiki/skills/* ~/.claude/skills/
pip install -e arch-design-wiki && export OPENAI_API_KEY=sk-...

# with a design space: the sample space, defined from its YAML file
ddspace init ~/git-hosting --yes && cd ~/git-hosting
ddspace import ~/arch-design-wiki/examples/your-own/design-space.yaml --kind space --yes
ddspace wiki build --yes
cp ~/arch-design-wiki/examples/toy-git-hosting/cases/1-hosting-search/problem.md PROBLEM.md
claude "Use the ddspace-search skill. The problem is in PROBLEM.md."
ddspace rationale list                                  # the file's id
ddspace rationale build rationale/<id>.json && open site/explainers/<id>.html

# zero-shot, for comparison (in a folder without a space; with ddspace installed, the skill warns first)
mkdir ~/git-hosting-zero && cd ~/git-hosting-zero
cp ~/git-hosting/PROBLEM.md .
claude "Use the ddspace-search skill. The problem is in PROBLEM.md."
```

With the space, expect two or three alternatives that differ where the requirements conflict (replicated Git
repositories, or an object-storage log as the source of truth), each step's trade-offs, and the requirements the
space has no dimension for (failover, the team's workload). Without it, the agent names similar decisions in its own
words, and nothing is left unaddressed: there is no space for a requirement to fall outside of. The
[recorded runs](https://andresdp.github.io/arch-design-wiki/#explainers) of this example show both.

To explain a solution instead, copy `examples/toy-git-hosting/cases/2-spokes-explain/solution.md` as `SOLUTION.md`
and use the explain skill.
