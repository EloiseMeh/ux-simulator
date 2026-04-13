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

Print the full report in this format:

```
UX Simulation Report
====================
Project:         <name>
Type:            <web app / mobile game / CLI / API / etc.>
Target audience: <from Phase 1c>
Screens found:   <count>
Personas tested: 5
Inputs used:     <code, URL, screenshots, Figma, user description — list what was available>

────────────────────────────────────────

PERSONA 1: <Name> — <one-line bio>
Device: <phone/desktop/tablet>  Context: <where they're using it>
Tests: <dimension>

Flow: <screen 1> → <screen 2> → <screen 3> → ...

  <screen 1>:
  ✓ <what works well>
  ✗ [P2] <issue description> (file.tsx:42)

  <screen 2>:
  ✓ <what works well>
  ✗ [P1] <issue description> (file.tsx:108)
  ✗ [P3] <issue description> (file.tsx:115)

  Verdict: <completes flow / drops off at screen X / gets stuck at Y>

────────────────────────────────────────

PERSONA 2: ...
(repeat for all 5)

────────────────────────────────────────

PRIORITY SUMMARY
================
P1 (Blocking):    <count> issues
P2 (Confusing):   <count> issues
P3 (Polish):      <count> issues

TOP 5 FIXES (by impact):
1. <most impactful fix — what to change, where, and why>
2. ...
3. ...
4. ...
5. ...

WHAT'S WORKING WELL:
- <things that are good — don't just report problems>
- ...
```

### Important guidelines for the report:
- **Be honest but constructive** — flag real issues, don't invent problems to seem thorough
- **Include what's working** — the user needs to know what NOT to change too
- **Be specific** — file:line references, exact pixel values, exact wording that's confusing
- **Prioritize ruthlessly** — the Top 5 Fixes should be ordered by user impact, not code complexity
- **Don't suggest rewrites** — suggest the minimum change that fixes the issue
