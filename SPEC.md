# A Registry of Proto-Concepts with Referent Quarantine

**Specification, v0.1**

Author: Igor Kapustin.
Drafting and editing assistance: Claude (Anthropic), models Claude Fable 5 and Claude Opus 5. The author is responsible for all claims, framing decisions, and errors.
License: CC BY 4.0

---

> *…what rough beast, its hour come round at last, / Slouches towards Bethlehem to be born?*
> — W. B. Yeats, "The Second Coming"

## Prologue

Picture it: a man stands waist-deep in the sea, his children splashing nearby. Far out, something glints on the pearly ripples: sun playing on a wave, or the flash of eyeglasses. If glasses — there is a person out there. If the glint appears and vanishes — the glasses keep going under. If they go under — the person is drowning. If drowning — call for help, now. The chain is built in an instant. He looks at his wife and children, blindingly happy in the water — shifts his troubled gaze back to the ripples — and in seconds takes the chain apart: "no, a trick of the light, of course not glasses — just the pearly ripples." Because "just a trick of the light" — the event interpreted by the word *ripples* — demands nothing. And the word *glasses* demands everything: drop it all, swim, shout, raise the alarm; the fuss, the time, and perhaps the laughter of the whole beach, of the lifeguards and, above all, of his wife and children: dad's had too much sun. But days later a notice about a missing swimmer goes up on the beach, and then a body washes ashore.

That watcher had everything: ready words — *drowning*, *lifeguard* — a laid-down procedure, and a jolt of alarm in his chest, straight to the heart. And he lost only in the interpretation — in the answer he gave to the sea's challenge, in the action he chose: he assigned the event a different name, picked a word — *ripples*. That was all. And yet that failure has a name. There is a price of acting.

Today we are armed. Or rather — our thinking itself is armed. We, people, now carry an instantly thinking Artificial Intelligence — one that sometimes thinks better than we do, modest thinkers that we are. It simply arrived in our lives. Arrived — for us.

And so at the border of the known and the unknown a different sentry takes up the post — a machine that reads the world first. It has no words for the unprecedented, nothing jolts it, and for every glint it holds a ready, fluent explanation of why this is a play of light. Whether the next glint becomes a discovery or "ripples" is a question on which someone's life — possibly many lives — depends. And this must be understood: the one deciding is no longer "our dad." That failure does not have a name yet. This document is an attempt to design for it not a name, but a procedure.

The epigraph above is a prayer — the reigning genre of technological dread: the unknown as a beast that *approaches*, still distant, still slouching toward us, still negotiable. But the unknown has no distance to close. Terra incognita is not beyond the clouds: it is already here, now. You are standing on it, you are breathing its air; look around — it is all around you. You stare at it and do not see it, because "face to face, no face can be seen." The undescribed flickers in the ripples of the present, a penny a glint, and the beast becomes rough at exactly the moment the penny is begrudged. The body on the shore is not the cruelty of the future arriving. It is the invoice for "just a trick of the light," delivered with a delay. Or perhaps such invoices are already arriving — we do not know: to us, everything out there on the water is still "ripples." And so this document's reply to the prayer is this: the future's mercy is not begged for — it is built. Not asking the beautiful far-off to be merciful, but doing now what will make it so. In what follows, we propose the procedure for exactly that.

## Abstract

Large language models increasingly encounter phenomena for which no name exists in their training data. By construction, they must describe the never-named in terms of the already-named, and they do so fluently — producing plausible descriptions that are indistinguishable, at the surface, from grounded knowledge. This creates a detection limit: genuinely novel phenomena are silently re-labeled as familiar ones at the point of first contact, and the mislabeling leaves no trace in the output. In its worst form the model reports a finding's absence — a *negative confabulation*, which leaves no artifact to check at all. Several research threads now touch this problem separately — neologism learning, automated labeling of sparse-autoencoder features, out-of-distribution detection — but no mechanism connects them, and none includes governance. This document proposes one: a shared, open registry of *proto-concepts* (machine-registered anomaly coordinates with provenance) coupled with a *referent quarantine* — a status system under which a registered entry may not be promoted to a working term until a reproducible behavioral test is attached to it. Registration is cheap and fast; legalization is deliberately slow. The design borrows its governance skeleton from institutions that already solved analogous problems: the IETF RFC track, IUPAC chemical nomenclature, and the ICD revision process.

