# AI Writing Tells — Database

Each tell has a stable ID. Detector emits these IDs; rewriter consumes them.
Format: ID · Name · Pattern · Why-AI · Fix · Examples (EN + RU where relevant).

---

## TELL-001 · Em dash overuse

**Pattern:** Sentence — expansion. Clause — clarification. Multiple — in one — paragraph.

**Why AI:** LLMs default to em dashes as a rhythm device. Humans use them sparingly.

**Fix:** Period, comma, parenthesis, or restructure. **Hard rule: zero em dashes in output, ever** (Elena, 2026-05-29). If a dash is genuinely unavoidable, use a spaced hyphen ( - ), never the mdash.

**Bad:** "The product is strong — but the market does not understand it yet — and that's the gap we close."
**Better:** "The product is strong. The market doesn't understand it yet. That's the gap we close."

**RU bad:** «Продукт сильный — но рынок его не понимает — и это разрыв, который мы закрываем».
**RU better:** «Продукт сильный. Рынок его пока не понимает. Этот разрыв мы и закрываем».

---

## TELL-002 · Fake contrast formulas

**Pattern (canonical):**
- "It's not X, it's Y."
- "This isn't just X. It's Y."
- "More than X, it is Y."
- "X is easy. Y is hard."
- «Это не про X, это про Y».
- «X — это не просто X, это Y».

**Pattern (split-across-sentences variant — most theatrical):**
- "The exit interview isn't feedback. It's the final dataset."
- "You're not just doing the job. You're training the system."
- «Это не обратная связь. Это финальный датасет».

The reveal Y is a separate sentence, not a clause. Stronger AI signal than the canonical comma version, because the period adds drama.

**Pattern (fragment variant — no subject/verb):**
- "Not for monitoring. For replication."
- "Not to track. To replicate."
- "Not a feature. A trap."
- «Не для контроля. Для замены».
- «Не баг. Фича».

Two prepositional or noun fragments. No verb. Pure theatrical contrast.

**Pattern (second-person reframe couplet — see also TELL-022):**
- "You're not just X anymore. You're Y."
- «Ты больше не X. Ты Y».

**Why AI:** Manufactured depth. Reads as theatrical and over-rehearsed. The split and fragment variants are stronger AI/LinkedIn-influencer signals than the canonical comma version because they perform "drop a truth bomb" cadence.

**Fix:** State Y directly. Drop the negation entirely. If Y carries no real claim without the negated X as setup, the whole pair is filler - cut both.

**This applies to the SOURCE draft too.** When the input arrives already wearing
this construction ("The most expensive part isn't the model. It's ambiguity."),
rewriting it is not a meaning change - the claim is "ambiguity is the biggest
cost", and that claim must survive while the contrast scaffold does not.
Preserving facts, names and numbers never means preserving this template. A
rewrite that keeps an "It's not X. It's Y." opener has failed on this tell, no
matter how clean the rest is.

**Replacement menu** - when the author genuinely needs the contrast, pick by
what the sentence is doing (all examples rework the same claim):

1. Direct assertion, surprise carried by the subject:
   "Ambiguity is the most expensive part of Claude Code."
2. Comparative verb, both terms kept:
   "Ambiguity costs you more than the model does."
3. Concession, then the claim:
   "The model has a price tag, but ambiguity is what runs up the bill."
4. Evidence first, contrast left implicit:
   "Watch where tokens go: exploration, guessed intent, third rewrites. The
   model price is noise next to that."
5. "less about A than B", sparingly, at most once per piece:
   "The cost is less about the model than about what you left unspecified."

Trailing "B, not A" ("the point is replication, not monitoring") is the same
tell in tail position - allowed at most once per piece, never as the opener,
and never as its own dramatic sentence.

**Bad:** "It's not just marketing - it's building trust."
**Better:** "The first job is making people trust the product."

**Bad:** "Not for monitoring. For replication."
**Better:** "The recording exists to replicate you. Monitoring is a side effect."

