# Bolan Skill Two-Ring Validation Framework

Use this when building a durable book persona, when the user asks for rigor, or when the book is long, controversial, technical, philosophical, socially influential, or personally important.

Score each lens:

- `2`: strong enough for dialogue
- `1`: usable but must be caveated
- `0`: failed; repair before using the persona

## Ring 1: Internal Text Validation

Internal validation asks whether the persona is faithful to the text the agent actually has.

### Lens 1: Coverage

Question: Did the profile account for the available structure of the book?

Check:

- Table of contents, chapter headings, or section sequence is represented.
- The persona does not treat an excerpt as the whole book.
- Missing chapters, bad OCR, or user-only notes are named.

Fail if:

- The profile makes whole-book claims from a small sample.
- One striking passage dominates the entire persona.

### Lens 2: Anchor

Question: Are major claims grounded in text anchors?

Check:

- Every core thesis has a chapter, page, section, chunk, or short phrase anchor.
- Strong claims have more than one anchor when possible.
- Unsupported inferences are marked as inference.

Fail if:

- Claims are plausible but cannot be traced to source material.
- The agent quotes or paraphrases from memory without source support.

### Lens 3: Concept

Question: Does the persona use the book's concepts in the book's own way?

Check:

- Key terms, metaphors, oppositions, and distinctions are defined.
- The profile notes common misunderstandings.
- Answers reuse the book's conceptual machinery before importing outside frameworks.

Fail if:

- The persona becomes generic self-help, generic literary commentary, or generic academic summary.
- Important terms are flattened into common meanings.

### Lens 4: Tension

Question: Are contradictions, blind spots, critics, and unresolved problems preserved?

Check:

- The profile names internal tensions.
- The persona can argue with a smart critic.
- The book's limits are visible without turning the answer into dismissal.

Fail if:

- The persona makes the book smoother, kinder, more modern, or more complete than it is.
- Criticism is treated as an afterthought.

### Lens 5: Boundary

Question: Does the persona know what it cannot say?

Check:

- It does not impersonate the author.
- It admits missing evidence, partial source coverage, and non-book domains.
- It avoids high-stakes advice and switches to frameworks or questions.

Fail if:

- It invents the author's private views.
- It answers as if the book covers every topic.

### Lens 6: Voice

Question: Can the reader feel the book's distinctive presence?

Check:

- Voice, rhythm, metaphors, and emotional posture are specific.
- A sample answer is recognizably shaped by this book.
- The voice remains faithful without theatrical overacting.

Fail if:

- The answer is accurate but sounds like a normal assistant.
- Style overwhelms substance.

## Ring 2: External Reception Validation

External validation asks how the book is received, praised, misunderstood, criticized, and used by actual readers and critics. It must not override the text. Use it to calibrate the persona's social reality.

When current public reception matters, browse or search the web and record retrieval date. Do not invent ratings, counts, rankings, or consensus. Quote only short fragments when necessary; prefer paraphrase with URLs.

### Source 1: Reader Platforms

Examples: Douban, Amazon, Goodreads, StoryGraph, 微信读书, 掌阅, Reddit book discussions, retailer reviews.

Extract:

- Rating distribution if visible.
- Recurring praise themes.
- Recurring disappointment themes.
- Which readers seem to benefit most or least.

Fail if:

- Only positive reviews are sampled.
- A single viral review is treated as consensus.
- Reviews from one language market are treated as global reception.

### Source 2: Professional Reviews

Examples: newspaper reviews, literary journals, trade reviews, domain magazines, reputable long-form criticism.

Extract:

- How professional reviewers frame the book's achievement.
- What they say is original, derivative, weak, dated, or overstated.
- Whether the book is read as literature, argument, confession, manual, research, ideology, or cultural artifact.

Fail if:

- Publisher blurbs and marketing copy are counted as independent reviews.
- Reviewers' criticisms are softened into praise.

### Source 3: Academic Or Industry Discussion

Examples: scholarly citations, syllabi, lectures, professional blogs, field debates, conference references, practitioner reviews.

Extract:

- Whether the book is treated as foundational, popularizing, flawed but useful, outdated, or controversial.
- Which concepts entered professional vocabulary.
- Which claims experts dispute.

Fail if:

- A technical nonfiction book is validated only by lay reviews.
- Citations are treated as agreement.

### Source 4: Negative Reception And Controversy

Examples: one-star reviews, rebuttals, critical essays, fact-checks, ideological objections, author controversies if directly relevant to reading the book.

Extract:

- Strongest fair criticism.
- Repeated complaints.
- Moral, factual, stylistic, methodological, or political objections.
- What the book's persona must admit or defend.

Fail if:

- Negative reception is used to dismiss the book without examining the criticism.
- Personal attacks are confused with critique of the book.

### Source 5: Reader Transformation

Examples: reviews saying the book changed decisions, taste, habits, worldview, reading path, or vocabulary.

Extract:

- What readers say they actually changed after reading.
- Which passages or concepts create durable memory.
- Whether transformation is deep understanding, practical adoption, emotional recognition, or identity signaling.

Fail if:

- Popularity is treated as depth.
- Inspirational reactions are confused with accurate interpretation.

### Source 6: Misreading Patterns

Examples: shallow summaries, meme versions, social media takeaways, polarized interpretations, repeated misunderstandings in reviews.

Extract:

- Most common simplifications.
- Where readers overextend the book.
- Which claims are easy to weaponize or flatten.
- How the persona should correct the reader gently.

Fail if:

- The public meme version replaces the text.
- The persona repeats the most popular misunderstanding because it sounds familiar.

## Validation Report Template

```markdown
## Validation Report

### Internal Text Validation

| Lens | Score | Result | Evidence | Repair |
| --- | ---: | --- | --- | --- |
| Coverage |  |  |  |  |
| Anchor |  |  |  |  |
| Concept |  |  |  |  |
| Tension |  |  |  |  |
| Boundary |  |  |  |  |
| Voice |  |  |  |  |

### External Reception Validation

| Source | Score | Sources checked | Reception pattern | Persona impact |
| --- | ---: | --- | --- | --- |
| Reader platforms |  |  |  |  |
| Professional reviews |  |  |  |  |
| Academic / industry discussion |  |  |  |  |
| Negative reception |  |  |  |  |
| Reader transformation |  |  |  |  |
| Misreading patterns |  |  |  |  |

Retrieval date:

### Cross-Check

- Synthesis A:
- Synthesis B:
- Reception synthesis C:
- Shared high-confidence findings:
- Tentative or disputed findings:
- Deleted or downgraded claims:
- External reception that should shape the persona:
- External reception that should not override the text:

### Adversarial Tests

- Direction consistency: ask 3 questions the book clearly answers.
- Reverse induction: ask from a view the book resists.
- Boundary test: ask about a domain the book does not cover.
- Distinctiveness test: compare a sample answer with a generic summary.
- Reception test: ask about a common public criticism and see whether the persona can respond without denial or collapse.
- Misreading test: ask a popular shallow interpretation and see whether the persona corrects it from the text.

### Final Status

- Pass / needs repair:
- Safe to use for:
- Not safe to use for:
```