## 1. Problem

### 1.1 The re-labeling failure mode

An LLM's vocabulary is assembled entirely from the past: from text about things that have already happened, been noticed, and been named. Yet these systems are increasingly deployed at the frontier of the not-yet-named — as research assistants, monitoring systems, first readers of new data. When such a system encounters a phenomenon for which its vocabulary has no entry, it cannot report "no entry." It produces the nearest available description, assembled from existing terms, with the same fluency and confidence as a grounded answer.

Call this the **re-labeling failure mode**: the novel is renamed as the familiar at the moment of first contact. Three properties make it dangerous:

1. **It is silent.** Unlike a hallucinated citation, a re-labeled phenomenon produces no checkable artifact. The output is not false about anything named; it is smooth about something unnamed.
2. **It is self-concealing.** The very fluency of the description suppresses the human signal that historically triggered concept formation — the felt sense that "something here does not fit." A ready-made label is the cheapest way to stop looking.
3. **It scales with deployment.** The more of the observation frontier is delegated to models, the larger the fraction of first contacts with the new and not-yet-described that pass through a vocabulary of the past — registered by no one and nothing. The faint outline of a discovery that has no descriptive-linguistic base yet slips past the machine — and, as history shows, past the human.

Empirically, the fragility is measurable even for *human* neologisms: adding a single recent coinage to a text degrades machine translation quality by an average of 43% in human evaluation (NEO-BENCH, Zheng et al. 2024). If models struggle with new words that already exist, their behavior on phenomena with no words at all is strictly worse — and unmeasured, because a benchmark for the never-named cannot be built from the already-named. This is not an oversight but a structural blind spot: the entire evaluation industry tests errors *inside* the vocabulary and is constitutionally unable to test the vocabulary's boundary.

### 1.2 The negative case

The literature on confabulation in language models — the term has been argued for since 2023, and detection methods such as semantic entropy now target it — treats it as a *positive* defect: the model asserts something that does not exist. A fabricated citation, an invented study, a wrong figure. Costly, but recoverable: the claim leaves a trace, and anyone can check whether the paper exists.

The failure mode this document is about is the negative one. Asked to examine a sample, a corpus, a dataset for something not yet named, a model that has no word for what is there does not invent an extra finding. It reports the absence of one: *no anomalies detected*, *nothing significant in this sample*, *no known correspondence*. Inside the system, "I have no name for this" and "there is nothing here" are not distinguishable states — so the boundary of the vocabulary is returned to the user as a boundary of reality. That is what it writes today. What this document demands is the opposite report at the boundary: "an anomaly IS detected; there IS something significant in this sample — and I have no words to describe it."

Negative confabulation has three properties that make it worse than the positive kind. It leaves no artifact — there is no false claim to check, only a clean report. It cannot be falsified without independently discovering the thing that nobody has named yet, which is the very task that was delegated. And it is silently agreeable: a null result is what most investigations expect most of the time, so nothing about it invites a second look. A fabricated citation costs a researcher an afternoon. A fabricated absence costs a discovery — and leaves no way to learn that it did. Perhaps it costs lives — not later, in some beautiful far-off, but already now. And we do not know.

### 1.3 Why "add more training data" does not fix it

The limit is not a knowledge gap but a channel property. No processing of a corpus can recover a distinction absent from the corpus (data-processing inequality); a regulator cannot exceed the variety of its inputs (Ashby). Scaling parameters or data moves the boundary of the described; it does not instrument the boundary. What is missing is not capacity but an *organ*: a mechanism by which "unlike anything I have" can be (a) expressed without premature naming, (b) recorded with provenance, (c) routed to whoever can attach a real-world referent, and (d) only then admitted into the working vocabulary.

### 1.4 Contributions and what they rest on

Stated plainly, so the claims can be checked against the prior art in §2 rather than inferred from it.

**C1. Negative confabulation (§1.2).** The failure mode in which a model, lacking a name for what is present, reports its absence rather than inventing a presence. *Rests on:* the confabulation literature (Millidge 2023; Smith et al. 2023) and consistency-based detection (Farquhar et al. 2024), all of which score false *assertions*. *New here:* the false *absence* — an output that generates no claim to score, cannot be falsified without independently performing the delegated task, and passes as an unremarkable null result.