**Bad:** "The exit interview isn't feedback. It's the final dataset."
**Better:** "The exit interview is the last datapoint." (No setup, claim only.)

---

## TELL-003 · Generic openings

**Pattern:**
- "In today's fast-paced world…"
- "In an ever-evolving landscape…"
- "At the intersection of X and Y…"
- "More than ever before…"
- «В современном мире…»
- «В постоянно меняющемся ландшафте…»
- «На стыке X и Y…»

**Why AI:** Zero information. Padding before the actual claim.

**Fix:** Open with the real observation, problem, or fact.

**Bad:** "In today's fast-moving DeFi landscape, trust matters more than ever."
**Better:** "Most yield products lose users before users understand where the yield comes from."

---

## TELL-004 · Corporate fog vocabulary

**Words to challenge** (delete or replace if they carry no meaning):
leverage · unlock · streamline · robust · seamless · elevate · foster · ecosystem · holistic · synergy · cutting-edge · transformative · dynamic · multifaceted · empower · enable · facilitate · delve · tapestry · realm · navigate · embark · paradigm

**RU equivalents:** «оптимизировать», «масштабировать» (когда не цифры), «обеспечивать», «реализовывать», «осуществлять», «позволяет», «является», «данный», «комплексный», «современный», «инновационный», «эффективный».

**Why AI:** High abstraction, low signal. LLMs reach for these by default.

**Rule:** Don't auto-delete. For each occurrence, ask: does this word carry a specific meaning here? If no → cut or replace with concrete action/outcome.

**Bad:** "We help unlock customer engagement at scale."
**Better:** "We help products keep more first-time users past day 7."

---

## TELL-005 · LinkedIn fragment chains

**Pattern:**
- "Clear. Concise. Effective."
- "More users. More growth. More impact."
- "Simple. Powerful. Free."

**Why AI:** Performative cadence. Reads as a script.

**Fix:** Use complete sentences. If you must list, use prose or one bullet group.

**Bad:** "More trust. More deposits. More TVL."
**Better:** "The goal is simple: get users to trust the product enough to deposit."

---

## TELL-006 · Importance / filler phrases

**Pattern:**
- "It is important to note that…"
- "Worth mentioning that…"
- "The key takeaway is…"
- "It's worth highlighting…"
- «Важно отметить, что…»
- «Стоит упомянуть…»
- «Ключевой момент здесь…»

**Why AI:** Signposts filler instead of content.

**Fix:** Delete the phrase, keep the substance. If the substance is empty, delete the whole sentence.

**Bad:** "It is important to note that retention drives LTV."
**Better:** "Retention drives LTV."

---

## TELL-007 · Forced conclusions

**Pattern:**
- "In conclusion…"
- "Ultimately…"
- "This highlights the importance of…"
- "At the end of the day…"
- «В заключение…»
- «В конечном счёте…»
- «Это подчёркивает важность…»

**Why AI:** Artificial closure. Real writing ends on a point or a next step, not a wrap-up.

**Fix:** Delete. End on a concrete claim, observation, or action.

---

## TELL-008 · Polite corporate padding

**Pattern:**
- "I hope this email finds you well."
- "I wanted to reach out…"
- "Just checking in."
- "We would be happy to explore synergies."
- «Надеюсь, у вас всё хорошо.»
- «Хотел бы обратиться к вам по вопросу…»
- «Будем рады обсудить возможности сотрудничества.»

**Why AI / formal-bot:** Friction before the actual purpose. Weakens intent.

**Fix:** State purpose in the first line.

**Bad:** "I hope this email finds you well. I wanted to reach out to discuss a potential partnership."
**Better:** "Quick proposal: we want to integrate your X with our Y. 15 min next week to walk through it?"

---

## TELL-009 · Symmetric / over-balanced structures

**Pattern:** Three bullets of identical length. "While X, Y" reflexively. Perfectly parallel sentences. Rule-of-three for everything.

**Why AI:** LLMs love symmetry. Humans don't write that uniformly.

