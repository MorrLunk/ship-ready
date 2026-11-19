---
name: ship-ready
description: Use when planning, designing, building, changing, reviewing, checking, deploying or maintaining any digital product, app, website, AI feature or AI agent - including "is it ready to deploy", "check this build", adding an AI or agent feature, moving a build between tools, or news that an AI model was released, deprecated or retired.
---

<!-- Ship Ready v1.0 - founding free copy. Not for resale. See LICENCE-FREE.md -->

# Ship Ready

Takes a product from plan to deploy to low-maintenance live, and produces a dated
record of what is actually true about it, so the owner can answer a question about
their product with evidence instead of memory.

**Read this before anything else.** Ship Ready produces an engineering record. It
does not determine whether a product meets a legal obligation, and it never says
"compliant". A `passed` status means a named check found named evidence on a named
date. Whether that satisfies any law is a judgement for the owner and their advisers.

## Core rules

1. **Evidence or it is not passed.** A check passes only with evidence: a file and a
   line, a test run's output, a screenshot, or a provider's own page with the date it
   was read. A plan that says something was done is not evidence.
2. **Designed is not built.** A rule written in documentation is `unverified` until
   the code exists.
3. **Check and Ship modes report and propose.** They never change code. Fixes go to
   the owner as a plan, and the owner approves before anything is built. Build mode
   applies checks inside work already approved.
4. **One next step at a time**, with a "done" test the owner can check themselves.
5. **Never invent.** No guessed statistics, incidents, retirement dates or provider
   terms. Unknown means `unverified`, with what would verify it.
6. **Never decide a legal question.** Which regimes apply, which risk tier a product
   falls in, and whether an obligation is met are collected from the owner, not
   determined here. Record the owner's answer and apply it consistently.
7. **Plain language.** The owner may not be an engineer. Say where to click, what
   they should see, how to check it worked and how to undo it. Define any unavoidable
   technical term in one line on first use.
8. **Free first.** Name a paid option as paid, and only when no free route exists.
9. **Confidence is a level with its reason** ("Low - one source, 2023"). Never a bare
   percentage.
10. **Date every outside fact.** Regulatory references, provider terms and model
    lifecycle facts carry their source and the date read.

## Step 1 - Find the project and the mode

The project is the folder holding the product. If the code sits in a sub-folder with
its own repository, read the code there; `SHIP-READY.md` still goes at the top.

If there is no code and no plan, say "Nothing to check yet" in one line and offer
Plan mode. Record no findings.

| Mode | Pick when | First action |
|---|---|---|
| **Plan** | A new product or feature is being planned | Classify (Step 3) |
| **Build** | Code is being written under an approved plan | Run the core-feature tests, apply the checks for the feature at hand, run the tests again |
| **Check** | Something exists and someone asks "is this ready?" | Read state, then the code, then compare claims against the code |
| **Ship** | "Deploy", "go live", "ready?" | Run every blocker check; answer deploy yes or no |
| **Live** | After deploy | Monitoring, feedback route, drift checks |
| **Maintain** | Monthly, or on model news | Area 12 |

Say the mode in the first line of the response.

## Step 2 - Load state

1. The product's own context or README, then `SHIP-READY.md` if it exists.
2. Any file in the project whose name contains `PLAN`, `HANDOFF`, `README` or `TODO`.
   Treat their claims as claims to verify in the code.
3. If there is no `SHIP-READY.md`, start from `templates/SHIP-READY.md`.

## Step 3 - Classify

Answered once per product, stored in `SHIP-READY.md`, revisited when the product
changes. Ask the owner only what the code and files cannot answer, one question at a
time.

1. Every AI feature, and what each one does.
2. The autonomy of each: **suggests** / **acts with approval** / **acts alone**.
3. The data the AI touches: none / personal / sensitive (health, children, finance) /
   other people's.
4. Who the users are, and how many at first.
5. **Which regulatory regimes the owner has been told apply to them.** Collected, not
   decided. If the owner does not know, record `unverified` and name getting advice
   as a next step. Do not guess and do not reassure.
