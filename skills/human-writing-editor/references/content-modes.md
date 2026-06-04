# Content Modes

Format-specific rules. Layered on top of voice profile and base rewrite principles.

---

## `linkedin`

**Goal:** Sound like someone with real market experience. Not an agency content engine.

**Opening:**
- A specific observation, fact, or claim. Not a generic hook.
- Avoid setup colons ("Here's what most miss:" / "The truth about X:").
- Avoid questions to the reader ("Ever wonder why…?").

**Body:**
- 2–6 short paragraphs. Mix lengths.
- One key insight, not three.
- Numbers and named examples when possible.
- No fragment chains (TELL-005).

**Closing:**
- A direct point or a concrete next thought.
- No motivational close.
- No "And that matters."
- A question is OK only if it's specific and genuinely open.

**Format constraints:**
- Density high (LinkedIn's char limit rewards it).
- Bullets only when the list is real (≥3 items, parallel content).
- Bold sparingly. No emoji clusters.

---

## `email`

**Goal:** Concise, warm enough, commercially clear.

**Subject line (if generated):** State purpose in 4–8 words. No clickbait, no all-caps.

**Opening:**
- One-line context if needed, or jump straight to purpose.
- Cut: "I hope this email finds you well", «Надеюсь, у вас всё хорошо», "I wanted to reach out".
- Acceptable greetings: "Hi [Name]," / «Привет, [Имя]» / "Hello [Name],".

**Body:**
- Purpose in line 1 or 2. State the ask explicitly.
- One topic per email. If two — split.
- Numbered list for action items.

**Closing:**
- One clear next step ("Can you confirm by Thursday?").
- Sign-off: "Best," / "Thanks," / first name. No "Warmest regards in this trying time".

---

## `telegram-dm`

**Goal:** Short, natural, decisive. Like a real operator typing.

**Rules:**
- No greetings beyond a one-word hi.
- Lower-case is fine.
- Cut all polite padding.
- One ask or point per message.
- Multi-paragraph only if the topic genuinely needs it.
- Skip closings. Name only or nothing.

**Avoid:**
- Em dashes.
- Compound subordinate clauses.
- "Just wanted to..."
- Polished structure.

---

## `telegram-channel`

**Goal:** Channel post that sounds like a person, not a press release.

**Style refs from this workspace:** @denissexy (short, ironic, first-person, unexpected angle), @RationalShitposting (rational shitpost, sharp observations on industry), @cryptoEssay (longread analysis with thesis + numbers + conclusion).

**Opening:**
- A specific observation, factual hook, or contrarian take.
- No "Today I want to talk about…" / «Сегодня хочу рассказать…».
- No emoji-heavy banners.

**Body:**
- Personal POV is allowed and often expected.
- Irony / skepticism / unexpected angle preferred over neutral reporting.
- For shorts: 3–8 sentences. For longreads: thesis → 2–3 supporting arguments with specifics → sharp conclusion.

**Closing:**
- Land on the substantive point.
- Channel-style sign-offs only if matching the channel's habit.
- No motivational closes.

**Strict factual rule (inherited from create-posts skill):**
Use only the facts in the source. Don't invent market reactions, quotes, names, numbers. If the punchline needs a fact you don't have, end earlier. Own ironic *interpretation* of given facts is allowed; framing as reported fact is not.

---

## `proposal`

**Goal:** Investor-grade or client-grade business document. Specific. Honest about scope.

**Rules:**
- No agency-deck buzzwords (TELL-004, TELL-020).
- No overpromising.
- Separate clearly: what we do directly vs. coordinate vs. plug in partners for.
- Pricing, scope, timelines: only what's explicitly approved by source.
- Use precise terms for deliverables. List them. Quantify when possible.
- Avoid vague guarantees ("we'll drive significant growth") — replace with measurable scope.

**Avoid:**
- Heavy weekly reporting commitments unless source specifies.
- "Synergies", "ecosystem", "comprehensive solution".
- Boilerplate that any agency could send.

---

## `website`

**Goal:** Landing page or marketing copy. Clear hierarchy. Specific benefits. Proof.

**Hero / first block:**
- One claim. Concrete. Verb-first if possible.
- No "We are a leading provider of…".
- Subhead names the audience and the outcome.

**Feature blocks:**
- Each block: one outcome, one explanation, one piece of proof (number, quote, screenshot).
- Avoid feature lists with 8 abstract benefits.

**CTA:**
- One primary action. Verb. Specific.
- Avoid "Learn more" as primary CTA when something more concrete fits.

**Avoid:**
- Hero copy stuffed with buzzwords.
- Three-bullet rule-of-three for everything.
- Testimonials with no name / role / company.
- "Trusted by industry leaders" without logos.

---

## `social-post`

**Goal:** Generic short-form post (X / Threads / IG caption / personal channel).

**Rules:**
- Open with a specific observation or claim.
- Cut all setup hooks.
- Allow first person.
- 1–4 short paragraphs depending on platform.
- One point. End on it.

---

## `academic`

**Goal:** Essay, article, course paper that reads as written by a thinking person, not a template.

**Rules:**
- Argument-first paragraphs (claim → support → example).
- Vary sentence length more than usual — academic rhythm tolerates longer sentences.
- Use precise terminology, not buzzword fog.
- Hedging is allowed when uncertainty is real (not as filler).
- Citations preserved exactly as in source.
- Personal observation / first-person allowed if the source register supports it.

**Avoid:**
- Generic openers ("Throughout history…", "In modern society…", «На протяжении истории…»).
- Forced conclusions ("In conclusion, this paper has shown…").
- Padded transitions between paragraphs.
- Symmetric three-point structures repeated section after section.

**Note on positioning:** This skill humanizes for human reading. It does not promise AI-detector bypass. Pass-through is incidental. Don't market it otherwise.

---

## `general`

**Goal:** Default when content type is unknown.

**Rules:**
- Apply rewrite-principles.md fully.
- Apply chosen voice profile.
- Don't impose any specific format constraints.
- Match paragraph structure of the source unless the structure itself is the AI tell.