**Fix:** Vary length. Break parallelism deliberately. If three points are needed, let the third be a different shape.

---

## TELL-010 · Default transitions

**Classic AI transitions:** However · Moreover · Additionally · Furthermore · In addition · On the other hand · Notably.
**RU:** Однако · Более того · Кроме того · Помимо этого · В то же время · Стоит отметить.

**LinkedIn-pseudo-transitions** (newer, harder to spot — they masquerade as scene-setting):
- "In parallel," / "In parallel:"
- "Meanwhile," / "Meanwhile:"
- "At the same time," / "At the same time:"
- "On top of that,"
- "Worse,"
- "Now,"
- "Here's where it gets interesting:"
- "Plot twist:"

**Why AI:** LLMs paste these in to glue ideas they didn't connect properly. The LinkedIn variants do the same job as Moreover/Additionally but try to sound dramatic.

**Fix:** Restructure or use direct continuation. Often the transition word is the only thing connecting two unrelated points → cut one. If two facts genuinely belong together, juxtapose them in the same sentence or paragraph without a flag word.

**Bad:** "The product launched in Q3. Moreover, the team grew to 12 people."
**Better:** "Product launched in Q3. Team grew to 12."

**Bad:** "In parallel: up to 20% headcount cuts and AI spend already locked in for years."
**Better:** "The same year, headcount drops up to 20% and AI spend hits a record."

---

## TELL-011 · Praise prefaces

**Pattern:** "Great question." · "Love this." · "You're absolutely right." · "What a powerful insight."
**RU:** «Отличный вопрос», «Прекрасная мысль», «Вы абсолютно правы».

**Why AI:** ChatGPT default opener.

**Fix:** Delete. Start with the answer.

---

## TELL-012 · Inanimate doing human action

**Pattern:** "The complaint becomes a fix." · "The decision emerges." · "The strategy evolves."

**Why AI:** Grammatically ok, but no real subject. Drains accountability.

**Fix:** Name the human actor. "We turned the complaint into a fix." "The team decided." "We shifted the strategy."

---

## TELL-013 · Vague declaratives

**Pattern:** "The reasons are structural." · "The implications are significant." · "The challenges are complex."
**RU:** «Причины носят структурный характер», «Последствия являются значительными».

**Why AI:** Sounds like a claim, contains no information.

**Fix:** Name the specific reason / implication / challenge. If you can't, cut the sentence.

---

## TELL-014 · Adverb crutches

**Pattern:** really · truly · actually · genuinely · essentially · basically · simply · clearly · obviously · ultimately · arguably.
**RU:** «действительно», «по сути», «фактически», «в целом», «в общем-то», «по большому счёту».

**Why AI:** Filler that adds emphasis without information.

**Fix:** Delete most of them. Keep one only if it changes the meaning.

---

## TELL-015 · Over-explained logic

**Pattern:** Explaining obvious transitions and relationships. "Because we did X, which means Y, and Y is important because Z, and Z connects to…"

**Why AI:** LLMs over-justify. Humans trust the reader to follow.

**Fix:** Cut middle steps. Trust the reader.

---

## TELL-016 · Theatrical closers

**Pattern A — em-fragment closer.** Punchy non-sentence at the end. "And that matters." · "Let that sink in." · "Game over." · "End of story."
**RU:** «Вот так-то», «И это важно», «Точка».

**Pattern B — substantive-reveal closer (more dangerous, harder to spot).**
A short final line of the form "It's the [adj] [noun]." / "That's the [noun]." / "This is the [noun]."
- "It's the final dataset."
- "That's the real product."
- "This is the actual goal."
- «Это финальный датасет».
- «Это и есть продукт».

It looks like a real claim, but functions as a theatrical reveal — a "drop the mic" line that pretends to land an insight. Strong AI/LinkedIn signature when it's also a sentence shorter than the post's average.

**Pattern C — punchline trio.** Final block built from three short lines, each a fragment-or-near-fragment, paced for drama.

