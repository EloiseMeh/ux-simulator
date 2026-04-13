---
name: ux-sim
description: Simulate virtual users walking through your app to find UX flaws. Trigger phrases include "do user test", "test userflow", "ux test", "test the UX", "simulate users", "find UX issues", "walk through as a user", "user testing", "check the flow", "test my app", "run UX sim", "UX review", "UX audit", "how's the UX", "any UX problems", or any variation indicating the user wants UX feedback or user flow testing.
---

# UX Simulator

Simulate diverse virtual users walking through a project to find UX issues, friction points, and accessibility gaps. This is AI-powered user testing — not a replacement for real users, but a fast way to catch obvious problems.

---

## Phase 1: Gather Context

Before simulating anything, collect as much context as possible. Use whatever the user provides — more inputs mean better simulations.

### 1a. Read the project

Read the codebase in the current working directory (or a path the user specifies):
- Entry points: `index.html`, `App.tsx`, `main.ts`, route files
- Components and screens: look for `/screens/`, `/pages/`, `/components/`, `/views/`
- State management: how does the app track progress, navigation, user choices?
- Assets: images, audio, animations — what does the user actually see and hear?
- Config: `package.json`, framework config — what kind of app is this?

Map out every screen/state and the transitions between them.

### 1b. Check for additional inputs

Ask the user if they can provide any of these (all optional — use whatever is available):

- **Live URL** — fetch the actual page to see what real users see, not just source code
- **Screenshots** — of key screens, for visual analysis (layout, readability, contrast)
- **Figma link** — compare intended design vs actual implementation
- **User flow description** — the intended happy path in plain language (e.g. "user taps chest → picks game → plays")

If the user provides a URL, fetch it. If they provide screenshots, read them. If they provide a Figma link, use MCP to extract specs. Combine all sources for the fullest picture.

### 1c. Understand the target audience

**Ask the user:** "Who are your target users? For example: casual mobile gamers, enterprise developers, kids learning to code, etc."

This is critical — personas must reflect the real audience, not generic archetypes. If the user says "drunk friends at a party playing on their phones," the personas should reflect that context (low attention, small screens, group setting, maybe impaired coordination).

Also ask:
- **Platform:** Mobile, desktop, or both?
- **Context of use:** When and where do people use this? (commute, office, party, classroom)

---

## Phase 2: Generate Personas

Based on the target audience, create **5 personas** that each stress-test a different dimension of the UX. Every persona should feel like a real person from the target audience — not a generic label.

Each persona needs:
- **Name and brief bio** (1 line — make them feel real)
- **Device and context** (what are they using, where are they)
- **Behavior traits** (how they interact — fast/slow, patient/impatient, etc.)
- **What they test** (the specific UX dimension they expose)

### Required dimensions to cover:

| Dimension | What it tests | Example persona traits |
|-----------|--------------|----------------------|
| **Discovery** | Can a new user figure out what to do without instructions? | First visit, no context, skims rather than reads |
| **Speed/Patience** | Does the app hold up when users rush or multitask? | Taps fast, skips animations, doesn't wait for loading |
| **Comprehension** | Is everything clear to someone unfamiliar with the domain? | Non-native English speaker, or non-technical user |
| **Accessibility** | Can someone with disabilities or limitations use it? | Vision impaired, motor impaired, keyboard-only, color blind |
| **Repeat use** | Does the experience hold up on return visits? | Has used the app before, expects shortcuts, notices staleness |

Adapt these to the target audience. For a drinking game app, "accessibility" might focus on drunk users with impaired coordination on small screens, not screen readers.

---

## Phase 3: Simulate Each Persona

For each persona, walk through the entire user flow step by step:

1. **Arrive** — What's the first thing they see? What do they think the app does?
2. **Orient** — How do they figure out what to do? Is there a clear call to action?
3. **Act** — Walk through each interaction. What do they tap/click? What happens?
4. **React** — At each step: are they confused, delighted, frustrated, bored?
5. **Complete or abandon** — Do they finish the flow? Where might they drop off?

At each step, flag issues with:
- **File and line reference** (e.g. `index.html:67`)
- **Priority level:**
  - **P1 (Blocking)** — user gets stuck, can't proceed, or the app breaks
  - **P2 (Confusing)** — user is unsure what to do, makes wrong assumptions, or has a bad experience
  - **P3 (Polish)** — minor friction, could be smoother but doesn't block anything

