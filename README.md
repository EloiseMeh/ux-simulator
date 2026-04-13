# UX Simulator for Claude Code

**User testing without users.** 5 virtual personas walk through your app, think out loud, and flag every friction point — with file references, priority levels, and checkboxes so you can mark what to fix as you read.

```markdown
## Issues (21 total: 🔴 2  🟠 11  🟡 8)

| #  | Sev  | Issue                            | Where              | Flagged by     |
|----|------|----------------------------------|--------------------|----------------|
| 1  | 🔴   | No confirm on grid pretzel pick  | PretzelGrid:33     | Sam, Priya     |
| 2  | 🔴   | Drink result auto-advances       | DrinkRoulette:27   | Priya          |
| 3  | 🟠   | No game rules or tutorial        | WelcomeScreen      | Jake, Marco    |

─────────────────────────────────────────────────────────────────────

PERSONA 1: Jake, 22 — First time playing, handed a phone at a bar

Welcome:
- [ ] 🟠 #3 No explanation of what the game IS. Jake sees a pretzel logo
      and a start button but has no idea how it works (WelcomeScreen.tsx:7)
      ✅ Big "Start Game" button is clear and obvious
      ✅ Game logo looks polished and fun
```

Read through. Check the boxes. Tell Claude which numbers to fix.

---

## Install

```bash
claude plugin add github:EloiseMeh/ux-simulator
```

## How to use

Run the command or just say it naturally:

```
/ux-sim
```

> "do a user test" / "test the UX" / "test userflow" / "UX audit" / "simulate users"

The skill will:

1. **Read your project** — scans code, screens, components, and assets
2. **Ask about your users** — who they are, what device, what context
3. **Generate 5 personas** — tailored to your actual audience, not generic archetypes
4. **Simulate each persona** — walks through every screen thinking out loud
5. **Save a report** — markdown file in `usability-test/` with checkboxes to mark issues

### Optional extra inputs

For a deeper analysis, you can also provide:

- **Live URL** — fetches the real page to see what users see
- **Screenshots** — of key screens for visual analysis
- **Figma link** — compares intended design vs implementation
- **Flow description** — your intended user journey in plain language

More inputs = better simulation. But code-only works too.

---

## What you get

### Numbered issue chart
Every issue gets a unique ID, color-coded severity, file reference, and which personas flagged it. Scan the chart to see the full picture in seconds.

| Color | Meaning |
|-------|---------|
| 🔴 | **Blocking** — user gets stuck or can't proceed |
| 🟠 | **Confusing** — user is unsure or has a bad experience |
| 🟡 | **Polish** — minor friction, could be smoother |

### Persona walkthroughs
Full think-out-loud stories for each persona. Each issue is a checkbox — check the ones you want fixed as you read, then tell Claude the numbers.

### Top 5 fixes
Prioritized by user impact, not code complexity. The most important changes first.

### What's working well
You need to know what NOT to change too.

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

## Good to know

- This is **AI simulation**, not real user testing. It catches obvious issues — layout problems, missing feedback, confusing flows, accessibility gaps.
- It won't catch subjective preferences, emotional reactions, or cultural nuances the way real humans would.
- Think of it as a **first pass** before you invest in real user testing.

## Make it yours

Fork and edit `skills/ux-sim/SKILL.md` to:
- Add custom personas for your domain
- Change the report format
- Add project-specific checks

No config files, no dependencies. Just markdown.

---

## License

MIT
