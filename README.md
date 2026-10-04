# Deslop

A Claude Code skill that rewrites AI-generated text to sound like a person wrote it, or audits a draft and tells you exactly which AI patterns it found. Works on blog posts, emails, docs, marketing copy, and anything else where AI tells are showing.

You know the voice: "This serves as an enduring testament to the transformative potential of..." Deslop catches that and rewrites it as something a human would actually say.

## How it works

One rule comes before everything else: **it doesn't make things up.** Every claim, stat, example, and opinion in the rewrite comes from your draft or from you. If a claim needs a source ("studies show") or a vague sentence has nothing concrete behind it, the skill cuts it or flags it for you instead of inventing a plausible-sounding detail.

Then, in order:

1. **Input check.** If there's no draft, or it can't tell who the piece is for or what the point is, it asks one question before starting.

2. **Voice calibration.** If you provide a writing sample, it matches your voice: your sentence patterns, word choices, punctuation habits. It keeps the hedges, humor, and bluntness that sound like you. Without a sample, it uses the draft itself as the reference.

3. **Format detection.** A blog post needs different treatment than an internal email. The skill identifies the format and flags what to preserve (SEO keywords in headings, the core ask in an email, data tables, FAQ structure).

4. **Intensity assessment.** Reads the text once, then classifies it as light, moderate, or heavy touch. A well-written email with minor filler gets trimmed, not restructured. Raw AI output gets a structural rewrite. Strong human sentences are left alone either way.

5. **Pattern detection.** 8 rules applied against a catalog of AI writing patterns: filler phrases, formulaic structures, passive voice, vague claims, narrator-from-a-distance voice, metronomic rhythm, hand-holding, bumper-sticker endings. Each rule has trigger words and before/after examples.

6. **Self-audit.** "What still sounds like AI wrote this?" Fix what the rules missed. Audit depth scales with touch level.

7. **Checklist.** 15 pass/fail checks covering fidelity, voice, patterns, and form. Any failure gets fixed before delivery. (This replaced the 1-10 self-score, which models tend to grade generously.)

8. **Delivery.** Final version, a brief change summary, and a short list of anything flagged for you (missing sources, gaps worth filling with a real detail).

### Detect mode

Ask "is this slop?" or "does this sound like AI?" and it audits instead of rewriting. You get each pattern it found, the quoted line, and a short fix. It doesn't score the draft or guess whether AI wrote it, since humans write "delve" too. Named patterns are evidence you can check yourself.

## What it catches

It catches two registers. The formal/promotional voice: significance inflation ("testament," "pivotal," "groundbreaking"), promotional language ("nestled," "vibrant," "breathtaking"), AI vocabulary ("delve," "interplay," "tapestry," "landscape"), copula avoidance ("serves as" instead of "is"), superficial -ing phrases ("highlighting," "underscoring," "showcasing"), generic conclusions ("The future looks bright").

And the casual thought-leader voice: business jargon ("circle back," "double down," "lean into"), faux-insight setups ("What nobody tells you," "The part everyone misses"), colon reveals ("The best part: it learns."), rhetorical setups ("What if I told you...", "The result? Faster deploys."), meta-commentary that narrates the piece ("Let me walk you through," "Plot twist," "That last part matters more than it sounds"), dramatic fragmentation ("It works. Every time. No config."), emphasis crutches ("Let that sink in," "Make no mistake"), filler adverbs ("just," "literally," "honestly"), casual throat-clearing ("Here's the thing," "The truth is").

Plus the patterns common to both: formulaic structures (rule of three, negative parallelisms, "Not a X. Not a Y. A Z."), fake-profound kickers ("The future isn't coming. It's already here."), which it deletes rather than rewrites, summary-recap endings ("In conclusion," "Ultimately"), sycophantic artifacts ("Great question!", "I hope this helps!"), em dash overuse, and formatting slop (emoji headings, decorative bold, bullets that should be prose, title case headings).

It also uses a **portability test**: if a sentence could be moved unchanged into a piece about a different company or product, it's filler.

## Installation

### Plugin marketplace (recommended, auto-updates)

```
/plugin marketplace add AHorihuela/deslop
/plugin install deslop@deslop
```

### Manual

Copy `SKILL.md` into `~/.claude/skills/deslop/SKILL.md`.

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

This skill merges and improves on three existing projects:

- [Stop Slop](https://github.com/hardikpandya/stop-slop) by Hardik Pandya: a concise 8-rule framework with a scoring rubric
- [Humanizer](https://github.com/blader/humanizer) by Blader: a 29-pattern catalog based on Wikipedia's "Signs of AI writing"
- [No AI Slop](https://github.com/petergyang/no-ai-slop) by Peter Yang: the no-invention rule, detect mode, the portability test, a pass/fail eval, and patterns like faux-insight setups and colon reveals

Deslop takes Stop Slop's rule structure, backs each rule with Humanizer's pattern catalog and examples, borrows No AI Slop's fidelity rules and checklist, and adds voice calibration, format-aware preservation, intensity assessment, and a self-audit loop.

## License

MIT
