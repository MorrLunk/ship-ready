<!-- Ship Ready v1.0 - founding free copy. Not for resale. See LICENCE-FREE.md -->
# Ship Ready - single file

Paste this whole file into your AI tool's instructions, project knowledge or chat,
then say "run Check mode on my product". Everything the skill needs is below.


---

# THE SKILL

---
name: ship-ready
description: Use when planning, designing, building, changing, reviewing, checking, deploying or maintaining any digital product, app, website, AI feature or AI agent - including "is it ready to deploy", "check this build", adding an AI or agent feature, moving a build between tools, or news that an AI model was released, deprecated or retired.
---


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


---

# THE CHECK LIBRARY

# Check library

Twelve areas. Each check has an ID, a weight, when it applies, what counts as
evidence, and the fix. Run only the areas the classification left live.

Weights: **B** blocker · **S** fix soon · **L** later.
Piles: **A** agent · **O** owner · **X** outside the code.

---

## 1 · Protect what already works

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 1.1 | Purpose and core features are written down | B | O | The file and section naming them | Ask the owner for two lines on purpose and the list of features that must never break |
| 1.2 | A test exists for each core feature | B | A | The test file, and output from a run | Write one test per core feature before anything else changes |
| 1.3 | The project is in version control with a remote | B | A | The remote, and the last commit | Set up a remote and push |
| 1.4 | The code is edited in one place | S | O | No second tool's copy of the project | Pick one place and say so in the project's own notes |

## 2 · What goes into the model

Applies when the product sends anything to a model.

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 2.1 | User text cannot rewrite the instructions | B | A | The prompt construction, showing user content kept separate from instructions | Keep user content in its own field and never concatenate it into the instruction |
| 2.2 | Content fetched from documents, files or the web is treated as data | B | A | The call site, showing retrieved content is not followed as instructions | State in the instruction that retrieved content is reference material only, and strip instruction-shaped text |
| 2.3 | Input size is capped | S | A | The cap in code | Set a maximum length and reject above it with a clear message |

## 3 · What comes out of the model

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 3.1 | Output is never run as code or a query | B | A | The handling code | Treat output as text; use parameters for anything that reaches a database |
| 3.2 | Output is checked before it is shown or stored | S | A | The validation step | Validate shape and length, and fail visibly rather than silently |
| 3.3 | The user is told when text was produced by AI | B | A | The label in the interface | Label AI-produced text where the user sees it |
| 3.4 | A safety-critical decision is never left to the model | B | O | The decision path in code | Move the decision to deterministic code; the model may only re-rank or re-word what already passed |

## 4 · Features that act

Applies only when a feature acts with approval, or acts alone.

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 4.1 | Each tool has the narrowest permission that works | B | A | The permission or scope in code or console | Reduce to the minimum and re-test |
| 4.2 | Anything irreversible asks first | B | O | The approval step before send, pay, publish or delete | Add an approval step naming exactly what will happen |
| 4.3 | Every action is logged with what, when and why | B | A | The log, and one real entry | Log the action, its input summary, and the outcome |
| 4.4 | There is a stop | S | O | The switch that halts the feature | Add a setting that disables the feature without a deploy |

## 5 · Data and privacy

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 5.1 | The model receives the minimum it needs | B | A | The payload construction | Strip identifiers before the call; send fields, not records |
| 5.2 | The provider's terms allow this use | B | X | The provider's page, with the date read | Read the terms; if unclear, ask the provider in writing before launch |
| 5.3 | Where the data is processed is known and recorded | B | X | The region setting, and the provider's statement | Set the region explicitly and record it |
| 5.4 | Users can get their data out and have it deleted | B | A | The export and delete paths | Build both, and say in the interface how long deletion takes |
| 5.5 | Other people's data is processed and discarded, not stored | B | A | The import path showing only the user's own rows persist | Parse on the device, keep the user's rows, discard the rest |
| 5.6 | Logs do not contain personal data | S | A | A sample log line | Redact before logging |

## 6 · Access and secrets

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 6.1 | Keys are never in the code or in the browser | B | A | The call happens server-side; no key in the client bundle | Move the call behind your own endpoint |
| 6.2 | Secret files were never saved into the project history | B | A | Ignore rules cover every key file, and the history contains none | Revoke the key, remove the file from history, then re-issue |
| 6.3 | Sign-in protects every private route | B | A | The guard on each route | Protect at the data layer, not only in the interface |
| 6.4 | A user can only reach their own rows | B | A | The row-level rule, and a test proving another user cannot read them | Add the rule and a test per table |

