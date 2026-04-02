# Deslop

A Claude Code skill that rewrites AI-generated text to sound like a person wrote it. Works on blog posts, emails, docs, marketing copy, and anything else where AI tells are showing.

You know the voice: "This serves as an enduring testament to the transformative potential of..." — deslop catches that and rewrites it as something a human would actually say.

## How it works

Seven steps, in order:

1. **Voice calibration** — If you provide a writing sample, it matches your voice: your sentence patterns, word choices, punctuation habits. Without a sample, it defaults to direct and varied prose.

2. **Format detection** — A blog post needs different treatment than an internal email. The skill identifies the format and flags what to preserve (SEO keywords in headings, the core ask in an email, data tables, FAQ structure).

3. **Intensity assessment** — Reads the text once. Classifies it as light, moderate, or heavy touch. A well-written email with minor filler gets trimmed, not restructured. Raw AI output gets a structural rewrite. This prevents overcorrection.

4. **Pattern detection** — 8 rules applied against a catalog of AI writing patterns. Filler phrases, formulaic structures, passive voice, vague claims, narrator-from-a-distance voice, metronomic rhythm, hand-holding, bumper-sticker conclusions. Each rule has trigger words and before/after examples.

5. **Self-audit** — "What still sounds like AI wrote this?" Fix what the rules missed. Audit depth scales with touch level.

6. **Scoring** — 6 dimensions (directness, rhythm, trust, authenticity, density, voice). Below threshold, revise.

7. **Delivery** — Final version with a brief change summary.

## What it catches

Significance inflation ("testament," "pivotal," "groundbreaking"). Promotional language ("nestled," "vibrant," "breathtaking"). AI vocabulary ("delve," "interplay," "tapestry," "landscape"). Formulaic structures (rule of three, negative parallelisms, false ranges). Copula avoidance ("serves as" instead of "is"). Superficial -ing phrases ("highlighting," "underscoring," "showcasing"). Sycophantic artifacts ("Great question!", "I hope this helps!"). Em dash overuse. Bolded-header lists. Title case headings. Generic conclusions ("The future looks bright"). Throat-clearing ("One thing I wanted to flag," "The reason I ask").

## Installation

### Claude Code

```bash
claude install-skill github:AHorihuela/deslop
```

### Manual

Copy `SKILL.md` into your Claude Code skills directory.

## Usage

```
/deslop [paste or reference your text]
```

Or provide a file path:

```
/deslop — rewrite the blog post in src/content/my-post.md
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

This skill merges and improves on two existing projects:

- [Stop Slop](https://github.com/hardikpandya/stop-slop) by Hardik Pandya — concise 8-rule framework with a scoring rubric
- [Humanizer](https://github.com/blader/humanizer) by Blader — comprehensive 29-pattern catalog based on Wikipedia's "Signs of AI writing"

Deslop takes Stop Slop's rule structure and scoring, backs each rule with Humanizer's pattern catalog and examples, and adds voice calibration, format-aware preservation, intensity assessment, and a self-audit loop.

## License

MIT
