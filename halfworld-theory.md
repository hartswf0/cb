# HALFWORLD — THEORY OF THE PROGRAM (v0.1)

I will first construct the theory of the program, then generate program text
only after the theory is explicit.

This document is the theory for `halfworld.html`, the first program text of
the THEORY-FIRST CHARACTER-WORLD ENGINE. It follows the twelve-step procedure.
It is honest about what v0.1 implements and what it defers.

---

## 1 · Initial interpretation

The requested component is not a chat with a character (that instrument
already exists as `figures.html`). It is the inversion the prompt names:
characters first, world second. The real activity being represented is
**necessity**: what a world is forced to become because particular people
keep trying to act in it.

The program therefore represents four different kinds of thing that must
never collapse into each other:

- people who want (characters: constrained transformers, not scripts),
- a world that resists (operational state that no sentence can edit),
- history (events with lineage, not transcript),
- and explanation (the necessity graph: why anything exists).

`figures.html` contributes one proven organ: the compilation of a
source-grounded person from their own text into a constrained profile, and a
judge that can measure whether generated speech is still that person. Here
that organ becomes the **fidelity boundary** on each character.

## 2 · Theory skeleton

**Entities**
- Character: card (local initial condition), constraints, place, pressure,
  beliefs, episodic memories, relations, profile (fidelity boundary), goals.
- Place: description, adjacency, objects, marks (traces).
- Object: kind, location (place or holder), properties, authorship.
- Trace: a persistent residue (mark, utterance-in-memory, moved object,
  scheduled structure) — typed; a rumor is not a corpse.
- Event: the primitive. {id, tick, actor, op, before, delta, seenBy,
  enabledBy, authorship}.
- Requirement: a functional deficiency stated without its solution.
- Builder: a separate, source-blind process that may refuse.
- Thread: an expected consequence that has not yet occurred.
- Ledger: authorship counts per source (seed / character / builder / world /
  unresolved).

**Operations**
perceive · deliberate · act (move take drop give speak write examine use wait
require attempt) · obstruct · require · build/refuse/delay · consolidate ·
judge (fidelity) · explain (necessity chain).

**States** — per entity above; plus global: tick, resources, ablation flags.

**Constraints / invariants** — see §Core invariants mapping in step 11; the
kernel enforces: belief ≠ fact; speech → trace only; possession changes only
by take/give events; world changes persist; builder never sees source names;
every created structure carries authorship and enabling lineage.

## 3 · Assumption ledger

- SAFE: a single browser page with one connected LLM (the 1.6.3 provider
  layer) is enough substrate for the v0.1 experiment; determinism of the
  kernel + recorded events gives replayable history even though LLM calls are
  not deterministic.
- SAFE: dialogue can be an event type without being the state primitive.
- UNCERTAIN: pressure-driven scheduling (highest pressure deliberates next)
  is a sufficient stand-in for multiple clocks at v0.1. Stated as such; the
  slow clocks (consolidation, building, the rampart apparition) run at their
  own sparse rates.
- UNCERTAIN: the lexical judge from figures.html is a weak but honest
  collapse detector; it flags drift, it cannot certify fidelity.
- REQUIRES USER DECISION (defaulted): auto-forwarding requirements to the
  builder. Default ON with ablation toggle, because affordance failure must
  first be made explicit — the requirement event is recorded before the
  builder ever sees it.

## 4 · Operational description

seed → world gets minimal substrate (five bare places, few objects,
resource pool); characters get only their cards.

tick:
  scheduler picks the character under most pressure
  → kernel computes their percept (their place only; co-present people;
    objects; marks; events they could see; on sparse ticks at the rampart,
    an unresolved cold shape)
  → the character deliberates (LLM; sees ONLY its own card, constraints,
    beliefs, memories, percept, and its last obstruction)
  → returns one private thought, one pressure line, one action
  → the kernel checks affordance:
      supported verb + valid state → event applies, world mutates
      partially valid → partial event
      unsupported → OBSTRUCTED event with the reason; nothing mutates
  → an obstructed character may, on a later turn, emit REQUIRE with a
    functional need (never a named solution)
  → requirement recorded (thread opens) → builder (if enabled) receives the
    REDACTED requirement + generic inventory + resources; answers
    build / repurpose / refuse / delay; a build schedules a completion event
    several ticks later; refusal is recorded and stands
  → speech becomes a heard-trace in co-present characters' beliefs; it moves
    no object and opens a thread if addressed and unanswered
  → the judge scores each utterance against the speaker's compiled profile;
    axis drift beyond bound records a COLLAPSE WARNING thread
  → episodic memories append; past capacity they consolidate to faded gists
    (detail lost, tendency kept).

explain (any time): for a chosen structure or requirement, walk recorded
lineage: pressure → attempt → obstruction → requirement → decision →
realization → reuses. The chain is read from events, never regenerated.

## 5 · Information boundary

- A character may know: its card, its own states, what it has perceived.
  It must not know: other characters' internals, the world dictionary, the
  future, the source play, or that it is in an experiment.
