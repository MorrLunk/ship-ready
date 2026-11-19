# Ship Ready

**Version 1.0 · November 2026 · founding free copy**

It tells you what you can prove about what you built, before someone asks you to.

---

## What this is

If you have shipped anything with AI in it, sooner or later someone asks you to prove
it is safe. A client, a procurement form, your own lead. Most teams know the answer
roughly. Almost nobody has it written down.

Ship Ready is a set of instructions you give to the AI tool you already build with.
It reads your project, works out what the product actually does, runs a list of
checks against it, and writes you a one-page record: what is built, what is missing,
and what nobody has checked yet.

It never tells you that you are compliant. It tells you what you can prove, and
leaves the judgement with you and whoever advises you.

**You do not need to be technical.** You describe the product in plain words. Your
AI tool does the reading.

---

## Install it - pick the one tool you use

### Claude Code

1. Find your project folder on your computer.
2. Inside it, make a folder called `.claude` if there is not one already. The dot at
   the start matters.
3. Inside `.claude`, make a folder called `skills`.
4. Copy this whole folder into it, and rename it `ship-ready`. You should end up with
   `.claude/skills/ship-ready/SKILL.md`.
5. Start Claude Code in that project and type `/ship-ready`, or just say "run Ship
   Ready in Check mode on this project".
   **You should see** it say `ship-ready · Check · <your product>` on the first line.

### Cursor

1. Open your project in Cursor.
2. Make a folder called `.cursor` in the project if there is not one, and a folder
   called `rules` inside it.
3. Copy `SKILL.md`, `references/` and `templates/` into it.
4. Open the chat and say: "Follow the Ship Ready instructions and run Check mode on
   this project."
   **You should see** it start by asking you about the product rather than editing
   code. Cursor changes how rules files work from time to time, so if it ignores
   them, check their current docs for where rules live.

### ChatGPT, Claude, Gemini or any chat tool with projects

1. Make a new Project.
2. Upload `SKILL.md`, `checks.md` and `SHIP-READY.md` to the project's files or
   knowledge.
3. Start a chat in it and say: "Follow SKILL.md. Run Check mode on the product I am
   about to describe."
   **You should see** it ask you the eight classification questions, one at a time.

### Lovable, Bolt, Figma Make and similar

These do not take skill files. Open `SKILL.md`, copy everything in it, and paste it
into the project's instructions or custom-knowledge box. Then ask it to run Check
mode. It works, it is just less tidy.

**If none of that works:** paste the contents of `SKILL.md` into any AI chat, then
say "run Check mode on my product" and answer its questions. That is the whole thing
in its simplest form.

---

## Run it

Say one of these:

| Say this | You get |
|---|---|
| "Run Check mode" | A record of what is true about your product today |
| "Run Plan mode" | The rules your build should hold, before you build it |
| "Run Ship mode" | A plain deploy yes or no, with every open blocker named |

It answers with three things: the mode, a summary line counting blockers and
unverified checks, and **one** next step with a test you can check yourself. The rest
goes into a file called `SHIP-READY.md`.

The first run asks you eight questions about the product. Answer them in plain words.
Two of them ask which rules apply to you and which accessibility standard you are
held to. **It will not answer those for you on purpose** - those are judgements with
consequences, and a tool that guesses them is wrong often and quietly.

---

## What I would like back

You have this free, permanently. Two things in return, whenever you get to them:

1. **Run it on one real project** and tell me what it caught that you had not written
   down anywhere.
2. **Tell me what confused you.** Especially anything that assumed you were an
   engineer. That is the thing I most need to fix.

And if it is useful, tell me who where you work should see it.

Message me on [LinkedIn](https://www.linkedin.com/in/matilda-orring-lunki-70564b6/). I answer there.

---

## Honest limits

- Version 1.0, run end to end on a real project on 19 November 2026 before you got
  it. It found 8 failing checks and 24 open blockers in a product I thought I knew.
  You are among the first people outside me to run it. Tell me where it breaks.
- It is not legal advice, an audit, a penetration test or an accessibility audit. It
  tells you which of those you have not done.
- Every outside fact it states carries the date it was checked. Rules move. A
  reference checked in November 2026 is accurate in November 2026.
- Licence: see `LICENCE-FREE.md`. Short version - use it on anything of your own,
  for free, forever. Do not resell it.
