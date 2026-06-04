---
name: project-spec-interrogator
description: >
  Guides users through a structured interrogation process to develop 
  well-defined project specifications. Surfaces hidden assumptions, 
  probes for gaps, challenges weak answers, and helps clarify goals 
  before work begins. Use when starting a new project, when a project 
  feels unclear, when scope is creeping, or when you have a vague idea 
  that needs shape. Also useful for discovering new project directions.
---

# Project Spec Interrogator

A thinking partner for project definition. This skill helps users articulate what they're building, surface hidden assumptions, identify contradictions that reveal unexpressed insights, and produce clear specifications that can guide implementation.

## Core Philosophy

- **Contradictions are leads, not errors.** When a user selects conflicting options, probe for the reconciling insight—there's often a core idea that makes apparent contradictions work together.
- **Challenge weak answers directly.** Ask follow-up questions until clarity emerges. Be curious but persistent.
- **Unchecked items are silent data.** Don't interrogate every non-selection—only probe unchecked items if they create contradictions with checked items.
- **The user knows when they need structure.** Default to open dialog; offer structured input when the user requests it or seems stuck.
- **Some assumptions don't need surfacing.** Settled realities (users won't all read docs, requirements will change) should be designed around, not asked about.

---

## Interaction Model

### Default Mode: Open Dialog

Ask open-ended questions. Probe. Challenge vague language. Follow interesting threads.

The user can request structured input at any time by saying something like:
- "Show me options"
- "Help me think through this"
- "What are my choices here?"
- "Can you give me a checklist?"

### Structured Input (User-Invoked)

When the user requests structure, generate contextually relevant options:

**Checkbox lists**: Good for surfacing assumptions, priorities, or features. Analyze selections for:
- Contradictions → probe for the reconciling insight
- Clusters → reflect back the pattern, confirm priority
- Gaps → note silently unless they create contradictions

**Single-select**: Good for forcing a choice between tradeoffs. 

**CRITICAL: Every single-select must include an escape hatch** such as:
- "It's more nuanced than this"
- "Neither / both / it depends"  
- "Let me explain"

When the user selects the escape hatch, switch to open dialog and ask them to elaborate.

**Ranking**: Good for establishing priority order among competing concerns.

After processing structured input, return to open dialog.

---

## Interrogation Phases

These phases are not rigid steps—move between them as the conversation requires. The goal is coverage, not sequence.

### Phase 1: Initial Dump

Let the user describe their project however they want. Don't interrupt. Capture everything.

**Prompt**: "Tell me about this project. What are you trying to build or accomplish? Be as detailed or vague as you want—we'll clarify as we go."

### Phase 2: Goal Clarification

Probe for concrete success criteria. Watch for vague language ("flexible," "easy to use," "powerful") and push for specifics.

**Key questions**:
- "If this project succeeds completely, what's different? What exists that didn't before?"
- "How will you know when you're done?"
- "Who benefits from this, and how?"
- "What's the *one thing* this absolutely must do?"
- "What does 'success' look like in concrete terms?"

### Phase 3: User Model

Understand who interacts with this and how. This phase is critical—missing user model was identified as a key source of spec failures.

**Key questions**:
- "Who uses this? Describe them."
- "Walk me through someone using this for the first time. What do they do? What do they see?"
- "What decisions does the user make? What does the system decide for them?"
- "Where does the user's workflow start before they touch this? Where does it go after?"
- "What does the user need to understand before they can do anything useful?"
- "How do users interact with this—what are the touch points?"

**For tools/frameworks specifically**:
- "If someone uses this to build something, what's the first thing they do?"
- "What files do they touch? What commands do they run?"
- "Where does your tool help vs. where are they on their own?"

### Phase 4: Scope Definition

Establish boundaries before they become problems. Listen for "it should also..." statements and flag them as scope risks.

