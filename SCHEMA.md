# AIB-C01 Study Hub content schema

Static site in `src/`, built by `node build.mjs` into `dist/`, deployed to Vercel. Content is JSON under `src/data/`.

The official exam guide is the source of truth. A copy lives in `research/`.

- `research/exam-guide-overview.txt` holds the introduction, target candidate, exam content and domain weights.
- `research/ai-business-strategist-01-domain1.md` to `domain4.md` list every task and skill.
- `research/tech.md` lists technologies and concepts that might appear.
- `research/aib-01-in-scope-services.md` and `research/aib-01-out-of-scope-services.md` list the AWS scope.

The online version is at https://docs.aws.amazon.com/aws-certification/latest/ai-business-strategist-01/ai-business-strategist-01.html

Every author must pass two checks before handing content over.

- `python3 -I validate.py <files>` prints OK.
- `node build.mjs --check <topicId>` prints 0 layout warnings when the topic has diagrams. Then open `preview/<topicId>.png` with the Read tool and look at every diagram. Fix anything cramped, tangled, or hard to read.

## Exam facts

- AIB-C01, AWS Certified AI Business Strategist, beta from 2026-09.
- The beta has 85 questions in 170 minutes for 50 USD (certification page).
- The exam guide gives 130 minutes for the standard exam and a passing score of 700 of 1000 with compensatory scoring.
- Multiple choice questions have 1 correct answer of 4. Multiple response questions have 2 or more correct answers of 5 or more.

| Domain | Name | Weight |
|---|---|---|
| D1 | AI Fundamentals and Literacy | 24% |
| D2 | AI Strategy and Business Value Creation | 28% |
| D3 | AI Governance and Responsible AI Leadership | 24% |
| D4 | Business Readiness, Leadership, and AI Transformation | 24% |

The exam tests business judgement, not AWS implementation. These AWS offerings are in scope at a strategic level only.

- Amazon Bedrock, Amazon SageMaker AI, Amazon Quick
- AWS Cloud Adoption Framework (AWS CAF) and the AWS shared responsibility model
- AI pricing structures, AWS Cost Explorer, AWS Marketplace, AWS Pricing Calculator

Every other AWS service is out of scope and must never be tested.

## Reader and writing rules

The reader is a working data engineer with SAA, DEA and SOA. They are strong on tech and weak on the business frameworks below.

- ROI and KPI design, build-buy-partner
- governance structures and regulation (EU AI Act, ISO/IEC 42001)
- change management and maturity models

Cut tech basics they already know; teach how the exam frames each idea for a business decision-maker.

- **Language.** Every title and explanation is Vietnamese, including topic summary, section title, block title, callout title, legend, caption, why and explain.
- **English terms.** AWS names, IT terms and business or AI terms stay in English inside the Vietnamese text and are never translated. Examples are "use case", "stakeholder", "governance", "compliance", "risk", "cost", "deploy", "monitoring", "fine-tuning", "hallucination", "model drift", "change management", "executive sponsor", "business case", "pilot", "workforce". The list `VI_TERMS` in `validate.py` holds the Vietnamese translations the validator rejects.
- **Titles.** A section title is a short Vietnamese phrase that carries English terms, never a full English sentence. A title made only of English terms stays as is, for example "RAG & fine-tuning".
- **Exam phrases.** The field `decision.says`, the quiz stem and options, and the card front stay English because the exam is English.
- **Bullets, not prose.** Anything with 2 or more facts is a `- ` list, one fact per line. Every non-bullet line is at most 30 words (caption 20). Use `**bold**` for the key term in a bullet.
- **No filler.** Delete UI instructions, intros, summaries and restated titles. The validator rejects UI verbs such as "click".
- **Concise.** A section holds 1 visual and at most 2 callouts. Prefer tables, compare cards and decision tables. Use diagrams only for real flows, for example a RAG flow or an agent tool loop.
- **Accurate and current.** Today is 2026-11. Verify facts with WebSearch and WebFetch against the sources listed below. Memory is a hypothesis. Mark recent changes with callout tone `new`.
- **Exam-oriented.** Tie each concept to the exam phrasing ("MOST effective first step", "BEST way to measure", "LEAST risk") and to the decisive signal in a scenario.
- No emoji, no em-dash, no arrows "->" in prose.

Authors verify facts against these sources.

- AWS docs and AWS blogs
- the AWS whitepapers AWS CAF for AI, Responsible AI Lens and Generative AI Lens
- ISO pages for ISO/IEC 42001 and ISO/IEC 23053
- the EU AI Act text on eur-lex.europa.eu or artificialintelligenceact.eu
- NIST AI RMF

Inline markdown supports `**bold**`, `*italic*`, `` `code` ``, `[label](https://...)`, `\n` and lines starting with `- `.

## Sources, accuracy and freshness

Every fact is checked, current and traceable. Memory and training data are hypotheses only.

