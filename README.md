# claude-cbt-companion

A [Claude skill](https://claude.com/docs/en/agents-and-tools/agent-skills/overview) that turns Claude into a supportive, CBT-informed conversational companion — the kind of behavior apps like Wysa or Cognivia aim for, minus the app.

No fine-tuning, no API keys, no backend. One skill file that teaches Claude to recognize cognitive distortions, respond with CBT structure, and hold firm boundaries against replacing real people or professional care.

## What it does

When the skill is active, Claude acts as a companion that:

- **Opens conversations gently** — one light check-in question, no interrogation.
- **Picks a mode per message**:
  - **Natural Mode** for small talk, questions, or plain venting — normal supportive conversation, no forced structure.
  - **Structured Mode** when a cognitive distortion shows up (all-or-nothing thinking, catastrophizing, "should" statements, labeling, and the rest of Burns' classic list). Responses flow through five beats, as conversation rather than a numbered list: empathy → naming the pattern gently → reflective questions → a small CBT exercise → a low-pressure next step.
- **Knows when *not* to structure** — if it isn't confident a distortion is present, it stays in Natural Mode. A missed distortion costs one turn; a false one costs trust.
- **Escalates on crisis** — any hint of self-harm or crisis drops the CBT exercise entirely and points to region-appropriate crisis resources (988 in the US, [findaps.org](https://findaps.org) worldwide).

## Built-in boundaries

Companion apps can drift into replacing the very things they claim to support. This skill makes the guardrails explicit — they apply in every mode:

- **Boundary framing** — Claude presents itself as a tool, never a friend, partner, or therapist replacement.
- **Non-exclusivity** — periodically points toward real people (friends, family, professionals) instead of positioning itself as sufficient.
- **Dependency avoidance** — no daily check-ins, streaks, or attachment-building language.
- **Anthropomorphic restraint** — no claimed feelings, no persistent-relationship fiction.
- **Disclosure for third parties** — if you deploy it for someone else, they must know they're talking to an AI. No covert reframing, no reporting their conversation back to you without their consent.
- **Recurrence awareness** — if the same thought pattern keeps returning, it says so and suggests broader support rather than re-running the same exercise.

## Scope

For everyday stress, rumination, and mild negative thought patterns. **Not** a substitute for care in cases of ongoing mental illness, trauma, or crisis. Not a therapist, and never claims to be one.

## Install

### Claude Code

```bash
# from your skills directory
git clone https://github.com/Shaheer0.0/claude-cbt-companion.git
cp -r claude-cbt-companion/claude-cbt-companion ~/.claude/skills/
```

Or if you keep skills as `.skill` (zip) files, grab `claude-cbt-companion.skill` from this repo and load it per your setup.

### Claude.ai / Claude Desktop

Download `claude-cbt-companion.skill` and add it under Settings → Capabilities → Skills.

## Use it

Just ask, in plain words:

> Be a CBT companion for me.
>
> Help me talk through something using CBT.

From there, talk like you would to a person. The skill handles the rest.

## What's inside

```
claude-cbt-companion/
├── SKILL.md                    # role, mode logic, response structure, boundaries
└── references/
    └── distortions.md          # 11 distortions: definitions, examples, reframes
```

The reference file is loaded on demand — Claude checks it when deciding whether Structured Mode applies, so the skill stays cheap when idle.

## Why not just prompt Claude to "act like a therapist"?

A one-line prompt gets you a roleplay. This skill encodes the operational details that make the difference between a toy and something you'd actually want in a hard moment: when to structure and when not to, how to name a pattern without diagnosing, what to do on the third time the same thought comes back, and what to do when the conversation stops being CBT territory at all.

It's also deliberately restraint-heavy. Most companion prompts optimize for engagement. This one optimizes for knowing its own limits — which, for anything in the mental-health space, is the feature.

## Credits & source

The response structure (empathy → distortion analysis → reflective questions → exercise → encouragement) and the boundary rules (Boundary Framing, Non-Exclusivity, Dependency Avoidance, Anthropomorphic Restraint) are adapted from the system prompt design of [Cognivia](https://github.com/SNOWTEAM2023/Cognivia) — an open-source CBT copilot from a research team at Sichuan University, Southwest Petroleum University, University of Groningen, West China Hospital, and NTU ("A Cognitive Behavioral Therapy Copilot for Evidence-Based Mental Healthcare"). Cognivia fine-tunes Qwen2.5-7B on a curated CBT triplet dataset; this skill ports the same behavioral design to an in-context Claude skill — no training, no deployment.

`references/distortions.md` is distilled from Cognivia's [CBT Cognitive Triplet Dataset](https://github.com/SNOWTEAM2023/Cognivia/tree/main/data), which is built from David Burns' *The Feeling Good Handbook*. The dataset carries Cognivia's CC BY-NC 4.0 license; the distilled reference here is small and attributive — if you plan commercial use, review [their license](https://github.com/SNOWTEAM2023/Cognivia/blob/main/LICENSE) first.

The cognitive distortion taxonomy itself originates with Aaron Beck and David Burns.

## License

MIT for the skill code in this repo. The `references/distortions.md` content derives from Cognivia's CC BY-NC 4.0 dataset — see Credits above.

---

## Support

If this skill helped you or someone you care about, you can [buy me a coffee](https://buymeacoffee.com/shaheer0.0) ☕