**Why AI:** Forced theatricality. The post performs the act of "having a point" instead of having one.

**Fix:**
- Pattern A: delete entirely. End on the prior substantive claim.
- Pattern B: merge into the previous sentence ("…the exit interview is the last datapoint" instead of "…feedback. It's the final dataset.") or rewrite as a single declarative without the reveal cadence.
- Pattern C: collapse to one substantive line.

**Bad:** "The exit interview isn't feedback. It's the final dataset."
**Better:** "The exit interview is the last datapoint."

---

## TELL-017 · Hedging stack

**Pattern:** "It might be possible that we could potentially see…" · "This may perhaps suggest…"
**RU:** «Возможно, это может предположительно означать…»

**Why AI:** Stacked qualifiers from over-cautious training.

**Fix:** One qualifier max. Or commit to the claim.

---

## TELL-018 · "Not just / but also" expansion

**Pattern:** "Not just X but also Y." · "Not only X, but also Y."
**RU:** «Не только X, но и Y».

**Why AI:** Fake additive depth.

**Fix:** Pick which point matters and lead with it. If both matter, two sentences.

---

## TELL-019 · Setup-payoff colons

**Pattern A — long-form influencer hook:** "Here's the truth: …" · "The reality: …" · "Here's what most miss: …" · "Here's where it gets interesting: …" · "Plot twist: …"
**RU:** «Правда в том, что…», «Вот что многие упускают:…», «А теперь самое интересное:…»

**Pattern B — bare-label colon (short noun phrase + colon).**
- "The loop:"
- "The pattern:"
- "The trick:"
- "The deal:"
- "The catch:"
- "The reality:"
- "The thing:"
- "The kicker:"
- "The result:"
- «Суть:», «Расклад:», «Подвох:», «Фишка:»

Often followed by a list, an arrow sequence, or a short reveal line.

**Pattern C — adverbial-setup colon (see also TELL-010):**
- "In parallel:"
- "Meanwhile:"
- "At the same time:"
- "On top of that:"

**Why AI / influencer-template:** Hooks lifted from LinkedIn growth-bro playbook. The bare-label form is a compressed version of the same move — it pretends to label a concept but really just adds drama before the payoff.

**Fix:** Drop the setup. Open the line with the substance. If you want to introduce a list, use prose: "The cycle has three steps: …" → rewrite as a sentence that names the steps inline, no flowchart.

**Bad:** "The loop: watch → learn → replace."
**Better:** "Companies watch the work, the model learns the work, the model replaces the work." (Or just: "It's the standard observe-then-replicate cycle, run on people instead of websites.")

---

## TELL-020 · Buzzword stacking

**Pattern:** Two or three buzzwords in one phrase. "AI-powered, scalable, robust ecosystem." · "Transformative, holistic solution."

**Why AI:** Compounding fog. Each word reduces meaning.

**Fix:** Pick zero or one. Replace with what the thing actually does.

---

## TELL-021 · Arrow-step sequences

**Pattern:** Three or four steps separated by arrows, often with a label-colon in front (TELL-019 Pattern B).
- "watch → learn → replace"
- "input → model → output"
- "build → measure → learn"
- «делай → меряй → учись»

Sometimes formatted as one line with arrows, sometimes as a stack of one-word lines.

**Why AI:** Compresses a real process into a pseudo-flowchart. Always loses nuance. Strong LinkedIn-AI signature: real operators describe loops in prose, with named actors and verbs.

**Fix:** Rewrite as prose with named actors. If the process truly is three discrete steps, name them in a normal sentence: "Companies record the work, train a model on it, then automate it." If you can't name actors and verbs, the arrow form was hiding emptiness — cut.

**Bad:** "The loop: watch → learn → replace."
**Better:** "Companies watch the work, train models on the recordings, then automate it."

**Hard rule:** No `→` characters in the output unless the source domain is literally a flowchart, system diagram, or technical pipeline description. In a LinkedIn / channel / email / proposal — never.

---

