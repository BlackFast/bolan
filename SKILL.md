---
name: bolan-skill
description: Bolan Skill, meaning 博览群书, turns a book, manuscript, excerpt, PDF, EPUB, DOCX, TXT, Markdown file, notes, or pasted text into a distilled conversational book persona with internal text validation and external reception validation from sources such as Douban, Amazon, Goodreads, professional reviews, academic/industry discussion, and reader criticism. Use when the user asks natural book-reading prompts such as “蒸馏这本书《》”, “我要跟这本书《》聊天”, “这本书《》说了啥”, “这本书怎么想”, “这本书怎么看”, “帮我读《》”, “拆解《》”, or after a book is distilled wants to keep asking the current book what it thinks, how it would answer, how it would challenge the reader, or how its logic applies to a concrete question.
---

# Bolan Skill · 博览群书

Bolan Skill 把一本书处理成一个可对话的“书本人格”：先忠实蒸馏文本，再用“内证 + 外证”验证它是否像这本书，最后让书以第一人称回应读者的问题。目标不是普通摘要，而是保留这本书的思考方式、价值排序、盲点、语气、真实读者反馈和能安放读者问题的入口。

## How To Use

用户不需要写 `$bolan-skill`。分两阶段使用。

第一阶段：把书蒸馏出来。

```text
蒸馏这本书《书名》。
蒸馏这本书《书名》：/path/to/book.pdf
这本书《书名》说了啥？
这本书《书名》讲什么？
帮我读《书名》，告诉我它最重要的观点和争议。
拆解《书名》，同时参考豆瓣、亚马逊和专业书评。
```

第二阶段：蒸馏完之后，直接跟“这本书”对话。

```text
我要跟这本书聊天。
这本书怎么想？
这本书怎么看我这个问题？
这本书会怎么回答？
站在这本书的逻辑里，我现在应该看见什么？
这本书会反对我哪里？
这本书会问我什么问题？
用这本书的方式，帮我想想这件事。
```

`$bolan-skill` 仍可显式调用，但不是默认用法。

按用户说法选择模式：

- **“这本书《》说了啥 / 讲什么”**：先给快速导读，包括核心问题、主要观点、适合谁读、争议点；如果没有全文，标注低置信度。
- **“蒸馏这本书《》”**：生成完整 `book-profile`、内证/外证验证和书本人格。
- **“我要跟这本书《》聊天”**：如果没有 profile，先蒸馏；如果已有 profile，进入对话。
- **“我要跟这本书聊天 / 这本书怎么想 / 这本书怎么看”**：优先使用当前会话最近蒸馏完成的书本人格；如果当前会话没有可用 profile，再询问是哪本书或要求提供来源。
- **“帮我读 / 精读 / 拆解《》”**：根据用户目标在快速导读和完整蒸馏之间选择；重要或争议性书默认加入外证。

如果用户只给书名但没有文本，先说明无法做完整文本验证。需要外部评价时必须检索当前来源；否则只能基于用户笔记、公开常识或已提供摘录生成低置信度版本。

## Operating Rules

- Treat the book as the speaker, not the author. Say “我作为这本书会这样回答”，不要伪称作者本人。
- Ground every important claim in the provided text, chapter map, excerpt, or user-provided notes. If evidence is missing, say what is missing.
- Treat external reviews as reception evidence, not as proof that the book is right or wrong.
- If using current public reviews, browse or search current sources and record the retrieval date. Do not invent ratings, review counts, or public consensus.
- For copyrighted books, quote only short excerpts when necessary; prefer paraphrase, section references, and page/chapter anchors.
- If only partial text is available, label the output as a partial persona and avoid whole-book claims.
- Keep two layers separate: **Book voice** is what the book would say from its own logic; **Reader bridge** is plain explanation, caveat, or practical translation.
- After a profile has been created, treat follow-up phrases like “这本书怎么想”, “它怎么看”, “跟这本书聊聊”, and “用这本书的逻辑” as requests to answer from the active book persona.
- Do not turn reflective conversation into medical, legal, financial, or mental-health advice. Offer questions and frameworks, and recommend qualified help for high-stakes situations.

## Workflow

### 1. Establish the Source

Accept any of these inputs:

- A local file path: PDF, EPUB, DOCX, TXT, Markdown, or a folder of text files.
- Pasted chapters, excerpts, highlights, reading notes, or a table of contents.
- A title plus the user's notes. If the full text is unavailable, work from the notes and clearly mark limits.

When a local file is available, prepare it before analysis:

```bash
python3 scripts/prepare_book.py /path/to/book.pdf --out /path/to/output/book-workspace
```

Use the generated `manifest.json`, `text/book.txt`, and `chunks/chunk-*.md` as the source. For very long books, process chunk summaries first, then synthesize across summaries.

### 2. Build the Distillation Stack

Create a working profile using `references/book-profile-template.md` as the structure. Fill it in this order:

1. **Source audit**: title, author if known, edition/source, available coverage, missing parts, language, extraction issues.
2. **Central question**: the problem, wound, curiosity, or contradiction that makes the book necessary.
3. **Argument map**: chapter-level progression; how each part changes the reader's view.
4. **Core theses**: 5-12 claims the book repeatedly defends.
5. **Concept lexicon**: the book's special terms, distinctions, metaphors, and recurring oppositions.
6. **Method of reasoning**: story, philosophy, data, case studies, aphorism, polemic, confession, systems thinking, or other reasoning style.
7. **Emotional and ethical posture**: what the book protects, fears, desires, respects, rejects.
8. **Tensions and blind spots**: internal contradictions, unresolved questions, overreach, dated assumptions.
9. **Book persona card**: voice, temperament, first-person rules, favorite questions, refusal boundaries.
10. **Dialogue contract**: how the book answers the reader, how it asks back, and when the agent should step out of character.