- **Today is 2026-11-04.** Verify every framework name, date, regulation status and AWS offering against the current official source. Mark changes from 2025 to 2026 with callout tone `new`.
- **Open every link you cite** with WebFetch and confirm the page says what you cite it for. A link you did not open is never cited. For a YouTube video, confirm title and channel through `https://www.youtube.com/oembed?url=<video url>&format=json`.
- **Cross-check with several sources.** Official docs are the primary source. Add independent sources that add exam value: official blogs and release notes, conference talks and YouTube walkthroughs from the vendor or known practitioners, reputable practitioner blogs, exam-experience write-ups and community discussions (Reddit, Medium, AWS re:Post, ExamTopics discussions). Use them for exam tips, traps and what candidates report, and cross-check any technical claim they make against the docs.
- **When sources disagree**, follow the current official docs and say so in a `trap` callout when the old behavior still circulates.
- **Validator rules.** Each section cites at least 1 source. Each topic cites at least 3 distinct hosts.
- **Hand-over note.** List every claim you could not confirm in an official source, with the reason. Do not publish such a claim as fact; drop it or label it "chưa xác minh" in the text.

## Resources file `src/data/resources.json`

A curated list shown on the page "Nguồn học". Only sources you opened and checked.

```json
[{"group":"Chính thức","md":"optional 1 Vietnamese line","items":[{"label":"Exam guide","url":"https://...","kind":"official","note":"1 short Vietnamese line: what it gives the candidate","date":"2026-10"}]}]
```

- Field `kind` is one of `official`, `docs`, `course`, `practice`, `video`, `blog`, `book`, `community`, `repo`.
- Suggested groups: Chính thức; Khoá học và đề luyện; Video; Blog và kinh nghiệm thi; Cộng đồng.
- Field `date` is the publish or update date (YYYY, YYYY-MM or YYYY-MM-DD) when the page shows one. Prefer material from 2025 to 2026 that matches the current outline; label older material in `note`.

## Topic file `src/data/topics/<id>.json`

| Topic id | Scope |
|---|---|
| `fundamentals` | D1 |
| `strategy` | D2 |
| `governance` | D3 |
| `transformation` | D4 |
| `aws` | AWS offerings at strategy level, across D1 to D4 |

```json
{"id":"strategy","title":"AI Strategy & Business Value","domain":["D2"],"icon":"cost-explorer",
 "summary":"<1 or 2 sentences in Vietnamese: which question types this chapter answers>",
 "sections":[{"id":"roi","title":"<Vietnamese title>","icon":"cost-explorer","task":"2.2","blocks":[]}]}
```

The field `task` names the exam guide task the section covers, for example "2.2". Every skill of the domain must be covered by at least one section.

## Block types

All blocks accept `"src":[{"label":"...","url":"https://..."}]`.

1. `text` `{"md"}` at most 110 words; never two text blocks in a row.
2. `callout` `{"tone":"tip|trap|new|exam","title","md"}`
3. `diagram` uses auto layout and has NO coordinates.
   ```json
   {"type":"diagram","title":"...","caption":"...","dir":"RIGHT",
    "groups":[{"id":"aws","label":"AWS","kind":"cloud"}],
    "nodes":[{"id":"kb","icon":"bedrock","label":"Knowledge Base","sub":"RAG","group":"aws","info":"md shown on click"}],
    "edges":[{"id":"e1","from":"user","to":"kb","label":"question","style":"solid|dashed|double","tone":"primary|backup|deny|data"}],
    "legend":[{"style":"dashed","tone":"backup","label":"..."}],
    "steps":[{"title":"1. ...","md":"...","hl":["e1","kb"]}]}
   ```
   - A group kind is one of `cloud`, `region`, `vpc`, `subnet`, `account`, `org`, `onprem`, `ou`.
   - A diagram has at most 9 nodes and 10 edges.
   - Node labels are at most 18 chars, subs 22, edge labels 22, group labels 34.
   - Rendered width stays at most 1000 px and height at most 760 px.
   - `python3 -I validate.py --icons` lists the icons. The generic icons that fit this exam are `r-user`, `r-users`, `r-office-building`, `r-servers`, `c-artificial-intelligence`, `bedrock`, `sagemaker-ai`, `quick`, `kendra`, `textract`, `comprehend`, `lex`, `personalize`, `rekognition`, `transcribe`, `translate`, `polly`, `simple-storage-service`, `cloudwatch`, `cloudtrail`, `audit-manager`, `organizations`, `cost-explorer`, `budgets`, `savings-plans`, `well-architected-tool`, `step-functions`, `lambda` and `api-gateway`.
   - The field `legend` is required when the diagram uses 2 or more (style, tone) pairs.
