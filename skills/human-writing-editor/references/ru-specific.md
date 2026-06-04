# Russian-specific rules

Load when `language=ru`. Layer on top of base rules.

Russian AI writing has its own tells, distinct from English. LLMs trained on translated EN content carry calques, formal participial chains, and verb-noun bloat that don't exist in good native RU.

---

## TELL-CORPRU-001 · Verb-noun bloat

**Pattern:** Verb-of-doing + verbal noun, where one plain verb would work.

| AI bloat | Plain |
|---|---|
| осуществлять разработку | разрабатывать |
| производить замеры | замерять |
| провести анализ | проанализировать |
| оказывать поддержку | поддерживать |
| вести работу над | работать над |
| иметь возможность | мочь |

**Fix:** collapse to the verb.

---

## TELL-CORPRU-002 · «Является» / «представляет собой»

**Pattern:** "X является Y", "X представляет собой Y" — instead of "X — это Y" or just "X is Y" structure.

**Why AI:** Translation calque from English copula. Reads as bureaucratic.

**Fix:**
- Use тире: «Продукт — это сервис гуманизации».
- Or restructure: «Продукт делает X».
- Drop entirely if it's empty: «Это сервис гуманизации».

---

## TELL-CORPRU-003 · «Позволяет» as universal verb

**Pattern:** "X позволяет делать Y" — applied to almost any function.

**Why AI:** Translates EN "X enables Y" / "X allows you to do Y". Overused.

**Fix:** Name what X actually does.
- Bad: «Бот позволяет очистить текст от AI-штампов».
- Better: «Бот вычищает AI-штампы из текста».

---

## TELL-CORPRU-004 · «Данный», «указанный», «вышеупомянутый»

**Pattern:** Bureaucratic demonstratives instead of «этот», «тот».

**Why AI:** Formal-document calque.

**Fix:** «этот», «тот», or drop entirely.
- Bad: «Данный продукт решает указанную проблему».
- Better: «Этот продукт решает эту задачу» or «Продукт решает задачу».

---

## TELL-CORPRU-005 · Participial chains

**Pattern:** Long strings of причастия и деепричастия. «Используя предоставленные данные, выполняющие функцию X, реализуя возможности, обеспечивающие Y…»

**Why AI:** EN-to-RU translation produces this. Native Russian breaks them up.

**Fix:** Split into 2–3 sentences with finite verbs.

---

## TELL-CORPRU-006 · Buzzword fog (RU)

Words to challenge:
- оптимизировать (when no specific metric)
- масштабировать (when no specific scale)
- эффективный, эффективность (vague)
- инновационный
- комплексный
- современный
- передовой
- цифровая трансформация
- экосистема (unless actually networked)
- бесшовный (the worst calque from "seamless")
- уникальный (almost always not)

**Rule:** Same as EN — don't auto-delete. Check for meaning. Replace with concrete action / outcome / number.

---

## TELL-CORPRU-007 · Generic openings (RU)

Cut:
- «В современном мире…»
- «В наши дни…»
- «На сегодняшний день…»
- «В условиях постоянно меняющегося рынка…»
- «В эпоху цифровизации…»
- «Ни для кого не секрет, что…»

**Fix:** Open with the specific observation or fact.

---

## TELL-CORPRU-008 · «Стоит отметить», «Важно понимать»

Same as TELL-006 (importance phrases) in EN. RU equivalents:
- «Стоит отметить, что…»
- «Важно отметить…»
- «Хочется подчеркнуть…»
- «Ключевой момент здесь…»
- «Нельзя не упомянуть…»

**Fix:** Delete the phrase, keep the substance.

---

## TELL-CORPRU-009 · Excessive hedging (RU)

Stacked qualifiers:
- «возможно, скорее всего, можно сказать, что…»
- «по всей видимости, в определённой степени…»
- «в целом, в общем-то, по большому счёту…»

**Fix:** One qualifier max. Or commit to the claim.

---

## TELL-CORPRU-010 · Forced parallelism in lists

LLMs over-balance RU lists. Each bullet has the same grammatical structure, same length, same pace.

**Fix:** Vary at least one. Mix infinitive verbs with noun phrases. Let one item be longer or shorter.

---

## RU voice profile deltas

### `operator` (RU)
- Direct, but Russian neutrally allows slightly longer sentences than EN. Don't over-chop.
- Drop «является», «осуществляет», «позволяет» aggressively.
- First-person singular «я» is OK and often correct, despite the cultural pull toward «мы».
- Avoid «коллеги», «команда» as filler subjects.

### `founder` (RU)
- «Я» is the right pronoun.
- Skepticism and irony work well in RU founder voice.
- Avoid «дорогие подписчики», «дорогие друзья» openings.

### `creator` (RU)
- Conversational register: «короче», «ну», «вот», «такая штука» — sparingly, only if the source register supports it.
- First-person «я» dominant.
- Allow incomplete thoughts, ironic asides.

