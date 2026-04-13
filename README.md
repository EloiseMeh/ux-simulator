# UX Simulator for Claude Code

**User testing without users.** Simulate 5 virtual personas walking through your app and get a prioritized list of UX issues — in seconds, not weeks.

```
> /ux-sim

UX Simulation Report
====================
Project:         Treasure Chest Launcher
Target audience: Friends at a party, on their phones
Personas tested: 5

PERSONA 1: Mia — First time at game night, handed a phone with this open
  ✗ [P2] No text explaining what this app is before first tap (index.html:45)
  ✗ [P3] "Tap the box" assumes touch — desktop users see this too (index.html:67)
  Verdict: Completes flow, but hesitates for 5+ seconds at the chest

PRIORITY SUMMARY
================
P1 (Blocking):   2 issues
P2 (Confusing):  6 issues
P3 (Polish):     4 issues

TOP 5 FIXES (by impact):
1. Add a loading state for the chest animation — impatient users tap twice
2. ...
```

---

## Install

```bash
claude plugin add github:EloiseMeh/ux-simulator
```

## How to use

Run the command:

```
/ux-sim
```

The skill will:

1. **Read your project** — scans code, screens, components, and assets
2. **Ask about your users** — who they are, what device, what context
3. **Generate 5 personas** — tailored to your actual audience, not generic archetypes
4. **Simulate each persona** — walks through every screen step by step
5. **Report issues** — prioritized, with file:line references and suggested fixes

### Optional extra inputs

For a deeper analysis, you can also provide:

- **Live URL** — the skill fetches the real page to see what users see
- **Screenshots** — of key screens for visual analysis
- **Figma link** — compares intended design vs implementation
- **Flow description** — your intended user journey in plain language

More inputs = better simulation. But code-only works too.

---

## What it tests

Each persona stress-tests a different UX dimension:

| Dimension | What gets caught |
|-----------|-----------------|
| **Discovery** | Can a new user figure it out without help? |
| **Speed** | Does the app hold up when users rush or multitask? |
| **Comprehension** | Is everything clear to non-expert users? |
| **Accessibility** | Can someone with limitations use it? |
| **Repeat use** | Does the experience hold up on return visits? |

Personas adapt to your audience. A drinking game gets "drunk user with bad coordination" instead of "enterprise power user."

## Priority levels

| Level | Meaning |
|-------|---------|
| **P1 — Blocking** | User gets stuck or can't proceed |
| **P2 — Confusing** | User is unsure what to do or has a bad experience |
| **P3 — Polish** | Minor friction, could be smoother |

## Good to know

- This is **AI simulation**, not real user testing. It catches obvious issues — layout problems, missing feedback, confusing flows, accessibility gaps.
- It won't catch subjective preferences, emotional reactions, or cultural nuances the way real humans would.
- Think of it as a **first pass** before you invest in real user testing.

## Make it yours

Fork and edit `skills/ux-sim/SKILL.md` to:
- Add custom personas for your domain
- Change the report format
- Add project-specific checks

---

## License

MIT
