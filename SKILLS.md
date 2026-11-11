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
- [2. Give the problem](#2-give-the-problem)
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

## 2. Give the problem

Call the skill with its slash command and write the problem right after it, as plain text:

```text
/ddspace-search I need alternatives for the following problem: an online shop with 2 million visits a day wants
product recommendations on every page. Recommendations must appear within 100 ms, a new product must be
recommended within a day, and a team of four with no ML platform runs everything on the company's AWS account.
```

To explain a solution, give the problem and then the solution:

```text
/ddspace-explain Explain this solution. Problem: an online shop with 2 million visits a day wants product
recommendations on every page, within 100 ms, with new products recommended within a day; a team of four runs it
on AWS. Solution: a nightly batch job trains a matrix-factorization model on SageMaker and writes the top 20
products per user to DynamoDB; the web servers read them with each page; new products are shown by popularity
until the next night's run.
```

The more the text says about the requirements, the better: what the system must do, the quality attributes it
must reach (best as scenarios with a measurable response, e.g. "within 100 ms"), and the constraints (a team, a
provider, a budget). Labels are not needed: the skill takes the requirements from the text, gives them ids (R1,
Q1, C1, ...) and says how it read them.

In an agent without slash commands for skills, name the skill instead: "Use the ddspace-search skill: I need
alternatives for ...". For a long problem, a file works too: "/ddspace-search The problem is in PROBLEM.md." (the
templates are in [`examples/your-own/`](examples/your-own/)); with no text and no file named, the skill looks for
`PROBLEM.md` (and `SOLUTION.md`) in the working folder.

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

A design space can be written by hand, in YAML (or the same structure in JSON). It needs only a name and its
dimensions (the decisions), each with its values (the options):

```yaml
name: git-hosting
dimensions:
  - name: Source of truth for repository state
    values: [Repository files on server disks, Write-ahead log in object storage]
  - name: Replication for durability
    values: [Three Git replicas with majority writes, Durability delegated to object storage]
```

Optionally, a dimension or a value can have a `description`, a dimension an `id`, and the file `relations` between
dimensions (`requires`, `constrains`, `affects` or `co_occurs_with`), which the wiki and the agent then use:

```yaml
dimensions:
  - id: storage
    name: Source of truth for repository state
    description: Where the authoritative copy of each repository's objects and references lives.
    values:
      - name: Repository files on server disks
        description: Plain Git repositories on the servers' local disks are the authoritative state.
      - Write-ahead log in object storage
  - id: replication
    name: Replication for durability
    values: [Three Git replicas with majority writes, Durability delegated to object storage]
relations:
  - {from: replication, to: storage, type: requires, note: What is replicated follows from where state lives.}
```

[`examples/your-own/design-space.yaml`](examples/your-own/design-space.yaml) is the whole Git-hosting sample in this
form.

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

A self-hosted Git service, first with a design space and then zero-shot.

```bash
cp -R arch-design-wiki/skills/* ~/.claude/skills/
pip install -e arch-design-wiki && export OPENAI_API_KEY=sk-...

# the sample space, defined from its YAML file
ddspace init ~/git-hosting --yes && cd ~/git-hosting
ddspace import ~/arch-design-wiki/examples/your-own/design-space.yaml --kind space --yes
ddspace wiki build --yes
claude
```

In the agent, in `~/git-hosting`:

```text
/ddspace-search I need alternatives for this problem: a software company hosts its own Git service for 3,000
engineers in four regions. CI starts 40,000 jobs a day, each fetching the repository it builds; the largest
repository is 200 GB and most engineers touch only a small part of it. No pushed commit may be lost when a machine
or disk fails; when a server fails, pushes and fetches must continue within one minute without an operator; a CI
job in any region must fetch the latest state within 30 seconds, even right after a push, and see every push that
succeeded before it started. Five engineers build and run the service, and engineers keep using standard Git
clients.
```

Then render the result in the space's wiki:

```bash
ddspace rationale list                                  # the file's id
ddspace rationale build rationale/<id>.json && open site/explainers/<id>.html     # xdg-open on Linux
```

Expect two or three alternatives that differ where the requirements conflict (replicated Git repositories, or an
object-storage log as the source of truth), each step's trade-offs, and the requirements the space has no
dimension for (operator-free failover, the team's workload).

For the zero-shot version, run the same command in an empty folder (with `ddspace` installed, the skill first warns
that there is no space there). The agent names similar decisions in its own words, and nothing is left unaddressed:
there is no space for a requirement to fall outside of. The
[recorded runs](https://andresdp.github.io/arch-design-wiki/#explainers) of this example show both.

To explain a solution, follow the problem with it: "/ddspace-explain Explain this solution. Problem: ... Solution:
every repository is stored as plain Git on the local disks of three file servers; a push updates references through
a three-phase commit and succeeds once a majority agrees; reads go to the closest up-to-date replica; engineers use
full clones." The full text of both is in
[`examples/toy-git-hosting/cases/`](examples/toy-git-hosting/cases/).