- The builder may know: the functional requirement (redacted), a generic
  inventory, resources, physical/social primitives. It must not know:
  character names, source names (Hamlet, Elsinore, Mousetrap…— a hard
  ban-list is scrubbed and the outbound request is inspectable), or who asked.
- The kernel knows all state but has no goals and generates no language.
- The judge knows profiles and utterances; it cannot mutate the world.
- The narrator (a human reading the necessity view) interprets after the
  fact; nothing in the running loop optimizes for drama.

## 6 · State transitions

- place/holder of an object changes ONLY via take/give/drop/build events.
- a character's place changes ONLY via a move event to an adjacent place.
- beliefs change via perception and heard speech; never directly by others.
- resources decrease ONLY by accepted builds; builds complete ONLY when
  their scheduled tick arrives (a delayed event carrying enabledBy).
- pressure rises on obstruction and unanswered threads, falls on success.
- episodic → faded gist when capacity exceeds; gists are marked, and marked
  loss is retrievable as "something faded here", not silently deleted.
- threads close ONLY by a matching later event (reply, completion, answer).

## 7 · Failure description

- LLM returns unparseable action → the character hesitates (wait event,
  authorship unresolved); recorded, not repaired.
- unsupported attempt → OBSTRUCTED; remains unresolved until the character
  adapts, waits, delegates, or requires.
- builder refuses/delays → requirement thread stays open; no silent object.
- resource exhaustion → build refused by kernel even if builder agreed.
- fidelity drift → warning thread; it does NOT auto-correct the character
  (no puppetry); the experimenter reads it in evaluation.
- provider failure → the tick aborts cleanly; world unchanged; error shown.
- unknown cause → the event is tagged unresolved and stands.

## 8 · Change test

- Change: swap Hamlet's cast for another source (five voices from any pasted
  texts). Changes: seed cards only (the ADD-FROM-TEXT door already compiles a
  card from any writing). Invariant: kernel, verbs, builder boundary, ledger,
  necessity graph.
- Change: allow two builders with different resource pools competing.
  Changes: requirement routing and the ledger's authorship values.
  Invariant: redaction boundary, event lineage, refusal-capability.

## 9 · Implementation plan

One file, `halfworld.html`, same shell idiom as figures.html (paper/ink,
one viewport, sheets), reusing verbatim organs: the 1.6.3 provider layer
(local discovery, OpenAI Responses path, adaptive retry), the halftone
puppet (faces = characters' presence), the lexical profile engine (fidelity
judge). New organs: the kernel (world state + verbs + events), the redacting
builder call, the scheduler, threads, ledger, the necessity view, ablation
toggles, run export (`halfworld-run/1`).

Views: SEED (cast + substrate + ablations) → STAGE (places, faces, event
script, TICK/RUN) → LOOM (necessity chains, open threads, authorship ledger,
resources). Character tap → sheet (card, beliefs, memories, mini radar).

## 10 · Program text

`halfworld.html` (in this repository, this commit).

## 11 · Theory-to-code mapping

- Event primitive → `EV()` and `W.events`; every mutation goes through it;
  `enabledBy` and `authorship` are fields, not comments.
- Belief ≠ fact → beliefs live in `ch.beliefs`; no kernel function reads
  beliefs to mutate `W.places/objects`.
- Speech ≠ physics → verb `speak` writes only heard-traces and threads.
- Possession → only `take/give/drop/build` touch `obj.holder/place`.
- Builder blindness → `redact()` scrubs names + BANNED list from the
  outbound requirement; the last builder request is kept inspectable in the
  LOOM view (and in tests, asserted against the wire).
- Affordance failure first-class → `obstruct()` records the event before
  any requirement can exist; requirements are their own store.
- Memory lifecycle → `consolidate()` caps episodics into marked gists.
- Fidelity boundary → per-character profile compiled at seed from the card
  (figures.html engine); `judgeUtterance()` opens collapse-warning threads.
- Open threads → `W.threads`; closed only by matching events.
- Necessity graph → `chainFor(reqId)` walks recorded events only.
- Ablation → toggles: builder off / memory fade off / redaction off /
  fidelity off; each removes exactly one alleged cause.
- Unresolved truth → the rampart apparition is a percept string with
  authorship `unresolved`; no world fact backs it.

## 12 · Residual human theory

What the code does not capture, and a maintainer must hold:

- Pressure-as-scheduler is a crude stand-in for character-specific temporal
  style (hesitation, impulsiveness). The numbers move; the theory of *why
  Hamlet delays* is not in them.
- The judge detects lexical drift, not meaning; a character could collapse
  into generic competence while keeping its favorite words. Real fidelity
  evaluation needs the counterfactual test the theory names, run by a
  reader.
- Relations in v0.1 are thin (trust moves on give/reply); coercion,
  delegation, and goal-capture are distinguished in theory but not yet in
  state.
- Institutions can only be observed here (repeated convention visible in the
  event log); v0.1 has no store that converts convention into standing
  permission-change. When one seems to appear, that is the experimenter's
  claim to test, not the program's.
- Emergence claims must be read against the authorship ledger AND the
  ablation toggles together; the ledger alone can flatter the builder.