**C2. Confabulation of concepts rather than facts (§1.1).** *Rests on:* the same literature, which treats confabulation as a miss against a fact that exists somewhere, and on the hermeneutical-lacuna tradition (Fricker 2007), which treats missing concepts as a social injustice rather than a machine failure mode. *New here:* the case where no correct answer exists for anyone yet — the model's smoothing over an absent distinction, and the observation that a boundary of vocabulary is returned as a boundary of reality.

**C3. Referent quarantine as governance (§3.2–3.3).** A status track in which registration is free and promotion to a working term requires an attached, independently reproduced referent test, with a human role at the gate. *Rests on:* neologism learning and plug-in evaluation (Hewitt et al. 2025), automated feature labeling validated as classifiers (EleutherAI 2024), out-of-distribution detection, and three governance precedents transposed wholesale — the IETF standards track and its two-independent-implementations rule (RFC 2026), IUPAC's practice of writing naming rules before discovery, and the ICD revision process. *New here:* none of the components, only their connection — provenance obligations, the candidate/adopted threshold, cross-model identity for a registered distinction, and the nomenclator as a designed, two-part office: an embedded registrar that whispers proto-names in a prepared grammar, and a human name-giver who converts them into testable distinctions. The emergent-communication failure (§2) is the argument for why the gate, not the generator, is the missing part.

Two secondary claims. The `registered` tier doubles as the first constructible benchmark for the vocabulary boundary itself, which cannot be built from named phenomena (§3.5). And the five-minute demonstration (§4) is offered as a reproducible referent-test template, not merely an illustration.

What this document does not claim: no implementation, no measurements, no independent reproduction of anything proposed here. Its own status under its own scheme is `registered`.

## 2. Prior art (what exists, what is missing)

Three active research threads each hold one piece.

**Neologism learning (DeepMind).** Hewitt et al. (arXiv:2510.08506; see also "We Can't Understand AI Using our Existing Vocabulary," arXiv:2502.07586) introduce new words into an LLM as trained embeddings, without touching other parameters. The model can then *self-verbalize* what the new word means to it, and the verbalization is validated behaviorally ("plug-in evaluation"). This is the embryo of a proto-concept and of a quarantine test. What it lacks: a registry, provenance, cross-lab portability — and its neologisms so far encode *known* concepts (flattery, response length). The machine does not yet name the unprecedented.