## 7 · Cost and abuse

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 7.1 | There is a hard spending cap | B | X | The cap in the provider console, with a screenshot or the date set | Set a cap, and an alert below it |
| 7.2 | Requests per user are limited | B | A | The limit in code | Add a per-user limit and a clear message when it is hit |
| 7.3 | The cost of one typical use is known | S | O | A measurement, with the date | Measure one real request and record it |

## 8 · Speed and reliability

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 8.1 | A slow or failed provider call fails gracefully | B | A | The timeout and the fallback | Set a timeout, show a usable state, never hang |
| 8.2 | The model is chosen on measured latency and health | S | A | The measurement, with the date | Measure your candidates on your own tier; the newest is often the most contended |
| 8.3 | The product works when the AI is unavailable | S | O | The non-AI path | Make the AI an enhancement, not the only route |

## 9 · Trust and transparency

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 9.1 | Every AI output shows what it did and on what source | B | A | The interface element | Show the source and a one-line statement of what was done |
| 9.2 | The user can edit, override and undo | B | A | The controls | Add all three; undo is the one most often missing |
| 9.3 | Confidence is expressed as a level with a reason | S | A | The copy shown | Replace any bare percentage with a level and its reason |
| 9.4 | A person reviews anything consequential | B | O | The review step | Put a person in the loop before the consequence, not after |

## 10 · Accessible interface

Measured against the standard the owner named in classification. These are
measurements, not a judgement about whether any law is satisfied.

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 10.1 | Text contrast meets the named standard's ratio | B | A | Measured ratios for body and interface text | Adjust the tokens, not the components |
| 10.2 | Every control is reachable and operable by keyboard, with a visible focus state | B | A | A keyboard walkthrough | Fix tab order and add a focus style that is visible on every surface |
| 10.3 | Colour is never the only way meaning is carried | B | A | The element, showing a second signal | Add a label, a shape or a pattern |
| 10.4 | Motion respects the reduced-motion setting | S | A | The media query | Provide a still alternative |
| 10.5 | The layout works at the narrowest width you support, with no sideways scrolling | B | A | A check at that width | Let rows wrap and stack |

## 11 · Deploy and live

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 11.1 | The deploy is repeatable and documented | B | A | The steps, and one successful run | Write the steps down and run them once from scratch |
| 11.2 | A smoke test proves the deploy worked | B | A | The test and its output | Test the one path that must work, after every deploy |
| 11.3 | Errors reach somebody | B | X | The error destination, and one captured error | Connect error reporting and trigger one on purpose |
| 11.4 | There is a way back | B | A | The rollback route | Prove it by rolling back once |
| 11.5 | Users have a route to report a problem | S | O | The route in the interface | Add one, and say who reads it |

## 12 · Model lifecycle and upkeep

| ID | Check | W | Pile | Evidence | Fix |
|---|---|---|---|---|---|
| 12.1 | Every model in use is named and pinned | B | A | The model identifier in code | Pin it; do not let the product drift onto a new model silently |
| 12.2 | Each model's retirement status is known | S | X | The provider's page, with the date read | Read it; if nothing is announced, record "none announced" and the date |
| 12.3 | A newer model is adopted on evidence, not on being newer | S | O | The comparison run | Run your own checks on it, then decide once |
| 12.4 | The record has been re-run this month | S | O | The date on `SHIP-READY.md` | Re-run Check mode and update the dates |


---

# THE RECORD TEMPLATE

# <Product> - ship-ready record

**Last run:** <date> · <Mode> · **Deploy:** <yes / no>
**Blockers open:** <n> (<n> failing) · **Decisions for you:** <n> · **Unverified:** <n>

> This is an engineering record. It states what evidence was found, where, and on
> what date. It is not a legal opinion and does not claim compliance with anything.

## Next step

**<The one next step.>** <Why it comes first.>
**Done test:** <how the owner checks it themselves.>

## Classification

| Question | Answer |
|---|---|
| AI features and what each does | |
| Autonomy of each | |
| Data the AI touches | |
| Users, and how many at first | |
| Regimes the owner has been told apply | <collected from the owner, not decided here> |
| Lawful basis, processing region, provider retention and training | |
| Accessibility standard the product is held to | <named by the owner> |
| Purpose, and core features that must never break | |

**Switched off by the classification:** <areas, with the answer that ruled them out>

## Models

| Setting | Model | Provider and tier | Region | Retirement | Checked |
|---|---|---|---|---|---|

## Checks

| ID | Check | Weight | Status | Evidence or reason | Date |
|---|---|---|---|---|---|

## Decisions waiting on the owner

| # | Decision | Options | Cost of each | Recommendation |
|---|---|---|---|---|

## Sources

| Source | What it was read for | Date read |
|---|---|---|
