<!-- Ship Ready v1.0 - founding free copy. Not for resale. See LICENCE-FREE.md -->

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