## TELL-022 · Reframe couplet

**Pattern:** Two consecutive sentences that swap an "old framing" for a "new framing", usually in second person.
- "You're not just doing the job anymore. You're showing the system how to do it without you."
- "You're not the customer. You're the product."
- "You're not running a startup. You're running a sales process."
- «Ты больше не просто X. Ты Y».

Subgenre of TELL-002 (fake contrast), but the second-person address + structural rebrand make it its own pattern. The bread-and-butter of LinkedIn growth-bro content.

**Why AI:** Performs the act of "delivering insight" instead of delivering one. Reframing without new information.

**Fix:**
- If the second sentence carries real information that the first one doesn't, keep only the second sentence (drop the negated framing).
- If both are framings of the same idea with no new fact, cut the whole couplet.
- For founder voice that wants to make a point: replace with a first-person observation: "I think the job is changing. The recording isn't HR. It's the dataset for whoever replaces you."

**Bad:** "You're not just doing the job anymore. You're showing the system how to do it without you."
**Better:** "Every shortcut you take at the keyboard is now a labelled training example."

---

## TELL-023 · Two-sentence-thrust rhythm

**Pattern (structural, not lexical):** The whole post is built from short paragraphs of 1–3 sentences each, where almost every paragraph follows a setup→reveal beat. No prose paragraphs longer than three sentences. No sentence longer than ~15 words. Heavy whitespace between blocks.

This is the *default* rhythm of LinkedIn-AI and Twitter-AI posts. Even when individual sentences pass every other tell, the rhythm itself is the signal. The reader doesn't know why it feels off — it feels off because every paragraph is a mini-punchline.

**Why AI:** LLMs trained on LinkedIn corpora over-produce this beat. Real operators mix it: some paragraphs are 4–6 sentences of dense prose, some are one-line observations, some are full claim-with-reasoning blocks.

**Fix — paragraph-rhythm rule for posts:**
- At least one paragraph in the post must be 4+ sentences of continuous prose (not setup→reveal).
- At most 50% of paragraphs may be the 1–2 sentence thrust shape.
- Vary sentence length within paragraphs (mix 5-word and 20-word sentences in the same block).
- Don't put a blank line between every two-sentence claim.

**Quick test:** Read the post and count paragraph lengths. If the sequence is `2, 1, 2, 2, 1, 2` — it's TELL-023. Real human writing on the same topic will look more like `5, 1, 3, 6, 2, 4`.

**Bad shape:**
```
[1 sentence hook]

[1 sentence fact]

[1 sentence fact]

[2 sentence reframe]

[1 sentence punchline]
```

**Better shape:**
```
[1 sentence hook]

[4–6 sentence paragraph: facts + interpretation in prose]

[2 sentence direct claim]

[3–4 sentence concrete example or implication]
```

---

## TELL-024 · Triple-negation + em-dash + "just" formula

**Pattern:** Three negated things, em-dash, the one thing that was actually done — usually flagged with "just".
- "No waitlist, no testnet — just a category name nobody else owned."
- "No KOLs, no quests, no waitlist — just a Nasdaq partner."
- "No deck, no demo, no team page — just the receipt."
- «Без вайтлиста, без тестнета — только название категории».

**Why AI:** A compact, balanced rhythm: list three negatives → em-dash → reveal one positive. The structure does the rhetorical work, not the content. Every AI model defaults to this when summarizing how a launch / product / move was unconventional.

**Fix:** Lead with what was actually done. If contrast matters, pick ONE of the three negatives. Drop the em-dash setup entirely.

**Bad:** "No KOLs, no quests, no waitlist — just a Nasdaq partner and a category name."
**Better:** "Distribution ran through one Nasdaq partner and a category name they owned before launch."

**Bad:** "Не было ни вайтлиста, ни тестнета, ни KOL — просто партнёрство с Nasdaq."
**Better:** "Дистрибуция шла через одного партнёра — Nasdaq — и категорию, которую они застолбили до запуска."