Be specific. "The UX could be better" is useless. "The tap target is 30px wide on mobile — too small for thumb input (index.html:142)" is actionable.

---

## Phase 4: Output Report

**Save the report as a markdown file**, not terminal output. Create a `usability-test/` folder inside the project directory and save the report as `usability-test/report-YYYY-MM-DD.md` (using today's date).

### Report structure

The report has 4 sections in this order:

#### Section 1: Header

```markdown
# UX Simulation Report

| | |
|---|---|
| **Project** | <name> |
| **Type** | <web app / mobile game / CLI / etc.> |
| **Target audience** | <from Phase 1c> |
| **Screens found** | <count> |
| **Personas tested** | 5 |
| **Inputs used** | <code, URL, screenshots, Figma — list what was available> |
| **Date** | <today's date> |
```

#### Section 2: Issue summary chart

A numbered chart of ALL issues found across all personas. Each issue appears only once, even if multiple personas flagged it. Group by severity.

Color key: 🔴 = Blocking (user gets stuck), 🟠 = Confusing (bad experience), 🟡 = Polish (minor friction)

```markdown
## Issues (total: 🔴 X  🟠 X  🟡 X)

| #  | Sev  | Issue                            | Where              | Flagged by     |
|----|------|----------------------------------|--------------------|----------------|
| 1  | 🔴   | No confirm on grid pretzel pick  | PretzelGrid:33     | Sam, Priya     |
| 2  | 🔴   | Drink result auto-advances       | DrinkRoulette:27   | Priya          |
| 3  | 🟠   | No game rules or tutorial        | WelcomeScreen      | Jake, Marco    |
| ...| ...  | ...                              | ...                | ...            |
```

Then a **Top 5 Fixes** list ordered by user impact.

#### Section 3: Persona walkthroughs

Full detailed think-out-loud walkthroughs for each persona. Keep these rich and real — the user should feel like they're watching a real person use their app.

Each persona section includes:
- Name, age, one-line bio
- Device and context
- What dimension they test
- Screen-by-screen walkthrough
- One-line verdict at the end

**Formatting rules for the walkthrough:**

Issues are markdown checkboxes so the user can mark which ones to fix. Good observations use ✅ indented to align with the color dots. This keeps everything scannable at the same vertical line.

```markdown
### PERSONA 1: Jake, 22 — First time playing, handed a phone at a bar
**Device:** iPhone SE · **Context:** Loud bar, no explanation · **Tests:** Discovery

**Flow:** Welcome → Name Entry → Poison Pick → Truth/Dare Pick

**Welcome:**
- [ ] 🟠 #3 No explanation of what the game IS. Jake sees a pretzel logo and a start
      button but has no idea what "Poisoned Pretzel" means or how it works
      (WelcomeScreen.tsx:7-29)
- [ ] 🟡 #9 No player count indicator — Jake doesn't know this is a 2-player game
      until he's asked for Player 2's name (WelcomeScreen.tsx)
      ✅ Big "Start Game" button is clear and obvious
      ✅ Game logo looks polished and fun

**Name Entry:**
      ✅ Clear "Enter your name" prompt, autoFocus on input is good
      ✅ maxLength={8} prevents overflow — smart
- [ ] 🟡 #10 "Player 1" label is generic — "What's your name?" would feel more
      natural (NameEntryScreen.tsx:27-29)
```

**CRITICAL formatting rule:** The ✅ lines must be indented with 6 spaces so the ✅ icon aligns vertically with the 🟠/🟡/🔴 dots on the checkbox lines. The text after `- [ ] ` is 6 characters, so `      ✅` (6 spaces + ✅) creates perfect alignment.

#### Section 4: What's working well

A bullet list of things that are good about the UX. The user needs to know what NOT to change.

### Important guidelines for the report:
- **Be honest but constructive** — flag real issues, don't invent problems to seem thorough
- **Include what's working** — the user needs to know what NOT to change too
- **Be specific** — file:line references, exact pixel values, exact wording that's confusing
- **Prioritize ruthlessly** — the Top 5 Fixes should be ordered by user impact, not code complexity
- **Don't suggest rewrites** — suggest the minimum change that fixes the issue
- **Deduplicate** — if 3 personas hit the same issue, it's ONE issue in the chart with all 3 names in the "Flagged by" column
- After saving the file, tell the user the file path and say: "Read through, check the boxes on issues you want fixed, then tell me which numbers to fix."