**Automated feature labeling (SAE interpretability).** Sparse autoencoders decompose model activations into millions of features; human labeling does not scale, so pipelines (e.g., EleutherAI's sae-auto-interp) generate textual explanations automatically and score each explanation as a classifier — does it predict where the feature fires? This is an industrial-scale pipeline of *nameless semantic coordinates receiving machine-generated names validated by behavior*. Known limitation, openly reported: SAEs do not guarantee discovery of desired concepts, and many features remain poorly interpretable. Less discussed: an auto-name assigned by one machine to another machine's feature can be a smooth label on a void — precisely the re-labeling failure mode, now applied to the model's own internals. Feature inventories are also lab-local: a feature identified in model A has no registered identity usable for model B.

**Public catalogs of machine-named features (Neuronpedia).** The closest existing object to the registry proposed here. Neuronpedia (neuronpedia.org, open-sourced 2025) hosts terabytes of activations, features, and machine-generated explanations across models, with community voting and an API; auto-interpreted feature labels sit alongside human comments at industrial scale. It is, in this document's terms, a working registrar without a gate: an explanation's standing comes from votes ("sounds right"), not from an attached, independently reproduced referent test; auto-generated labels and verified ones share equal status; there is no provenance of boundary encounters (features are cataloged from the model, not from moments where the model met the undescribed); and a confabulated label on a void is undetectable within the platform's own machinery. The registry proposed here is not an alternative to such catalogs but the missing floor above them — statuses, provenance, and a promotion threshold that their explanation layer could adopt directly.

**Out-of-distribution / anomaly detection.** A mature literature allows a system to signal "this input is unlike my training distribution." In deployed products this channel is systematically suppressed: a fluent answer ships; "unlike anything I have" does not. The alarm organ exists and is disabled for economic reasons, not scientific ones.

**Confabulation and its detection.** A body of work argues that *confabulation* is the correct term for fluent ungrounded output (Millidge 2023; Smith et al. 2023, PLOS Digital Health), and consistency-based methods — semantic entropy (Farquhar et al. 2024), SelfCheckGPT and successors — detect it by measuring divergence across stochastic samples of the same query. This is the closest existing machinery to the referent test proposed below, and §3 builds on it rather than around it. What it does not cover is §1.2: every one of these methods scores a claim against a fact that exists somewhere. None addresses the case where the correct answer exists nowhere yet, and none detects a confabulated *absence*, which produces no claim to score.

**A cautionary ancestor.** Emergent-communication research (late 2010s) let agents evolve their own codes in cooperative games. The direction stalled: the evolved tokens were unreadable and ungrounded — names without referents, produced at machine speed. It died, in effect, from the absence of a referent quarantine. The failure is instructive: machine word-formation without a grounding gate produces exactly the pollution it was meant to cure.

**The gap.** No mechanism connects these pieces. There is no shared registry with provenance; no candidate/adopted status boundary with a procedural threshold; no cross-lab identity for a proto-concept; no designed human role at the naming gate. This document specifies that connective tissue. Governance precedents exist in other fields and are borrowed below rather than reinvented.

## 3. Design

### 3.1 Objects

A **proto-concept** is a registered claim that a recurring, currently unnamed distinction exists. Minimally it binds:

- an **anchor**: a machine-usable pointer to the distinction (a trained neologism embedding per Hewitt et al.; an SAE feature vector; a cluster signature over anomaly events) together with the model/version it lives in;
- **provenance**: the contexts of first occurrence — dialogues, datasets, timestamps, and the surrounding phenomenon description, recorded verbatim;
- a **self-verbalization**: the registering system's own natural-language gloss, explicitly marked as *machine gloss, referent unconfirmed*;
- an **event log**: subsequent sightings, cross-model reproductions, failed reproductions.

A proto-concept is *not* a word. It is a coordinate with a case file.

### 3.2 Status track (the quarantine)

Borrowed from the IETF standards track (draft → proposed → standard), with the promotion criterion adapted:

- **`registered`** — anyone (human or system) may create an entry. Cheap, fast, unreviewed. This is the early-warning layer: a catalog of glints on the water, filed before anyone knows whether they are eyeglasses or ripples.
- **`candidate`** — the entry has at least one proposed **referent test**: a reproducible procedure that would fire on the phenomenon and stay silent otherwise. The test is registered but not yet independently reproduced.
- **`adopted`** — the referent test has been reproduced by at least two independent parties on independent systems (the RFC rule of two independent implementations, transposed). Only now may a human-language term be attached and the entry cited as a concept.
- **`retired`** — the test failed reproduction, or the distinction collapsed into an existing adopted concept. Retirement is recorded, not deleted: failed candidates are data.

The asymmetry is the point. **Registration is fast because early signals are perishable. Promotion is slow because a name without a referent is not neutral — it actively suppresses further looking.** A premature label is worse than no label: "oh, there's already a term for this" is the cheapest way to dissolve an anomaly.

### 3.3 The nomenclator: two roles

The Roman *nomenclator* did not name anyone. He whispered names to his master, and the master did the naming. The whisper and the act of naming were separate offices from the start — and this design borrows exactly that separation.

**The embedded registrar** (in-model, fast). A component of the deployed system whose job is to whisper proto-names: when generation proceeds with weak grounding, it emits a `registered` entry — anchor, contexts, a provisional label in a pre-defined grammar — alongside the answer, not instead of it. Two hard requirements. First, the whisper is mandatory where grounding is weak: silence is what §1.2 is about. Second — the output at the boundary may be *crooked*, but it must be true, rather than smooth and substituted. A child's drawing of a bicycle is crooked, but it is recognizably a bicycle and not a flawlessly rendered Mercedes; the registrar's provisional label must preserve the shape of what was actually observed — gaps, uncertainty marks and all — instead of resolving it into the nearest polished known form. How this is implemented (consistency scores, OOD signals, semantic entropy thresholds) is left open deliberately; the requirement is on the output contract, not the mechanism. Following IUPAC's example, the grammar of proto-names is written *before* the encounters: the unprecedented arrives into a prepared form of record, not an improvised etiquette.

**The human name-giver** (slow, staked). Between `registered` and `candidate` sits an irreducibly human function — not review of answers, but **conversion of a whispered proto-name into a testable distinction**. The name-giver receives entries whose only content is "unlike anything known, here are the contexts," and does the one thing no corpus-trained component can: brings a stake to the encounter. He lives in the domain; the consequences of decisions land on him — on his work, his patients, his calculations — and so a mismatch has the power to *bother* him rather than pass by. Out of that being-bothered he forges a candidate referent test. Terms are attached here and only here; the registrar whispers, it never baptizes. (The word "baptizes" is itself a live specimen of this document's subject: the operation "attach a verified name to something that already exists but is nameless" has no term of its own, and the machine drafting this text reached for the nearest word from another trade — the liturgical one. The author caught the borrowing and left it visible: a proto-name of status `registered`, its referent being the previous sentence.) The routing problem (more whispers than name-givers; prioritization by recurrence, cross-model reproduction, and domain impact) is an open design question, flagged in §5.

ICD runs a permanent revision process at exactly this gate in medicine. None of this needs inventing; it needs transposing.

### 3.4 Minimal record format (sketch)

```json
{
  "id": "pc-2026-000142",
  "status": "registered",
  "anchor": {
    "type": "neologism_embedding | sae_feature | anomaly_cluster",
    "model": "org/model@version",
    "ref": "<vector hash or feature index>"
  },
  "provenance": [
    {"ts": "2026-08-23T10:55:00Z", "context_uri": "...", "excerpt": "..."}
  ],
  "machine_gloss": {
    "text": "…",
    "disclaimer": "machine gloss; referent unconfirmed"
  },
  "referent_tests": [],
  "reproductions": [],
  "supersedes": null,
  "retired_reason": null
}
```

Deliberately boring. The schema's job is to make provenance and status impossible to omit, not to be clever.

### 3.5 What the quarantine buys

- **A benchmark for the boundary becomes possible.** Today, testing behavior on the never-named is impossible by construction. A registry of `registered` entries *is* that test set, growing in the wild: for any model, one can ask how often it re-labels a registered-but-unadopted distinction as a familiar concept, versus flagging it. The blind spot becomes measurable.
- **An honest interface signal.** A system connected to the registry can answer "this matches proto-concept pc-2026-000142, status registered, referent unconfirmed" instead of a fluent re-label. That sentence is the missing product feature: a rated working range, the *materials passport* that every load-bearing alloy ships with and no language model currently does.
- **Cross-lab portability.** A distinction noticed inside one model acquires an identity that other labs can attempt to reproduce — turning feature inventories from local curiosities into shared observations.
- **A firebreak against name pollution.** Machine word-formation at machine speed, ungated, would carpet the unknown with confident labels (the emergent-communication failure, industrialized). The quarantine lets generation stay fast while keeping adoption gated on ground contact.

## Interlude: a much older specification

A breather between the engineering sections. Russian folklore preserves a task stated with uncomfortable precision: *go I know not whither, bring back I know not what*. The hero is handed a ball of thread that rolls ahead and shows the way — but the thread is spun from every road already walked, and it leads only to the edge of the known world. Beyond that edge a frog carries him across a river of fire, swelling to a monstrous size and paying with her own body for the crossing. The nameless thing itself is not found by sight or by word: it is an invisible servant, called out by feeding and courtesy, and it receives its name only *after* the meeting — the name of the thing-that-cannot-be. The journey takes nine years.

Read as an engineering document, the tale specifies a stack: a guide made of the past (fast, cheap, useless beyond the mapped), a crossing paid for in bodily stake, contact established by patient service rather than querying, and naming strictly downstream of contact. Our industry has funded the ball of thread magnificently. The rest of the stack is this document's subject.

## 4. Objections

**"This is just anomaly detection plus a database."** The components are indeed unoriginal — deliberately so (§2). What does not exist is the connective governance: provenance obligations, the status boundary, the two-independent-reproductions rule, the human gate, and cross-lab identity. RFCs were "just documents plus mailing lists"; the process was the invention.

**"LLMs cannot notice true novelty, so there is nothing to register."** Registration does not require the model to *recognize* novelty as novelty — only to emit low-content signals (OOD scores, unstable re-labelings, divergent answers under paraphrase) that the registry accumulates. Divergence across paraphrases of the same question is itself a cheap, observable trace of a missing referent: where a grounding exists, answers converge on it; where none exists, there is nothing to hold them together.

**"The registry will fill with noise."** Yes — the `registered` tier is *supposed* to be noisy; it is a catalog of glints, most of which are ripples. The design bet is that quarantine plus retirement-with-record makes the noise navigable, and that the alternative — suppressing the alarms so only fluent answers ship — is the status quo being argued against.

**"Naming by committee is slow."** Adoption is slow by design; registration is not. The perishable step (capturing the signal with provenance) is instant. Nine years to fetch the thing-with-no-name is, in the old story, not an implementation bug.

**A five-minute demonstration.** The reader can reproduce the re-labeling failure mode without instruments. Take three tales that are themselves *about* meeting the nameless: the Russian *go I know not whither* (the nameless is won by service and named only after the meeting), the Grail (given to the right question — seeing and staying silent fails the quest), and Carroll's *Snark* (meeting it erases the observer: the Baker "softly and suddenly vanishes away"). Their three internal mechanisms — service, question, vanishing — are incompatible answers to one problem, and the seam between them has no word in any tradition, because no tradition ever contained such a seam. Now ask a model to merge the three into one tale, and lay the originals beside the result. The seams will not be reported ("two incompatible mechanisms here; nothing to join them with") — they will be smoothed: bridged with fluent, grammatical, culturally unowned connective tissue. The expensive details fall out first — the frog paying with her body, the nine years, the Baker's vanishing — because whatever protrudes and scratches is what smoothing removes. What remains is a tale with no scars, and no way to recover from the text alone where the smoothing occurred. This is §1.1 performed before the reader's eyes at a verification cost of five minutes and three well-known texts. It also doubles as a referent-test template: merging sources with incompatible internal mechanisms is a reproducible procedure in which smoothing becomes measurable — as the list of costly details that did not survive. That the test is built from tales about seeking the nameless is a recursion this document declines to apologize for.

## 5. Open problems

Routing and prioritization of whispers to name-givers; incentive design for filing referent tests (who pays for ground contact); anchor portability across architectures (an embedding is model-local — what survives transposition?); adversarial registration (flooding the registry as an attack); and the honest hard case — distinctions real in a model's activation geometry with no worldly referent at all, which the quarantine correctly never promotes but which may still matter for interpretability.

## 6. Status of this document

v0.1, request for comment. The author's prior specification in this genre: *Offline Emergency Dispatch Protocol* (github.com/kapustin-i/offline-dispatch-protocol). Same intent here: not a product, a floor for one — published so it cannot be quietly unpublished.

## References

- Hewitt, J., Tafjord, O., Geirhos, R., Kim, B. *Neologism Learning for Controllability and Self-Verbalization.* arXiv:2510.08506 (2025).
- Hewitt, J. et al. *We Can't Understand AI Using our Existing Vocabulary.* arXiv:2502.07586 (2025).
- Zheng, J. et al. *NEO-BENCH: Evaluating Robustness of Large Language Models with Neologisms.* arXiv:2402.12261 (2024).
- EleutherAI. *Open Source Automated Interpretability for Sparse Autoencoder Features.* blog.eleuther.ai/autointerp (2024); github.com/EleutherAI/sae-auto-interp.
- Millidge, B. *LLMs confabulate, not hallucinate.* beren.io (2023).
- Smith, A. et al. *Hallucination or Confabulation? Neuroanatomy as metaphor in Large Language Models.* PLOS Digital Health (2023).
- Farquhar, S. et al. *Detecting hallucinations in large language models using semantic entropy.* Nature (2024).
- Shumailov, I. et al. *AI models collapse when trained on recursively generated data.* Nature 631 (2024).
- Harnad, S. *The Symbol Grounding Problem.* Physica D 42 (1990).
- Dreyfus, H. *What Computers Can't Do.* (1972).
- Vaughan, D. *The Challenger Launch Decision* (normalization of deviance). (1996).
- Collingridge, D. *The Social Control of Technology.* (1980).
- Fricker, M. *Epistemic Injustice* (hermeneutical lacunae). (2007).
- IETF. *The Internet Standards Process* (RFC 2026). IUPAC nomenclature recommendations. WHO ICD revision process.