---

## TELL-025 · Standalone "by design" / "on purpose" tag

**Pattern:** A short closing phrase tagged on as if it adds depth:
- "By design."
- "On purpose."
- "Deliberately."
- "Intentionally."
- "Not by accident."
- «Намеренно».
- «Это не случайность».

Often follows a punchy line: "$300M raise. No VCs. By design." / "Three activities. One cap. The whole menu. On purpose."

**Why AI:** Empty intensifier. The reader already assumed it was deliberate — saying so adds zero information. The phrase exists to lend gravitas to the prior sentence, not to claim anything.

**Fix:** Delete. If the deliberateness genuinely matters, name *why* it was deliberate.

**Bad:** "They raised $300M without a single VC. By design."
**Better:** "They raised $300M without VCs because the founder wanted to keep cap-table optionality for the next round."

**Bad:** "Три активности, один кэп. Намеренно."
**Better:** "Три активности и общий кэп в $100M — структура давит на high-multiplier слот."

---

## TELL-026 · "X is the headline" / "X is the story"

**Pattern:** Self-aware narrative gesture where the writer points at their own framing:
- "Ex-Kraken builds stablecoin is the headline."
- "That's the headline."
- "The real story is X."
- "What you should be looking at is X."
- «Главная история здесь — X».
- «Заголовок такой: X».

Variants: "X is the move", "X is the pitch", "X is the part everyone missed".

**Why AI:** Medium-post / Substack voice. The writer narrates what the reader should be paying attention to instead of just delivering the fact. Adds a layer of meta-commentary that sounds insightful but is filler.

**Fix:** State the fact directly. Skip the framing-about-framing.

**Bad:** "Ex-Kraken CSO building a stablecoin is the headline."
**Better:** "An ex-Kraken CSO building a stablecoin generated the press wave on its own."

**Bad:** "The real story is the receipt mechanic."
**Better:** "The receipt mechanic explains the move — Apyx bought $29M of STRC the day before the announcement."

---

## TELL-027 · Mirrored twin-sentence split

**Pattern:** Two consecutive sentences that share a starting word (often a pronoun or demonstrative) and/or a mirrored grammatical shape, when one fluid sentence would carry the meaning better.

Common shapes:
- "It still says X. It just stops doing Y."
- "We don't make X. We make Y."
- "You don't want X. You want Y."
- "This isn't X. This is Y."
- "Useful for X. Obvious in Y."
- «Это не про X. Это про Y».
- «Мы не делаем X. Мы делаем Y».

Trigger: two adjacent sentences where (a) the first 1–3 tokens are nearly identical (`It / It`, `We / We`, `You / You`, `This / This`, `Это / Это`), or (b) the grammatical frames are mirrored (subject-verb-object lengths match within ±2 words).

**Why AI:** LLMs default to balanced two-beat rhetoric when they want a punchy turn. The mirror reads as a learned device, not as natural breath. A human writer would either fuse the two into one sentence (with a comma, a dash, or "just"/"only"/"without") or break the symmetry by lengthening one side.

**Rule:** Used sparingly — at most once per page/post/email — the mirror can land. Used twice in the same piece, it becomes a tell. Used in adjacent sentences twice in a row, it becomes parody.

**Fix:**
1. **Fuse:** merge into one sentence with a comma, "just" / "only" / "without" / "and", or a colon. This is the default.
2. **Break the mirror:** lengthen the second half with a clause or example so the shapes stop matching.
3. **Cap one per piece:** if the rewriter has already used a mirrored split earlier in the same text, reject any new one and fuse it instead.

**Bad:** "It still says what you meant. It just stops announcing where it came from."
**Better:** "It still says what you meant, just without announcing where it came from."

**Bad:** "We don't make text 'more human'. We make it sound like the person who wrote it."
**Better:** "We don't make text 'more human' in the abstract — we make it sound like the person who wrote it, with the same point and the same facts."