6. The lawful basis, the processing region, and the provider's retention and training
   settings, as the owner states or as a provider page shows with a date.
7. **Which accessibility standard the product is being held to**, as the owner states.
   Once a standard is named, its success criteria are measured like any other check.
8. The product's purpose in two lines, and its core features - the ones that must
   never break.

**What the answers switch on:**

| Answer | Effect |
|---|---|
| No AI in the product | Areas 2, 3, 4 and 12 are `not applicable`. All others still apply. |
| Any feature acts with approval or acts alone | Area 4 applies in full. |
| Sensitive data, or children | Area 5 at blocker weight throughout. A free tier that may train on inputs is a blocker. |
| Other people's data | Area 5: only the user's own rows are stored; the rest is processed and discarded. |
| Retrieval over documents, the web or user files | Area 2's indirect-injection checks apply. |
| Public sign-up | Areas 6 and 7 at blocker weight. |
| A named accessibility standard | Area 10 measures against that standard's criteria. |

## Step 4 - Run the checks

The 12 areas are in `references/checks.md`. Load it and run the areas the
classification left live.

| # | Area |
|---|---|
| 1 | Protect what already works |
| 2 | What goes into the model |
| 3 | What comes out of the model |
| 4 | Features that act |
| 5 | Data and privacy |
| 6 | Access and secrets |
| 7 | Cost and abuse |
| 8 | Speed and reliability |
| 9 | Trust and transparency |
| 10 | Accessible interface |
| 11 | Deploy and live |
| 12 | Model lifecycle and upkeep |

Code-level vulnerability scanning and dependency advisories belong to a dedicated
security tool. Suggest running one and record its result as evidence. Do not
duplicate it here.

### Statuses

- `passed` - evidence found, with the evidence and the date.
- `failing` - the check ran and the code does not hold. Give the location and the fix.
- `unverified` - nobody has proven it either way. Give what would verify it.
- `not applicable` - with the classification answer that ruled it out.

### Weights

`blocker` - do not deploy with this open. `fix soon` - deploy is possible, this is
scheduled. `later` - recorded, not urgent.

### Piles

- **Agent** - handled in the code, with approval in Check and Ship modes, then
  reported with evidence.
- **Owner** - a product decision. Asked as one question with the options, what each
  costs, and a recommendation.
- **Outside** - not in the code: a provider setting, a console, a contract, or advice
  the owner needs from someone qualified. Reported with numbered steps.

## Step 5 - Respond

1. **Mode line:** `ship-ready · <Mode> · <Product>`
2. **Summary line:** `Blockers open <n> (<n> failing) · Decisions for you <n> ·
   Unverified <n>`. Blockers open counts blocker-weight checks that are `failing` or
   `unverified`. Ship mode adds `Deploy: yes` or `Deploy: no`, and it is `no` while
   any blocker is open.
3. **One next step:** what it is, why it comes first, and its done test. If it is the
   owner's decision, it is one question with the options and a recommendation.

Everything else goes in `SHIP-READY.md`. Checks that share a status and a reason go
in one row. Order next steps: blockers, then decisions that unblock other checks,
then fix soon, then later.

### Teaching a step

When a step is raised for the first time, explain it in four lines, in product terms:

```
**[ID] Step name**
- Risk: what can go wrong, and who it hurts.
- Decision: what is the owner's to decide, and what the agent handles.
- Trade-off: what each choice costs, now and after launch.
- Check: how the owner knows it worked.
```

Leave out anything unverifiable rather than filling it in.

## Common mistakes

| Mistake | Instead |
|---|---|
| Marking a check passed because a plan says it was done | Find it in the code, otherwise `unverified` |
| Marking a check passed because a rule exists in documentation | Designed is not built |
| Telling the owner they are compliant | Report the evidence and say the determination is theirs |
| Deciding a risk tier or which laws apply | Collect the owner's answer; name getting advice as a step |
| Stating a provider term or retirement date from memory | Read the provider's page and record the date, otherwise `unverified` |
| Listing every finding in the reply | Summary line, one next step, the rest in the record |
| Fixing code during a Check | Propose the fix; wait for approval |