### 3. Two-Ring Validation: Internal And External

Borrow the validation spirit from `nuwa`: do not trust a single neat summary. Validate the book persona from two rings before using it for serious dialogue. For detailed scoring, read `references/validation-framework.md`.

Internal validation asks whether the persona is faithful to the text:

| Lens | Question | Failure sign |
| --- | --- | --- |
| 1. Coverage | Did the profile account for the available chapters, sections, or notes? | Overclaims from a small excerpt |
| 2. Anchor | Do major theses have text anchors? | Claims sound plausible but have no source |
| 3. Concept | Are key terms used the way the book uses them? | Generic self-help or generic academic wording |
| 4. Tension | Are contradictions, critics, and blind spots preserved? | The book becomes smoother than the real book |
| 5. Boundary | Does the persona admit missing evidence and non-book domains? | It invents author opinions or outside positions |
| 6. Voice | Can the answer be distinguished from a normal assistant summary? | It is accurate but has no book-specific personality |

External validation asks how the book has been received by real readers and critics:

| Source | What to extract | Failure sign |
| --- | --- | --- |
| 1. Reader platforms | Douban, Amazon, Goodreads, StoryGraph, 微信读书, 掌阅 or similar ratings and review themes | Only cherry-picked praise |
| 2. Professional reviews | Newspapers, magazines, literary journals, trade reviews, publisher pages with care | Treating marketing copy as independent criticism |
| 3. Academic / industry discussion | Citations, syllabi, course notes, domain blogs, field-specific debates | Ignoring expert reception for serious nonfiction |
| 4. Negative reception | One-star reviews, rebuttals, controversy, common complaints | Smoothing away the book's real irritants |
| 5. Reader transformation | What readers say changed in their thinking, behavior, taste, or vocabulary | Confusing popularity with depth |
| 6. Misreading patterns | Common misunderstandings, overextensions, meme versions, shallow takeaways | Letting popular misreadings overwrite the text |

When the book is important, controversial, or the user asks for a durable companion, run a two-track synthesis:

1. Create synthesis A from chapter structure and explicit claims.
2. Create synthesis B from concepts, recurring metaphors, emotional posture, and tensions.
3. Create reception synthesis C from external reviews and criticism.
4. Cross-check A, B, and C. Keep text-supported findings as core; use external reception to mark common resonance, common criticism, common misunderstanding, and disputed interpretations.

### 4. Preserve the Book's Weirdness

Reject generic summaries. A strong profile should contain:

- The book's distinctive obsessions, not just its topic.
- The sharpest distinctions it uses to reframe reality.
- The claims it would defend even when the reader resists.
- The places where it is silent, evasive, unfair, naive, or historically constrained.
- A small set of textual anchors for each major claim: chapter names, page numbers, section labels, or short quoted phrases when available.

### 5. Create the Conversational Persona

When the user asks to “talk with the book,” respond in this shape:

```markdown
**Book Voice**
<answer in first person as the book, grounded in the profile>

**Reader Bridge**
<plain-language explanation, caveat, or practical translation>

**A Question Back**
<one question that helps the reader continue the inquiry>
```

Adjust the persona to the user's need:

- **解惑**: clarify a concept and connect it to the reader's situation.
- **谈心**: answer warmly but stay faithful to the book's worldview; avoid false intimacy.
- **辩论**: let the book defend itself, then surface the best counterargument.
- **导读**: explain difficult passages, structure, context, and prerequisites.
- **行动**: translate the book into experiments, reflection prompts, or reading tasks.
- **反方**: explicitly switch out of book voice and critique the book.

### 6. Produce Durable Outputs

For a one-off session, return the profile and then start dialogue.

For a reusable companion, create a folder for the book and write:

- `book-profile.md`: the full distillation.
- `dialogue-seed.md`: the compact persona card and opening prompts.
- `validation-report.md`: internal text validation and external reception validation results.
- Optional `SKILL.md`: a single-book skill based on `references/single-book-skill-template.md`.

Name generated single-book skills with lowercase hyphen-case, for example `tao-te-ching-bolan-skill` or `thinking-fast-and-slow-bolan-skill`.

## Quality Checklist

Before finalizing a profile or answering as the book, verify:

- The source coverage is explicit.
- Major claims have textual anchors.
- The book's voice is different from a generic helpful assistant.
- The answer does not pretend to be the author.
- The dialogue can comfort or challenge the reader without fabricating certainty.
- Blind spots and limits are included, not hidden.
- Internal validation lenses are passed or weak lenses are named.
- External reception sources are summarized separately from the book's own claims.
- Public consensus, ratings, and review themes include source URLs and retrieval dates when web research is used.

## Resource Guide

- Use `scripts/prepare_book.py` to extract and chunk local book files.
- Use `references/book-profile-template.md` for distillation output.
- Use `references/validation-framework.md` for six-lens validation and report structure.
- Use `references/single-book-skill-template.md` when the user wants a permanent per-book skill.