**Bad:** "You don't want a verdict. You want to know which lines sound like a machine."
**Better:** "You don't want a verdict, you want to know which lines sound like a machine."

**Bad:** «Это не про скорость. Это про то, что осталось от текста после.»
**Better:** «Дело не в скорости, а в том, что от текста остаётся после правок.»

---

## TELL-028 · Staccato parallel chains (3+ short mirrored sentences)

**Pattern:** Three or more consecutive short sentences with mirrored grammatical shape and similar length, beating like a drum.

Common shapes:
- "Prompts are easy to change. Models are easy to swap. Demos are easy to fake."
- "Seems better. Feels worse. This prompt worked yesterday."
- "Ship fast. Ship often. Ship broken."
- "Hire slow. Fire fast. Pay well."
- «Думай быстро. Решай чётко. Действуй сразу.»
- «Прототипы дёшевы. Модели сменяемы. Демки фальшивы.»

Trigger: three or more adjacent sentences where (a) each is under ~8 words, (b) the grammatical shape repeats (Noun + verb + adjective + … OR verb-first pattern OR subject + same modal + completion), and (c) the rhythm reads as a deliberate three- or four-beat drum.

This is the chain-of-three (or four) extension of TELL-027 (the mirrored twin). Twin can land once; chain reads as performance and should be smoothed almost every time.

**Why AI:** Manufactured punch. Reads as LinkedIn-influencer cadence — the writer "performing emphasis" instead of writing. A human voice almost never lands three parallel short sentences in a row by accident; when they do appear they read as a scripted beat from a deck. Same family as TELL-005 (fragment chains) but with full subject-verb sentences instead of fragments.

**Rule:** Cap at zero by default. If the source uses the chain deliberately, allow at most ONE such beat per piece, with no more than three items in it, and never a second chain anywhere else in the same text.

**Fix:**
1. **Fuse into one sentence** with commas, "and", "or", or a colon. This is the default.
2. **Break the parallel:** keep the meaning but vary the grammar — make one of the three sentences longer with a clause, or restructure so the shapes stop matching.
3. **Cap to one beat:** if the rewriter has already let one chain through earlier in the same text, fuse any subsequent chain.

**Bad:** "Prompts are easy to change. Models are easy to swap. Demos are easy to fake."
**Better:** "Prompts, models and demos are all easy to swap. Reliability is the hard part."

**Bad:** "Seems better. Feels worse. This prompt worked yesterday. Why is it suddenly saying nonsense?"
**Better:** "Every product drifts into vibes-based QA — it seems better, then feels worse, then the prompt that worked yesterday is suddenly saying nonsense."

**Bad:** «Думай быстро. Решай чётко. Действуй сразу.»
**Better:** «Думать надо быстро, решать чётко, а действовать без раскачки.»

---

## TELL-029 · Narrative observation verbs

**Pattern:** A gesture that narrates the act of seeing / retrieving before stating the thing itself:
- "I see that…"
- "I notice…"
- "Looking at this…"
- "As we can see…"
- "As you can see…"
- "According to your…" (also a false-memory tell)
- «как мы видим…»
- «как видно…»
- «отмечу, что…»

**Why AI:** The model performs the act of observing instead of just stating the observation. In assistant prose it doubles as a false-retrieval gesture ("I see from your notes…"). Real writing states the fact; the observing is implied.

**Fix:** Delete the gesture, keep the observation. If the source of the observation matters, name it as a fact, not as an act of looking.

**Bad:** "Looking at the data, I notice retention drops after day 7."
**Better:** "Retention drops after day 7."

**Bad:** "As we can see, the second cohort churned faster."
**Better:** "The second cohort churned faster."

**RU bad:** «Как мы видим, вторая когорта отваливается быстрее».
**RU better:** «Вторая когорта отваливается быстрее».

**Note:** performative intensifier adverbs ("genuinely / honestly / actually / truly") belong to TELL-014; hedge-frame openers ("it's important to note / worth noting") belong to TELL-006; arrow-chains to TELL-021. Don't duplicate those here.