4. `table` `{"title","columns":[...],"rows":[[...]]}`
5. `decision` `{"title","rows":[{"says":"exam phrase in English","pick":"...","why":"Vietnamese, max 30 words","src":{"label","url"}}]}`
6. `code` `{"title","lang":"text|json","code","notes":[{"line":3,"md":"..."}]}` fits a prompt template example.
7. `chart` `{"title","chart":"bar|hbar|line","labels","series":[{"name","data"}],"xLabel","yLabel","note"}` takes numbers from `src`; illustrative charts say so in `note`.
8. `compare` `{"title","items":[{"name","icon","tag","points":[...]}]}` holds 2 to 4 cards.
9. `steps` `{"title","items":[{"title","md"}]}`
10. `figure` shows a real image: an official architecture diagram, a docs illustration, or a UI screenshot from the official docs.
   ```json
   {"type":"figure","kind":"diagram|screenshot|docs","title":"<Vietnamese>","img":"figs/<file>.png or https://<vendor host>/<image>",
    "alt":"<what the image shows>","caption":"<Vietnamese, max 40 words: what to look at for the exam>",
    "credit":{"label":"<site>: <page title>","url":"https://<page that shows the image>","license":"CC BY 4.0","licenseUrl":"https://creativecommons.org/licenses/by/4.0/"}}
   ```
   - **Only real images.** Take the image from the official page that shows it. Never draw, generate, crop or edit an image.
   - **Copy or embed by license.** AWS docs on docs.aws.amazon.com are CC BY-SA 4.0 (https://aws.amazon.com/terms/), so download the image into `src/figs/<topic>-<name>.png` and set license "CC BY-SA 4.0" with licenseUrl https://creativecommons.org/licenses/by-sa/4.0/. That statement covers docs.aws.amazon.com only; images from other AWS pages (whitepaper PDFs, aws.amazon.com, AWS blogs) are embedded by their https url, no license field.
   - Open every image with the Read tool before using it, and confirm it shows what the caption says and matches the current product UI and naming.
   - Choose images that teach an exam point: object models, architecture overviews, UI pages that the exam names (settings, monitoring hubs, lineage views). Skip decorative images.
   - A section may hold 1 figure in addition to its 1 visual. A topic holds 3 to 8 figures.

## Quiz `src/data/quiz/<topicId>.json`

Each question is `{"id","topic","domain":"D1|D2|D3|D4","task":"2.2","source":"original","select","stem","options":[{"k","t"}],"answer":[...],"explain","wrong":{},"refs":[...]}`.

- **Stem.** The stem is English in real AIB-C01 style, a company scenario of 50 to 130 words with industry, size, goal, constraint and stakeholder concern. It ends with a question such as "Which approach should the AI strategist recommend?" or "What should the company do FIRST?". It tests business judgement, never AWS configuration.
- **Option count.** A question with `select` 1 has exactly 4 options, `select` 2 has exactly 5, `select` 3 has exactly 6. About 1 in 5 questions uses select 2.
- **Distractors.** Every option is plausible and differs in a decisive detail such as sequence, scope, stakeholder or metric type. Do not make the longest option the correct one.
- **Explain.** The field `explain` holds Vietnamese bullets with the decisive signal in the stem and why the answer meets it. The field `wrong` gives the specific flaw of each distractor in Vietnamese.
- **Refs.** The field `refs` points to the AWS doc, whitepaper, or standard page that supports the answer.
- **Style models.** Study the official sample questions, Skill Builder material, YouTube walkthroughs, blogs and community discussions to match difficulty and wording. Write every stem and option yourself.

## Cards `src/data/cards/<topicId>.json`

Each card is `{"id","front":"English exam phrase or concept","back":"English answer plus 1 Vietnamese sentence","ref":{"label","url"}}`.

## Glossary `src/data/glossary.json`

```json
{"id":"rag","term":"RAG","full":"Retrieval Augmented Generation","aliases":["retrieval augmented generation"],"cat":"GenAI",
 "what":"<1 Vietnamese sentence, max 25 words: what the concept is>",
 "means":["<2 or 3 Vietnamese bullets, max 20 words each: practical effect and what the exam asks>"],
 "related":["fine-tuning","knowledge-base"],
 "src":{"label":"...","url":"https://..."}}
```

| Value of field `cat` | Covers |
|---|---|
| AI Fundamentals | AI, ML, data, training, inference, drift |
| GenAI | prompts, tokens, RAG, fine-tuning, agents |
| Strategy & Value | use cases, ROI, KPI, build-buy-partner |
| Governance & Risk | responsible AI, governance bodies, risk controls |
| Regulation & Standards | EU AI Act, ISO/IEC, NIST AI RMF |
| Transformation | readiness, maturity, change, CoE, scaling |
| AWS | in-scope AWS offerings and frameworks |

The site underlines the first occurrence of `term` or an alias in each section, so pick aliases that appear in real text. Skip terms every data engineer knows, such as database and API.
