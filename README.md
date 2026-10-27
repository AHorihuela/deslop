# Deslop

A Claude Code skill that rewrites AI-generated text to sound like a person wrote it, or audits a draft and tells you exactly which AI patterns it found. Works on blog posts, emails, docs, marketing copy, and anything else where AI tells are showing.

You know the voice: "This serves as an enduring testament to the transformative potential of..." Deslop catches that and rewrites it as something a human would actually say.

## How it works

One rule comes before everything else: **it doesn't make things up.** Every claim, stat, example, and opinion comes from your draft or designated content sources. Writing samples guide the voice. The skill cuts empty appraisal and flags missing sources for concrete claims while preserving facts, uncertainty, and prerequisites.

Then, in order:

1. **Input check.** If there's no draft, or it can't tell who the piece is for or what the point is, it asks one question before starting.

2. **Voice calibration.** If you provide a writing sample, it matches your voice: your sentence patterns, word choices, punctuation habits. It keeps the hedges, humor, and bluntness that sound like you. Without a sample, it uses the draft itself as the reference.

3. **Format detection.** A blog post needs different treatment than an internal email. The skill identifies the format and flags what to preserve (SEO keywords in headings, the core ask in an email, data tables, FAQ structure).

4. **Intensity assessment.** Reads the text once, then classifies it as light, moderate, or heavy touch. A well-written email with minor filler gets trimmed, not restructured. Raw AI output gets a structural rewrite. Strong human sentences are left alone either way.

5. **Pattern detection.** 8 rules applied against a catalog of AI writing patterns: filler phrases, formulaic structures, passive voice, vague claims, narrator-from-a-distance voice, metronomic rhythm, hand-holding, bumper-sticker endings. Each rule has trigger words and before/after examples.

6. **Self-audit.** Check for specific problems in clarity, repetition, and voice. Fix only problems the editor can identify. No change is a valid result.

7. **Checklist.** 16 checks covering fidelity, voice, patterns, and form. They guide the edit without assigning a quality or authorship score.

8. **Delivery.** Final version, a change note when useful, and unresolved questions when needed. Requests for a single edit or rewrite only take precedence.

### Detect mode

Ask "is this slop?" or "does this sound like AI?" and it audits instead of rewriting. You get each pattern it found, the quoted line, and a short fix. It doesn't score the draft or guess whether AI wrote it, since humans write "delve" too. Named patterns are evidence you can check yourself.

## What it catches

It catches two registers. The formal/promotional voice: significance inflation ("testament," "pivotal," "groundbreaking"), promotional language ("nestled," "vibrant," "breathtaking"), AI vocabulary ("delve," "interplay," "tapestry," "landscape"), copula avoidance ("serves as" instead of "is"), superficial -ing phrases ("highlighting," "underscoring," "showcasing"), generic conclusions ("The future looks bright").

And the casual thought-leader voice: business jargon ("circle back," "double down," "lean into"), faux-insight setups ("What nobody tells you," "The part everyone misses"), colon reveals ("The best part: it learns."), rhetorical setups ("What if I told you...", "The result? Faster deploys."), meta-commentary that narrates the piece ("Let me walk you through," "Plot twist," "That last part matters more than it sounds"), dramatic fragmentation ("It works. Every time. No config."), emphasis crutches ("Let that sink in," "Make no mistake"), filler adverbs ("just," "literally," "honestly"), casual throat-clearing ("Here's the thing," "The truth is").

Plus the patterns common to both: formulaic structures (rule of three, negative parallelisms, "Not a X. Not a Y. A Z."), fake-profound kickers ("The future isn't coming. It's already here."), which it deletes rather than rewrites, summary-recap endings ("In conclusion," "Ultimately"), sycophantic artifacts ("Great question!", "I hope this helps!"), em dash overuse, and formatting slop (emoji headings, decorative bold, bullets that should be prose, title case headings).

It also uses a **portability test**: a sentence that could move unchanged into an unrelated piece may be filler. Necessary instructions, meaningful facts, and personal feelings still belong. The pattern catalog supplies editing prompts, not blanket bans.

### Version 1.3.1

This patch keeps the 1.3 structure and editing approach. It corrects examples that changed facts, protects useful detail, and allows clear prose to remain unchanged. It preserves the included [writing preferences](references/writing-preferences.md), including Alberto's preference for “still need to be fixed” in work updates. An explicit brief or another target author's voice takes precedence.

[Technical English guidance](references/technical-english.md) is available for procedures and explicit ASD-STE100 requests. It does not impose controlled language on ordinary prose or establish full STE compliance.

## Installation

### Plugin marketplace (recommended, auto-updates)

```
/plugin marketplace add AHorihuela/deslop
/plugin install deslop@deslop
```

### Manual

Copy `SKILL.md` and the entire `references/` directory into `~/.claude/skills/deslop/`. Keep their relative paths intact. For another compatible agent, copy the same files into its deslop skill directory.

## Usage

```
/deslop [paste or reference your text]
```

Or provide a file path:

```
/deslop — rewrite the blog post in src/content/my-post.md
```

### Audit without rewriting

```
/deslop is this slop? [paste your text]
```

### Voice matching

Provide a writing sample and the output matches your voice, not a generic one:

```
/deslop — rewrite this draft. Use my-previous-post.md as a voice reference.
```

## Format awareness

| Format | Touch level | What it preserves |
|--------|------------|-------------------|
| Blog post | Moderate to heavy | Keywords in headings, FAQ structure, comparison tables |
| Email | Light | The core ask, data tables, recipient hierarchy |
| Technical doc | Light to moderate | Accuracy, code references, defined terms |
| Marketing copy | Moderate | Brand voice, product names, value propositions |
| Report / memo | Light to moderate | Executive summary structure, data, recommendations |

## Built from

The original framework draws on three projects:

- [Stop Slop](https://github.com/hardikpandya/stop-slop) by Hardik Pandya: a concise 8-rule framework with a scoring rubric
- [Humanizer](https://github.com/blader/humanizer) by Blader: a 29-pattern catalog based on Wikipedia's "Signs of AI writing"
- [No AI Slop](https://github.com/petergyang/no-ai-slop) by Peter Yang: the no-invention rule, detect mode, the portability test, a pass/fail eval, and patterns like faux-insight setups and colon reveals

Deslop takes Stop Slop's rule structure, backs each rule with Humanizer's pattern catalog and examples, borrows No AI Slop's fidelity rules and checklist, and adds voice calibration, format-aware preservation, intensity assessment, and a self-audit loop.

The 1.3.1 review also consulted [Avoid AI Writing](https://github.com/conorbronsdon/avoid-ai-writing), [Writing clearly and concisely](https://github.com/obra/the-elements-of-style), and [Copy Editing](https://github.com/coreyhaines31/marketingskills/blob/main/skills/copy-editing/SKILL.md). Useful guidance included contextual edits, keeping related words together, and checking clarity separately. These sources do not establish a performance advantage across models.

## License

MIT
