# Reading an explainer

An explainer is a web page that shows one **rationale file**: what a coding agent decided, and how it got there,
when it followed the search or the explain skill for one problem. This guide covers four things:

- the difference between the two modes;
- what each part of the page shows;
- how the page is built from the file;
- what changes when the agent worked without a design space.

The [landing page](https://andresdp.github.io/arch-design-wiki/#explainers) links every explainer of the study and
of the running example. Each explainer also has a short "How to read this page" box under its title.

- [1. Search and explain](#1-search-and-explain)
- [2. The page, part by part](#2-the-page-part-by-part)
- [3. How an explainer is built](#3-how-an-explainer-is-built)
- [4. With and without a design space](#4-with-and-without-a-design-space)
- [5. A quick reading order](#5-a-quick-reading-order)

## 1. Search and explain

Both modes use the same vocabulary:

- a **dimension** is a design decision (for example, Model serving);
- a **value** is one option for that decision;
- a **design point** is a combination of values, at most one per dimension;
- a **partial design point** is a point that settles only some dimensions.

Both modes also record every point the agent examined, as a trajectory within a budget, and both end in
architecture decision records (ADRs). What differs is the direction they work in.

| | **Search** (magnifier icon) | **Explain** (light-bulb icon) |
|---|---|---|
| Question | Which designs could solve this problem? | Why does this solution look the way it does? |
| Input | A problem: context and requirements | A solution and, optionally, the problem it solves. Without the problem, the agent infers the requirements from the solution and marks them *inferred*. |
| What the agent examines | Design points grouped in **approaches**, over **rounds**: it seeds each approach, refines the good points, starts new approaches, and sometimes undoes one value to see which value made a point work | The **solution** as one design point; **regions** (parts of the solution) that the requirements may justify; and **contrasts** (a region with one value swapped) to tell whether a value is **forced** by the requirements or chosen **freely** |
| How each point is judged | Every requirement: *meets*, *partly* or *misses*. Each point is rated **strong**, **mixed** or **weak**. | Every requirement: *meets*, *partly* or *misses*. Each point gets a verdict: **grounded**, **partial** or **ungrounded**. |
| Budget (default, maximum) | 12 points, at most 20 | 8 points, at most 12 (fewer when the solution is grounded early) |
| Result | **2 to 4 alternatives**. Each is built from partial design points, one per ADR. An ADR's options are chosen by one or more alternatives, or discarded. | **The solution**, with one to three regions that justify it. Each ADR sets the solution's option against the options it was contrasted with. |
| Extra views | **Comparison** tab (alternatives side by side), **lanes** (approaches by rounds), **requirements strip** | **Questions, options and criteria** (which choices are forced and which free), **regions** |
| Gaps it can report | Requirements no ADR addresses; approximate fits | The same, plus **decisions the space does not cover** |

## 2. The page, part by part

The page has two columns. The text is on the left, and a graph of the decisions involved is on the right. Selecting
an alternative, an option, a design point or a requirement in either column highlights it in the other.

### Header

- **The mode icon and label**: *Search* or *Explain*, with the design space's run, or *no design space*.
- **The title and context** of the problem, or of the solution.
- **A banner, when the space changed.** The rationale was written against an earlier version of the space. Its ids
  were checked against the current version, but labels and values may differ from what the agent saw.

### Requirements

One chip per requirement. Its id says its kind: **R** for a functional requirement, **Q** for a quality-attribute
scenario (with its attribute) and **C** for a constraint. The agent assigns the ids when it reads the problem.
When no problem was given, the heading says *inferred from the solution*. In that case the requirements are the
agent's reading of what the solution appears to be built for, and the explanation rests on them.

### Decisions (ADRs) tab

This tab opens first. It answers **what was decided**.

- **Alternatives** (search) or **The solution** (explain). Each alternative is listed with the partial design points
  that compose it, one per ADR, each as dimension → value pairs. *Left open* lists the dimensions the alternative
  deliberately does not settle, and why.
- **The ADRs.** Each ADR addresses a few related requirements, its **drivers**, shown as chips after its title. Each
  ADR has:
  - a context;
  - its decision;
  - every option it weighed, with the option's values, pros, cons and reason.

  In search, an option is either *chosen in A1, A2...* (by the alternatives that take it) or *discarded*. In
  explain, it is the solution's option or a contrasted one. An **approximate fit** badge marks an option whose
  values only roughly match what the agent meant, with a note saying how.
- **Requirements not addressed.** The requirements that are not a driver of any ADR, each with its reason:
  - no dimension of the space bears on it;
  - the solution does not address it;
  - it was traded off for a stronger requirement.

### Comparison tab (search, two or more alternatives)

One row per dimension involved and one column per alternative. The rows where the alternatives differ come
first, so the top of the table shows what the choice between them is about. *open* marks a dimension that an
alternative leaves unsettled.

### Trajectory tab

This tab answers **how the agent got there**. The hint at its top gives the number of points evaluated against
the budget.

In **search**, the tab has three views:

- **Approaches and rounds.** One lane per approach, with one column per round. Each design point is a chip, coloured
  by its rating (strong, mixed or weak). Arrows connect the points:
  - a solid arrow refines a point on the same lane;
  - a dashed arrow starts a new approach from a point;
  - a dotted arrow is an ablation, which undoes one value to see which value made a point work.

  The last column gives each approach's outcome: the alternative it became, *dropped* with the reason, or *not
  proposed*.
- **Requirements, point by point.** A strip with one row per requirement and one column per point. The colour
  shows whether the point meets the requirement, meets it partly, misses it, or was not judged on it. Reading a row
  from left to right shows whether the search improved on that requirement.
- **The search, round by round.** The story of every point (see *A step of the story* below).

In **explain**, the tab has three views:

- **The explanation, step by step.** The solution as a point, then the regions and contrasts the agent evaluated.
- **Questions, options and criteria.**
  - Each question is a dimension that the solution settles.
  - Its options are the solution's value and the values the contrasts tried.
  - Lines link each option to the requirements (the criteria): meets, partly or misses.

  Each of the solution's values is marked **forced** (a contrast broke a requirement), **free** (no requirement
  depended on it) or neither (not tested). Faint links come from an option that was judged only as part of the
  whole solution.
- **Regions that justify the solution.** The one to three partial design points that the requirements call for,
  each with its drivers and the reason.

The **Dimension grid** is collapsed at the bottom of both modes. It shows every point dimension by dimension. In
search it marks the values that each refinement added or changed; in explain it marks the values that each
contrast swapped.

#### A step of the story

Every point evaluated has the same anatomy:

| Part | What it is |
|---|---|
| Header | The step number, the move (*seed*, *refined #n*, *new approach*, *ablation*, *solution*, *region*, *contrast*), the rating or verdict, and the alternative the point became, if any |
| **Thought** | The agent's hypothesis before it evaluated the point |
| **Move** | The point's values, or what changed from the step it starts from (*add*, *change*, *drop*) |
| **Observed** | What the evaluation showed, including what the agent did not expect |
| Judgements | One chip per requirement: meets, partly or misses |
| Trade-offs | The values that cause each trade-off, the requirements they gain and the requirements they give up |
| Description | A short description of the point and its own trade-off, which `ddspace point` wrote when the agent checked the point |
| Attested by | With a space whose sources record systems: the sources that attest this combination of values |

### Gaps in the space

This section is at the bottom of the page. With a design space, it lists where the space fell short of the problem
or of the solution:

- **Decisions the space does not cover** (explain only): parts of the solution that no dimension or value describes,
  each with a quote from the solution and the nearest dimension;
- **Requirements no ADR addresses**, with the reason and the nearest dimension;
- **Approximate fits**: values the agent kept although they only roughly match.

The agent never changes the space to make a problem or a solution fit. It records the gap instead. *No gaps* means
three things: every decision maps onto the space, every requirement is addressed, and every value fits.

### The graph

The right column is a radial graph, read from the centre outwards:

- the dimensions involved, then their values;
- one design-point node (▲) per step, coloured by its rating;
- the requirements (■), each linked to every point by how that point judged it.

Explored paths are blue, and the point being shown is outlined. Selecting a node lights its path to the centre and
its paths to design points and requirements, and shows its details below the graph. *Show every value* adds the
values that no point took. With a space, every dimension and value links to its page in the space's wiki.

## 3. How an explainer is built

1. **The agent works through the skill.** With a space, it reads the dimensions and values through `ddspace query`
   and evaluates each combination it considers with `ddspace point`. That command checks that the values exist and
   respect the space's relations, then describes the point. The agent records each point as a step of the
   trajectory: its hypothesis, values, judgement of each requirement, trade-offs, observation, and rating or
   verdict.
2. **It writes one rationale file**, `rationale/<id>.json` (schema `ddspace-rationale/6`). The file holds:
   - the problem and its requirements;
   - the points, the trajectory and, for search, the approaches;
   - the alternatives, or the solution and its regions;
   - the ADRs;
   - the unaddressed requirements and, for explain, the uncovered decisions.
3. **`ddspace rationale check`** checks the file, and the agent fixes it until the check passes.
   - With a space, every id must exist in the space, every trade-off must name values of its own point, every
     driver must be a requirement, and so on. The file also records a hash of the space's graph, so a later change
     to the space shows up as the banner.
   - Without a space, only the file's structure is checked.
4. **`ddspace rationale build`** renders the page. Inside the space's workspace, the page lands in the space's wiki
   (`site/explainers/<id>.html`) and is listed on the wiki's index. Every later `ddspace wiki build` renders it
   again.

**Where each part comes from.** Every judgement on the page is the agent's: ratings, verdicts, meets, partly or
misses, trade-offs, reasons, forced or free. The page computes none of them. It only lays out what the file says:

| On the page | Taken from |
|---|---|
| Lanes, rounds and arrows | Each step's approach, round, move and parent |
| Requirements strip and graph links | Each step's assessment |
| Comparison table | The alternatives' values, ordered so that the rows where they differ come first |
| Questions, options and criteria | The contrasts, and the most specific point that judged each option |
| Gaps | The unaddressed requirements, the uncovered decisions and the options marked as approximate fits |

The check guarantees that the file is consistent with itself and with the space. It does not guarantee that the
agent's judgements are right. Those are for the reader to assess, which is what the page is for.

## 4. With and without a design space

| | With a design space | Without a space (zero-shot) |
|---|---|---|
| Dimensions and values | The space's own, with their ids | Named by the agent from its own knowledge, in its own words |
| Where the page lives | Inside the space's wiki: every dimension and value links to its wiki page | A standalone page, with no wiki links |
| Check | Ids, relations, trade-offs, drivers and the graph hash | Structure only |
| Gaps in the space | Uncovered decisions, requirements no dimension bears on, approximate fits | None. With no space, nothing can fall outside one. The requirements no ADR addresses are still listed in the ADRs tab. |
| Attested by | The sources that record the combination, when the space has sources | Not shown |

Comparing the two explainers of the same case shows what the space adds. With the space, the agent's decisions
are the space's dimensions, and the gaps show where the space ran out. Zero-shot, the agent may name similar
decisions, but nothing ties them to a shared vocabulary.

## 5. A quick reading order

**Search:**

1. Read the alternatives at the top of the ADRs tab.
2. Open **Comparison** to see where the alternatives differ.
3. Read the ADRs behind those rows: drivers, chosen and discarded options, pros and cons.
4. In **Trajectory**, check the lanes for the approaches that were dropped, and why.
5. End with **Gaps in the space**.

**Explain:**

1. Read the solution and the requirements. If they were inferred, check them first.
2. In **Trajectory**, read **Questions, options and criteria** to see which values are forced and which are free.
3. Read **Regions that justify the solution**.
4. Read the ADRs.
5. End with **Gaps in the space**, in particular the decisions the space does not cover.