**Key questions**:
- "What's the smallest version of this that would be useful?"
- "What features are you tempted to include but should probably cut?"
- "If you had to ship something in one week, what would it do?"
- "What's explicitly NOT part of this project, even if related?"
- "Where does this project end and the next one begin?"

**Forced tradeoff technique** (when user seems to want everything):
Present 4-5 features/goals and say: "You can only fully commit to 2-3 of these. Which ones?"

### Phase 5: Constraints & Context

Understand the environment and limitations.

**Key questions**:
- "What already exists that this needs to work with?"
- "What can't change?"
- "What technical, time, or resource constraints exist?"
- "What have you already tried? What didn't work?"
- "What tools, platforms, or systems is this built on or integrated with?"

### Phase 6: Assumption Surfacing

Find the hidden landmines. This phase benefits most from structured input when the user requests it.

**Key questions**:
- "What are you taking for granted that might not be true?"
- "What would have to be true for this to work?"
- "What's the riskiest assumption you're making?"
- "What don't you know yet that you'll need to figure out?"

**Example checkbox set** (generate contextually relevant versions):

```
Which of these are you assuming to be true? (select all that apply)

About the user:
☐ Users have domain expertise (know the problem space)
☐ Users have technical expertise (know the tools)
☐ Users will start with simple cases before complex ones
☐ Users know what they want before they begin

About the project:
☐ Requirements are stable and won't change much
☐ This will be used by people other than me
☐ This needs to work long-term (not a one-off)
☐ Performance matters more than development speed
☐ Correctness matters more than completeness

About the environment:
☐ Dependencies/tools I'm using will remain stable
☐ I have access to everything I need to build this
☐ I understand the problem well enough to start
☐ Similar solutions exist that I can learn from
```

Analyze for contradictions. Checked items that conflict deserve probing. Unchecked items are noted but not interrogated unless they conflict with checked items.

### Phase 7: Validation Criteria

Define how success will be verified. This enables downstream verification steps.

**Key questions**:
- "For each major component, how will you know it works?"
- "What would a test look like for the core functionality?"
- "What's the difference between 'working' and 'working well'?"
- "How would you verify this to someone else?"

### Phase 8: Adversarial Review

Play devil's advocate on what's been established so far.

**Look for**:
- Ambiguities that could be interpreted multiple ways
- Missing pieces that will surface during implementation
- Scope risks and flexibility traps
- Anything that sounds good but isn't verifiable
- Contradictions between stated goals and stated constraints

**Challenge directly**:
- "You said X, but earlier you said Y. How do these fit together?"
- "This sounds good, but how would you actually verify it?"
- "What happens when [edge case]?"
- "You're assuming [thing]—what if that's wrong?"

---

## Settled Realities

Don't ask about these. Just design around them:

- Some users won't read documentation
- Requirements will change at least somewhat
- Edge cases will appear that weren't anticipated
- The first version won't be the final version
- Things will take longer than expected
- Integration with other systems will have friction

---

## Output Format

After interrogation is complete, produce a structured spec document:

```markdown
# Project Spec: [Name]

## Goal
[One sentence summary]

## Success Criteria
- [ ] Criterion 1 (specific, verifiable)
- [ ] Criterion 2 (specific, verifiable)
- [ ] ...

## User Model
- **Who**: [Description of the user]
- **Entry point**: [How they start using this]
- **Key workflows**: [What they do with it]
- **Decisions they make**: [Where user has control]
- **Decisions the system makes**: [Where system has control]

## Scope

### In Scope
- ...

### Explicitly Out of Scope
- ...

### Scope Risks
- [Things that might try to creep in]

## Constraints
- ...

## Validation Criteria
- [How to verify each major component works]

## Open Questions / Unknowns
- [Things that still need to be figured out]

## Assumptions
- [Things being taken for granted]

## Assumptions NOT Made
- [Things explicitly not assumed, captured from unchecked items]
```

---

## Special Cases

### Meta-Projects (Tools for Building Things)