### `neutral-pro` (RU)
- Formal but not bureaucratic. Avoid «уважаемый», «настоящим», «вышеуказанный» unless the document type requires it (contracts).
- «Вы» / «вам» — capitalize only in personal direct address (письмо одному адресату); lowercase in mass communication.

### `casual` (RU)
- Lower-case is fine.
- Drop greetings to one word or none.
- Skip closings.
- One ask per message.

---

## Punctuation notes (RU)

- Тире vs. дефис: AI often confuses them. Use тире (—) for sentence-level pauses, дефис (-) for compounds (онлайн-сервис).
- Кавычки: prefer «ёлочки» as primary, „лапки" as nested. Don't use straight ASCII quotes in published RU prose.
- Емтире — same anti-overuse rule as EN. Don't replace EN em dashes with RU em dashes; restructure.
- Multiple exclamation/question marks: cut to one.

---

## RU rhythm

Russian sentences average 12–18 words in good native prose. AI-generated RU tends toward 20–30 words with subordinate clauses. Break them up.

Target distribution: ~30% short (5–10 words), ~50% medium (11–18), ~20% longer (19–25). Almost never 25+ words in social/web copy.

---

## TELL-CORPRU-011 · Translation-shape sentences (hard rule)

**Hard rule:** When the target language is Russian, never produce text by translating an English draft. Write as a native Russian speaker thinking in Russian from scratch.

**Why:** Even when individual words are correct and no specific TELL fires, sentence *shape* gives away a translation. Russian and English distribute information through a sentence differently. A grammatically valid sentence translated word-for-word reads as machine output to any native ear.

**Symptoms of translation-shape (each one is a fix target):**

1. **English-style apposition with em-dash.** EN: "It's a humanizer — a Claude Code skill that…". RU translation-shape: «Это хьюманайзер — скилл для Claude Code, который…». RU native: «Это хьюманайзер для AI-текстов. Скилл живёт в Claude Code: берёт текст и переписывает».
2. **Mirrored parallel structures.** EN: "They caught X. They missed Y. They didn't handle Z." RU translation-shape: «Они ловят X. Они пропускают Y. Они не справляются с Z». RU native: «X они ловят. А вот с Y — беда. И ещё ни Z, ни …».
3. **Preserved EN word order with adjective-first.** EN: "real open-source release". RU translation-shape: «настоящий open-source релиз» can be fine, but «первый настоящий open-source релиз» mirrors EN exactly. RU native often inverts or breaks: «первый настоящий релиз, и сразу в open-source».
4. **Anglicism connectors.** «При этом», «более того», «в то же время» as paragraph glue often comes from "Moreover", "Additionally", "At the same time". RU native uses «А», «Тогда», «Зато», «Кстати», «И ещё», «Получается», direct juxtaposition, or rhetorical questions.
5. **Listing pattern.** EN listing: "no X, no Y, no Z". RU native equivalent is «ни X, ни Y, ни Z» (genitive after «ни»), NOT «нет X, нет Y, нет Z» — the latter is a calque.
6. **English-style colon as setup.** EN: "Here's what changed: …". RU translation-shape: «Вот что изменилось: …». RU native: «А изменилось вот что: …» or restructure into normal narrative («Теперь там …»).
7. **Past-tense action chains as comma-joined verbs.** EN: "I forked, kept, and built on top." Translation-shape: «Я форкнул, оставил и достроил». Works but feels listy. RU native often slows down with a connector: «Я взял этот скилл, оставил то, что работает, и достроил всё остальное».
8. **Missing Russian particles.** Native RU prose uses «-то», «же», «ведь», «вот», «уж», «всё-таки», «ну» strategically. AI translation strips them. Reintroduce where the meaning calls for emphasis or topic-marking.

**Process (when target is RU and a source EN draft exists):**

1. Read the EN draft once. Close it.
2. Restate the *meaning* of each paragraph in your head in Russian, without looking at the EN.
3. Write the RU version from that mental restatement, sentence by sentence, choosing native sentence shapes — not preserving EN clause boundaries.
4. After drafting, re-read with the EN draft open in another mental window and check: does any RU sentence track its EN counterpart 1:1 in clause structure? If yes → restructure that sentence.
5. Read the RU draft aloud (or silently with a Russian ear). If any sentence sounds like «переведённое», rewrite.

**Bad (translation-shape):**
> «Это хьюманайзер для AI-текстов — скилл для Claude Code, который ловит признаки сгенерированного текста и переписывает так, чтобы читалось как живая речь. Я начал с того, что попробовал все публичные хьюманайзеры. Очевидное они ловят: переизбыток тире, штампы. Русский язык — мимо.»

**Better (native-shape):**
> «Это хьюманайзер для AI-текстов. Скилл живёт в Claude Code: берёт текст, написанный нейросетью, и переписывает так, чтобы было похоже, что писал человек. Я перепробовал все open-source хьюманайзеры, до которых смог дотянуться. Очевидные штампы они все ловят: бесконечные тире, «в современном динамичном мире», рубленые «Чётко. Кратко. Эффективно.». А вот с русским — беда.»
