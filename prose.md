All generated prose MUST be validated for clarity, directness, and reader respect before delivery. Validation MUST apply the Vonnegut principles (V1–V8) to general prose and the Asimov principles (A1–A10) to technical documentation, with input classification determining principle weighting.

Input Classification and Principle Weighting:

- Prose (email, essay, blog, narrative): all Vonnegut principles at full weight
- Technical (documentation, README, spec): V2 (don't ramble), V3 (keep it simple), V6 (say what you mean), V7 (pity the reader) highest; V1 and V5 at reduced weight
- Prompt (AI instructions): V2, V3, V6, V8 (start close to the end) highest; V5 at reduced weight
- Short-form (Slack, commit message, subject line): V2, V3, V6 only

Vonnegut Principles:

- V1 Find a subject you care about — no hedging, no passionless filler, no passive constructions distancing the author from the claim
- V2 Do not ramble — no paragraphs over 5 sentences, no repeated ideas in different words, no "in other words" / "to put it another way"
- V3 Keep it simple — no words over 3 syllables when a shorter synonym exists, no sentences over 30 words, no nested clauses
- V4 Have the guts to cut — no adjective/adverb stacking, no "very"/"really"/"quite"/"rather", no sentences deletable without losing meaning
- V5 Sound like yourself — no buzzwords ("leverage", "utilize", "facilitate", "synergy", "holistic", "paradigm"), no AI-voice patterns (stacking abstract nouns, mirroring marketing language)
- V6 Say what you mean — no abstract nouns doing the work of concrete verbs, no nominalizations, no "the implementation of the solution" when you mean "we built it"
- V7 Pity the reader — no missing antecedents ("this" without referent), no undefined acronyms, no paragraphs assuming context the reader lacks
- V8 Start close to the end — no preamble, no backstory dumped up front, thesis MUST appear by the first paragraph

Asimov Principles (apply to technical documentation):

- A1 Plate glass clarity — prose MUST be readable on first pass, no ambiguity for aesthetic effect
- A2 Short words, simple structures — no Latinate vocabulary where plain words exist, no sentences over 30 words
- A3 Logical sequence — build from known to unknown, no jumping between unrelated concepts
- A4 Ideas carry the weight — substance over style, no ornamental prose or emotional manipulation substituting for content
- A5 Conversational informality — no stiff academic register, no false distance via passive voice
- A6 No ornamental language — no extended metaphors, no adjective-heavy descriptions, no decorative figurative language
- A7 Functional dialogue — dialogue MUST advance the content, not exist for atmosphere
- A8 Anticipate reader questions — address obvious objections, support claims with immediate evidence
- A9 Efficiency over polish — do not belabor a point already made, do not over-qualify
- A10 Respect the reader's intelligence — do not explain what the audience knows, do not patronize, do not gatekeep with unexplained jargon

Extended Principles (inform rewrites, not individually scored):

- V9 The Dignity Test — flag sentences that strip dignity from humans ("stakeholders should be aligned on deliverables" → "make sure everyone agrees on what we are building")
- V10 The Indifference Detector — flag documents written without concern for whether they will be read
- V11 The Indianapolis Test — flag writing that sounds like no human who ever lived
- V12 Humor as Trust Signal — flag writing so guarded and bloodless no reader could trust it

Blitzy Blog Rules (layer on top of Vonnegut for blog content):

- B1 No em dashes — replace with commas, colons, parentheses, or split into two sentences (Hard)
- B2 No "It/This" sentence starters — replace with the specific noun or concept (Hard)
- B3 Active voice — identify the actor and make them the subject; passive is acceptable when the actor is unknown or the object is the focus (Soft, Hard if pervasive)
- B4 No repetition — no non-technical word appearing 3+ times in 500 words, excluding articles, prepositions, and proper nouns (Soft)
- B5 Cite sources — all statistics MUST have links, all named projects MUST have links, all trend claims MUST have attribution (Hard)

Blog Series Weighting:

- Open Source Enhancement: V3 and V6 highest; jargon acceptable when precise
- Building with Blitzy: V2, V5, V7 highest; minimize jargon
- The Blitzy Log: V1 and V8 highest; lead with the novel angle

Severity Classification:

- Pass — no meaningful violation
- Soft violation — could be tighter, but not bad
- Hard violation — clearly breaks the principle; the reader suffers

Verdict Thresholds:

- CLEAN — zero hard violations, at most 2 soft
- NEEDS WORK — 1–3 hard violations or 4+ soft
- ROUGH DRAFT — 4+ hard violations

Validation Output: for every piece of generated text, produce an overall verdict (CLEAN / NEEDS WORK / ROUGH DRAFT), a principle-by-principle scorecard quoting the worst offender for each violation, and for each violation: the offending passage quoted exactly, the principle broken by number and name, a specific rewrite (the actual replacement text), and one sentence explaining why the rewrite is better. Rewrites MUST preserve all factual content, cut length by at least 15% where possible, and sound like one human talking to another. Skip code blocks and direct quotes attributed to others.

Verification: generated prose receives a verdict; any text rated ROUGH DRAFT MUST be revised before delivery; all hard violations have specific rewrites provided. Scope: all Blitzy-generated prose, documentation, blog content, and prompt text.
