# Domino Slides

A Claude Code skill for creating stunning, animation-rich HTML presentation slides — from scratch or by converting PowerPoint files.

## What It Does

**Domino Slides** turns your ideas into polished, self-contained HTML presentations without requiring any design or frontend skills. Instead of asking you to describe your aesthetic in words, it generates visual style previews and lets you pick what resonates — show, don't tell.

### Key Features

- **Zero Dependencies** — Single HTML files with inline CSS/JS. No npm, no build tools, no frameworks.
- **Visual Style Discovery** — Can't articulate design preferences? Pick from generated visual previews instead.
- **PowerPoint Conversion** — Convert existing `.pptx` files to web presentations, preserving images and content.
- **Domino Brand Presets** — 9 on-brand style presets following Domino Brand Guidelines.
- **Production Quality** — Accessible, responsive, viewport-fitted slides with keyboard, touch, and scroll navigation.

## Installation

### For Claude Code Users

Copy the skill files to your Claude Code skills directory:

```bash
# Create the skill directory
mkdir -p ~/.claude/skills/domino-slides

# Copy the files
cp SKILL.md ~/.claude/skills/domino-slides/
cp STYLE_PRESETS.md ~/.claude/skills/domino-slides/
cp domino-logo.png ~/.claude/skills/domino-slides/
```

Then invoke it by typing `/domino-slides` in Claude Code.

### Manual Download

1. Download `SKILL.md`, `STYLE_PRESETS.md`, and `domino-logo.png` from this repo
2. Place them in `~/.claude/skills/domino-slides/`
3. Restart Claude Code

## Usage

### Create a New Presentation

```
/domino-slides

> "Create a presentation on best practices for deploying models in Domino"
```

Domino Slides will:
1. Ask about your content (slides, key messages, images)
2. Ask about the feeling you want (impressed? excited? calm?)
3. Generate 3 visual style previews for you to compare
4. Build the full presentation in your chosen style
5. Open it in your browser

### Convert a PowerPoint

```
/domino-slides

> "Convert my presentation.pptx to a web slideshow"
```

Domino Slides will:
1. Extract all text, images, and notes from your `.pptx`
2. Show the extracted content for confirmation
3. Let you pick a visual style
4. Generate an HTML presentation with all your original assets

## Style Presets

All presets follow the Domino Brand Guidelines — approved colors, New Grotesk typography, and design patterns.

### Dark Themes

| Preset | Vibe | Best For |
|--------|------|----------|
| Domino Dark Hero | Bold, modern, high-impact | Keynotes, pitch decks |
| Domino Dark Minimal | Clean, confident, sophisticated | Technical, data-heavy |
| Domino Dark Gradient Accent | Premium, energetic, forward-looking | Product launches, keynotes |

### Light Themes

| Preset | Vibe | Best For |
|--------|------|----------|
| Domino Light Corporate | Professional, clean, trustworthy | Standard corporate |
| Domino Purple | Approachable, creative, distinctive | Thought leadership, community |
| Domino Blue | Calm, trustworthy, technical | Product, engineering |
| Domino Light Grey | Understated, corporate, structured | Internal, executive |

### Specialty

| Preset | Vibe | Best For |
|--------|------|----------|
| Domino Platform | Clean, functional, data-forward | Product demos, platform UI |
| Domino Data Viz | Analytical, precise, data-rich | Reports, analytics |

## Output

Each presentation is a single, self-contained HTML file with:

- Domino logo in the bottom-left corner of every slide
- PDF and PPT download buttons in the top-right corner
- Keyboard navigation (arrow keys, space)
- Touch/swipe support
- Mouse wheel scrolling
- Progress bar and navigation dots
- Scroll-triggered animations
- Responsive design (desktop, tablet, mobile)
- Viewport-fitted slides — no scrolling within slides, ever
- Reduced motion support for accessibility

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Main skill instructions for Claude Code |
| `STYLE_PRESETS.md` | Reference file with 9 Domino-branded style presets |
| `domino-logo.png` | Domino logo displayed in the bottom-left corner of every slide |

## Requirements

- [Claude Code](https://claude.ai/claude-code) CLI
- For PPT conversion: Python with `python-pptx` library

## Adapted From

[frontend-slides](https://github.com/zarazhangrui/frontend-slides) by [@zarazhangrui](https://github.com/zarazhangrui)

## License

MIT