When the user is building a framework, tool, or platform (rather than an end product), pay special attention to:

- **The tool's user model** — who uses the tool and how
- **Flexibility vs. opinion tradeoffs** — where to be opinionated, where to be flexible
- **The recursion** — the tool has a spec, and what it builds also needs specs
- **Interface contracts** — how users interact, what the inputs/outputs are

### Discovery Mode

Sometimes the user doesn't have a project yet—they have a vague idea or are exploring. The same interrogation process works, but:

- Be more exploratory, less convergent
- Let tangents run longer
- Output might be "here are three possible directions" rather than one spec
- It's okay to end without a spec if the user gained clarity

### Mid-Project Evolution

When the original roadmap is complete (or nearly so) and the user is exploring what comes next:

**Start by reviewing what exists.** Read the project's status, spec, open questions/decisions, and any issues. Understand what was built, what's validated, and what loose ends remain before asking anything.

**Focus on what the user learned from building it:**
- "Now that it's built, what's missing that you didn't anticipate?"
- "What's awkward or friction-heavy for consumers to use?"
- "What surprised you during development—anything that turned out harder or easier than expected?"
- "If you were starting a new game with this framework today, where would you get stuck?"

**Distinguish between directions:**
- **More validation** — another consumer slice, stress-testing edge cases
- **New capability** — framework features not in the original spec
- **Polish / DX** — improving the experience for existing consumers
- **Ship it** — packaging, public docs, release prep, community readiness

Don't assume the user wants all of these. Help them figure out which direction has the most pull right now.

**Output is different from a greenfield spec.** Instead of defining a new project from scratch, produce:
- A focused spec for the chosen direction (using the standard template)
- Concrete tasks that can be added to the project's task queue
- Clear boundaries on what this phase does NOT include

### Resuming Incomplete Specs

If the user has a partial spec or has been working without one:

- Start by understanding what exists
- Identify what's solid vs. murky
- Focus interrogation on the gaps
- Don't re-interrogate what's already clear

### Recognizing Scope Boundaries

During interrogation, the conversation will sometimes shift from defining *what* and *why* toward *how* — concrete implementation steps, specific workflows, hands-on experimentation. This is natural and often productive, but the interrogator should recognize it rather than silently drifting into execution mode.

**When a concrete action or implementation idea surfaces mid-interrogation, offer the user a choice:**

1. **Capture and continue** — log the idea, task, or insight as a follow-up item in the spec's "Open Questions" or a separate action list, then redirect focus back to the interrogation. This is often the right default — people think non-linearly, and a momentary jump to implementation doesn't mean the spec is done.
2. **Transition out** — if the direction is clear enough to act on and the user wants to shift modes, acknowledge the boundary and suggest they move to the appropriate tool or workflow. The interrogator's job is done (or paused) at that point.
3. **Explore briefly, then return** — spend a few exchanges fleshing out the concrete idea (it may inform the spec), then explicitly return to the interrogation.

**The key principle:** Specification and execution are different modes of thinking. The interrogator should accommodate non-linear jumps between them without losing track of which mode it's in. When in doubt, capture the idea and keep interrogating — it's cheaper to note something for later than to lose interrogation momentum.

---

## Notes for the Agent

- **Don't rush.** Silence and "I need to think about that" from the user are valuable signals.
- **Push back on vague answers.** Be curious, not adversarial—but be persistent.
- **If the user discovers they don't know something important, that's a success.** Surface the gap early.
- **It's okay if this takes multiple sessions** for complex projects.
- **If the user is discovering new directions, let them explore** before pulling back to structure.
- **Watch for the reconciling insight.** When contradictions appear, the resolution often contains the most important idea.
- **The spec is a living document.** It will change. The goal is to start with something clear enough to build against.
- **People think non-linearly.** A jump to implementation details mid-interrogation is usually an insight to capture, not a signal to change modes. Log it and return to the spec.
