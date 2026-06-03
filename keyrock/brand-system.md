# Keyrock Brand System — Chart Generation Reference

> Single source of truth for all Keyrock brand rules applied to chart and data-visualisation generation.
> Keyrock is an institutional digital asset market maker.

---

## 1. Colour Palette

### 1.1 Primary Series — Blue Tones (up to 8 series)

Use these first for all standard data series. Ordered from most vibrant to darkest.

| Index | Hex | Reference |
|---|---|---|
| PRIMARY[0] | `#3867FF` | Default single-series colour (vibrant blue) |
| PRIMARY[1] | `#7696FF` | Mid-light blue |
| PRIMARY[2] | `#A9BDFF` | Soft blue |
| PRIMARY[3] | `#DEE2FF` | Pale blue |
| PRIMARY[4] | `#001FFF` | Pure blue |
| PRIMARY[5] | `#3636BB` | Deep blue-violet |
| PRIMARY[6] | `#22227E` | Navy |
| PRIMARY[7] | `#303052` | Dark slate |

### 1.2 Secondary Series — Purple (9+ series ONLY)

Extend into these **only** when a chart has more than 8 data series.

| Index | Hex | Reference |
|---|---|---|
| SECONDARY[0] | `#A580FF` | Light purple |
| SECONDARY[1] | `#592DC5` | Mid purple |
| SECONDARY[2] | `#371096` | Deep purple |

### 1.3 Accent — Orange (Highlighting ONLY)

Use **only** to highlight a specific series or data point. Never as a default data colour.

| Token | Hex | Usage |
|---|---|---|
| ACCENT_ORANGE | `#FF7800` | Primary highlight |
| ACCENT_ORANGE_LIGHT | `#FFBA7D` | Secondary / softer highlight |

### 1.4 Structural Colours

| Token | Hex | Usage |
|---|---|---|
| BG | `#FFFFFF` | Primary background |
| BG_PANEL | `#F8FAFC` | Card / panel background |
| BG_CARD | `#F1F5F9` | Elevated surface |
| TEXT_PRIMARY | `#1F1F1F` | Primary text, X-axis line |
| TEXT_MUTED | `#9B9B9B` | X and Y axis tick marks |
| GRID_COLOR | `#5F5F5F` | Horizontal gridlines |
| BORDER_COLOR | `#CBD5E1` | Borders |

### 1.5 Semantic Exceptions (Inline Only)

For contexts where directional colour is essential (waterfall charts, KPI trend indicators, scorecards), use these as **inline hex values** — they are not defined as named variables in the setup block.

| Hex | Usage |
|---|---|
| `#10B981` | Positive / success (green) |
| `#EF4444` | Negative / risk (red) |

---

## 2. Typography

### Text Specifications

| Element | Size | Weight | Colour |
|---|---|---|---|
| Title | 17px | Bold | `#1F1F1F` (TEXT_PRIMARY) |
| Subtitle | — | — | **Not used.** Keyrock charts never carry a subtitle / subheader (Amir's standing rule, 2026-06-03). Put context in the title or an in-chart annotation. |
| Axis labels | 12px | Bold | `#1F1F1F` (TEXT_PRIMARY) |
| Tick labels | 10px | Regular | `#9B9B9B` (both X and Y axis) |
| Legend | 12px | Bold | `#1F1F1F` (TEXT_PRIMARY) |
| Data labels / Annotations | 12px | Bold | Series colour, or `#FF7800` / `#3867FF` / `#A580FF` |
| Source line | 9px | Regular | `#9B9B9B` (TEXT_MUTED) |

### Font Stack

- **Primary:** FK Grotesk Neue (bundled — TTF files in `~/.claude/keyrock/assets/fonts/`)
- **Fallback chain:** Inter, Inter Tight, Helvetica Neue, Helvetica, Arial, DejaVu Sans

### Kerning

Designer spec is **-10 tracking** for all text. FK Grotesk Neue's natural metrics provide tight tracking. matplotlib does not support CSS-style letter-spacing natively — the font's built-in tracking is the best approximation. For pixel-perfect kerning, export SVG and adjust in Figma or Illustrator.

### Headline Style

Bold, punchy headlines are preferred. Keep titles concise and informative.

**Title-as-measurement rule.** A chart title must describe what is actually measured, not gesture at the topic. If the data is one slice of a broader category, the title says so — readers infer scope from the title, and a loose title will be read as a claim about the broader category.

Examples (from the Stablecoin FX project):
- ✗ "Onchain Non-USD DEX Trading" — implies all non-USD DEX activity (would include same-peg swaps and non-USD ↔ non-USD pairs)
- ✓ "Onchain Non-USD vs USD-Stablecoin DEX Volume" — specifies the pairing (Measure B: FX corridor only)
- ✗ "Stablecoin Trading Is Concentrated In The Euro" — ambiguous about which trading
- ✓ "Non-USD Stablecoin DEX Trading Is Concentrated In The Euro" — adds DEX, distinguishing from CEX layers

When the title declares a number range or trend ("Swings between $X and $Y", "Doubled since 2024"), confirm the data window matches the chart's actual x-axis. Pick declarative over descriptive only when the punchy claim is what the chart actually shows; otherwise descriptive accuracy beats forced punchiness.

---

## 3. Logo

### Files

Located in `~/.claude/keyrock/assets/`:

| File | Mode |
|---|---|
| `keyrock-logo-black.svg` | Light mode |
| `keyrock-logo-black.png` | Light mode |
| `keyrock-logo-white.svg` | Dark mode |
| `keyrock-logo-white.png` | Dark mode |

### Placement Rules

- **Do NOT add a logo.** `/keyrock-chart` never places the Keyrock logo on generated charts (Amir's standing preference, 2026-06-03). The `add_keyrock_logo()` helper is kept for manual/one-off use only — do not call it in generated charts.
- If ever explicitly requested by the user: top-right, ~8–10% of chart width, ≥10px clear space.
- Logo brand black is `#171717`

### Mode Selection

- Light mode charts: use **black** logo variant
- Dark mode charts: use **white** logo variant

---

## 4. Source Lines

- **Default text:** "Source: Keyrock Research"
- User may override with a specific source string
- **Position:** Bottom-left of the figure (`x=0.02, y=0.02, ha='left'`)
- **Format:** 9px, Regular, `#9B9B9B` (TEXT_MUTED)
- Encouraged by default; user can request omission

---

## 5. Number Formatting

| Scale | Format | Example |
|---|---|---|
| Trillions | `$X.XT` | $1.5T |
| Billions | `$X.XB` | $1.2B |
| Millions | `$X.XM` or `$XXXM` | $340M |
| Full numbers | Comma-separated thousands | $1,250,000 |

- **One decimal maximum** for abbreviated numbers
- Always prefix financial data with `$` (USD assumed unless stated)

---

## 6. Design Direction

### Do

- Institutional, clean, modern, understated
- Credible, polished, brand-consistent
- Balanced whitespace
- Subtle gridlines (low alpha)
- Branded but not loud

### Do Not

- Flashy or decorative
- Generic startup / SaaS aesthetic
- Overly busy annotations or ornaments
- Loud colour usage without purpose

---

## 7. Chart Colour Assignment Rules

Colours are assigned in this strict priority order:

1. **Primary blues first** — use `CHART_COLORS` (8 blue tones) for all standard data series
2. **Secondary purples only for 9+ series** — extend into `CHART_COLORS_EXTENDED` when more than 8 categories
3. **Accent orange for highlighting only** — use `ACCENT_ORANGE` to draw attention to a specific data point or series, never as a default data colour
4. **Single-series default:** `PRIMARY_DEFAULT` (`#3867FF`)
5. **Semantic exceptions:** For waterfall positive/negative, KPI trends, and scorecard status, use inline green (`#10B981`) and red (`#EF4444`) — see section 1.5
6. **Diverging colormaps:** Red (`#EF4444`) through white to `PRIMARY[0]` (`#3867FF`)
7. **Never** use background or text colours for data series

---

## 8. Layout Rules

### Spacing Philosophy

Charts should breathe. Every element (title, chart area, source, logo) needs clear separation. **There is no subtitle.** `layout_chart()` (§16) places everything in inch-based, scale-invariant positions — do not hand-place title/source in figure fractions.

### Layout Zones (figure-relative, indicative — `layout_chart` computes exact positions in inches)

| Zone | Y range | Contents |
|---|---|---|
| Title block | 0.93–0.97 | Title (centred, 17pt bold) |
| Legend band (only if a legend) | ~0.87–0.91 | Single frameless legend row under the title |
| Chart area | 0.10–0.90 (0.85 with legend) | Axes, gridlines, data |
| Source | 0.00–0.08 | Source line (bottom-left). No logo. |

### Key Spacing Values

Handled entirely by `layout_chart()` (§16) — title 0.40" from top, optional legend row beneath, source bottom-left, axes pinned with `fig.subplots_adjust`. Do not reproduce these by hand.

### Legend

- 10.5px, regular-bold
- Marker style by chart type: **`Patch` rectangles** for bar / stacked-bar / area charts (the series are filled shapes); **circle markers** (`Line2D([0],[0], marker='o', color='w', markerfacecolor=col, markersize=10, label=r)`) for scatter and line charts where each row maps to a point/line.
- **Let `layout_chart()` place the legend.** Pass your handles as `legend_handles=` (and `legend_ncol=` if you want a specific column count) and the helper drops a single frameless legend row into the band directly beneath the title, with the chart top lowered to make room. This is the only supported way to get a top-of-chart legend.

**Correct pattern:**
```python
from matplotlib.patches import Patch
handles = [Patch(facecolor=COL_A, label='Series A'),
           Patch(facecolor=COL_B, label='Series B')]
layout_chart(fig, 'My Title', legend_handles=handles)   # legend placed for you
```

**Anti-patterns:**
```python
# DO NOT place the legend yourself with a hand-tuned figure-coord anchor —
# the old legend_y = 1.0 - 1.05/H + top_extra_inches recipe drifted and left
# gaps. Pass legend_handles to layout_chart instead.
fig.legend(..., bbox_to_anchor=(0.5, 1.0 - 1.05/H))   # removed 2026-06-03

# DO NOT anchor in axes coords just above the box — leaves a gap under the title.
ax.legend(loc='lower center', bbox_to_anchor=(0.5, 1.02), ...)
```

### Aspect Ratios (Context-Adaptive)

| Context | Dimensions | Ratio |
|---|---|---|
| PDF report full-width | ~1200 x 700 | ~1.7:1 (landscape) |
| PDF report half-width | ~600 x 450 | ~1.33:1 (slightly taller) |
| Slide | ~1920 x 1080 | 16:9 |
| Social / web | ~1200 x 630 | ~2:1 |
| Square (social) | 1080 x 1080 | 1:1 |

---

## 9. Axis Rules

### Spines

- **Top spine:** Hidden
- **Right spine:** Hidden
- **Bottom spine (X-axis):** Visible, **2px** width, colour `#1F1F1F`
- **Left spine (Y-axis):** Hidden — no Y-axis line

### Tick Marks

- **Y-axis ticks:** 1px width, colour `#9B9B9B` — horizontal gridlines at tick positions extend the full chart width, serving as visual reference lines in place of the Y-axis spine
- **X-axis ticks:** 1px width, colour `#9B9B9B`
- **Placement:** Ticks on main data points only

### Gridlines

- **Horizontal gridlines** span the full chart width at Y-axis tick positions
- Alpha: 0.3, linewidth: 0.5
- No vertical gridlines by default

---

## 10. Annotation Rules

- Use annotations **only when they add clarity** — do not over-annotate
- If legend and axis labels communicate the message, annotations may not be needed

### Style Guidelines

| Element | Rule |
|---|---|
| Annotation colour | Match the annotated data series, or use `#FF7800` / `#3867FF` / `#A580FF` |
| Font size | 12px, Bold |
| Leader lines | Thin (1–1.5px), match data series colour |
| Callout boxes | BG_PANEL or BG_CARD background with accent-coloured border |
| Overall | Clean, not busy or cluttered |

---

## 11. Accessibility

- Ensure sufficient contrast between data colours and background
- The primary blue palette provides adequate contrast on `#FFFFFF`
- When using inline semantic green/red, add **pattern or marker differentiation** for colour-blind friendliness

---

## 12. Matplotlib Global Defaults (Python)

Every generated chart script must begin with this setup block.

### 12.1 Light Mode Setup (Default)

```python
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
import matplotlib.font_manager as fm
import numpy as np
import os

# === REGISTER FK GROTESK NEUE FONTS ===
_font_dir = os.path.expanduser('~/.claude/keyrock/assets/fonts')
for _ttf in ['FKGroteskNeue-Regular.ttf', 'FKGroteskNeue-Medium.ttf',
             'FKGroteskNeue-Bold.ttf', 'FKGroteskNeue-Light.ttf']:
    _path = os.path.join(_font_dir, _ttf)
    if os.path.exists(_path):
        fm.fontManager.addfont(_path)

# === KEYROCK BRAND PALETTE — LIGHT MODE (DEFAULT) ===
BG = '#FFFFFF'
BG_PANEL = '#F8FAFC'
BG_CARD = '#F1F5F9'

TEXT_PRIMARY = '#1F1F1F'
TEXT_MUTED = '#9B9B9B'

# Primary series colours (blue tones, up to 8 series)
PRIMARY = ['#3867FF', '#7696FF', '#A9BDFF', '#DEE2FF', '#001FFF', '#3636BB', '#22227E', '#303052']
PRIMARY_DEFAULT = PRIMARY[0]

# Secondary series colours (purple, 9+ series only)
SECONDARY = ['#A580FF', '#592DC5', '#371096']

# Accent colours (highlighting only — never as default data colour)
ACCENT_ORANGE = '#FF7800'
ACCENT_ORANGE_LIGHT = '#FFBA7D'

# Chart colour cycles
CHART_COLORS = PRIMARY.copy()
CHART_COLORS_EXTENDED = PRIMARY + SECONDARY

# Axis styling
X_AXIS_COLOR = TEXT_PRIMARY    # #1F1F1F — X-axis line only
TICK_COLOR = TEXT_MUTED        # #9B9B9B — both X and Y tick marks
GRID_COLOR = '#5F5F5F'
BORDER_COLOR = '#CBD5E1'

# Kerning note: Designer spec is -10 tracking for all text.
# FK Grotesk Neue has naturally tight tracking in its font metrics.
# matplotlib does not support letter-spacing adjustment. The font's
# default tracking is the closest achievable approximation.

plt.rcParams.update({
    'font.family': 'sans-serif',
    'font.sans-serif': ['FK Grotesk Neue', 'Inter', 'Inter Tight', 'Helvetica Neue', 'Helvetica', 'Arial', 'DejaVu Sans'],
    'font.size': 12,
    'text.color': TEXT_PRIMARY,
    'axes.facecolor': BG,
    'figure.facecolor': BG,
    'axes.edgecolor': BORDER_COLOR,
    'axes.labelcolor': TEXT_PRIMARY,
    'axes.labelweight': 'bold',
    'axes.labelsize': 12,
    'xtick.color': TICK_COLOR,
    'ytick.color': TICK_COLOR,
    'xtick.labelsize': 10,
    'ytick.labelsize': 10,
    'grid.color': GRID_COLOR,
    'grid.alpha': 0.3,
    'legend.fontsize': 12,
})

LOGO_PATH = os.path.expanduser('~/.claude/keyrock/assets/keyrock-logo-black.png')
```

### 12.2 Dark Mode Override

> **Note:** The new palette was specified for light mode only. Dark mode structural colours have been adapted to work with the new data colours. PRIMARY and SECONDARY palettes are used identically in both modes. This adaptation is pending designer review.

When dark mode is requested, apply this block **after** the light mode setup:

```python
# === DARK MODE OVERRIDE ===
BG = '#0B1A2E'
BG_PANEL = '#122240'
BG_CARD = '#1A2D4A'
TEXT_PRIMARY = '#FFFFFF'
TEXT_MUTED = '#9B9B9B'
X_AXIS_COLOR = '#FFFFFF'
TICK_COLOR = '#9B9B9B'
GRID_COLOR = '#1E3A5F'
BORDER_COLOR = '#2D4A6F'

# PRIMARY, SECONDARY, ACCENT colours stay identical (high-saturation, work on dark)

plt.rcParams.update({
    'text.color': TEXT_PRIMARY,
    'axes.facecolor': BG,
    'figure.facecolor': BG,
    'axes.edgecolor': BORDER_COLOR,
    'axes.labelcolor': TEXT_PRIMARY,
    'xtick.color': TICK_COLOR,
    'ytick.color': TICK_COLOR,
    'grid.color': GRID_COLOR,
    'grid.alpha': 0.2,
})

LOGO_PATH = os.path.expanduser('~/.claude/keyrock/assets/keyrock-logo-white.png')
```

---

## 13. Axis Styling Helper (matplotlib)

```python
def style_axes(ax, grid_axis='y'):
    """Apply Keyrock brand axis styling.
    grid_axis: 'y' (default), 'x', 'both', or None to disable grid.
    """
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    ax.spines['left'].set_visible(False)
    ax.spines['bottom'].set_color(X_AXIS_COLOR)
    ax.spines['bottom'].set_linewidth(2)

    ax.tick_params(axis='y', colors=TICK_COLOR, labelsize=10, width=1, length=4)
    ax.tick_params(axis='x', colors=TICK_COLOR, labelsize=10, width=1, length=4)

    if grid_axis:
        ax.grid(axis=grid_axis, alpha=0.3, linewidth=0.5, zorder=0, color=GRID_COLOR)
```

---

## 14. Logo Placement Pattern (matplotlib)

```python
def add_keyrock_logo(fig, logo_path=LOGO_PATH, size=0.08, position='top-right', padding=0.02):
    """Add Keyrock logo to chart. size is fraction of figure width.
    NOTE: /keyrock-chart does NOT add a logo by default — do not call this for
    generated charts. Kept only for manual use if a logo is ever explicitly asked for."""
    try:
        logo = mpimg.imread(logo_path)
        aspect = logo.shape[1] / logo.shape[0]  # width/height
        logo_width = size
        logo_height = logo_width / aspect * (fig.get_figwidth() / fig.get_figheight())

        if position == 'bottom-right':
            x = 1 - padding - logo_width
            y = padding
        elif position == 'bottom-left':
            x = padding
            y = padding
        elif position == 'top-right':
            x = 1 - padding - logo_width
            y = 1 - padding - logo_height
        elif position == 'top-left':
            x = padding
            y = 1 - padding - logo_height

        logo_ax = fig.add_axes([x, y, logo_width, logo_height])
        logo_ax.imshow(logo)
        logo_ax.axis('off')
    except FileNotFoundError:
        pass  # Skip logo if file not found
```

---

## 15. Export Pattern (matplotlib)

```python
def export_chart(fig, name, output_dir='.', dpi=250, formats=('svg', 'png', 'pdf')):
    """Export chart in multiple formats. SVG is master."""
    os.makedirs(output_dir, exist_ok=True)
    for fmt in formats:
        path = os.path.join(output_dir, f'{name}.{fmt}')
        fig.savefig(path, dpi=dpi, bbox_inches='tight',
                    facecolor=fig.get_facecolor(), edgecolor='none',
                    format=fmt)
    plt.close(fig)
```

---

---

## 16. Chart Layout Helper (matplotlib)

This function replaces manual `ax.set_title()` / `fig.suptitle()` / `fig.text(source)` / `plt.tight_layout()` calls. It positions the **title**, an optional **legend row**, and the **source** at figure level, then pins the axes deterministically. It reproduces the spacing of the Stablecoin FX report charts — the house reference for what good Keyrock spacing looks like.

**No subtitle.** Keyrock charts never carry a subtitle/subheader (Amir's standing rule). The helper has no subtitle parameter. Put any context into the title itself or an in-chart annotation.

**Spacing principle: inches, scale-invariant.** Padding is specified in inches so it stays physically consistent regardless of figure size, then converted to figure fractions and applied with `fig.subplots_adjust` (deterministic — the old `tight_layout(rect=...)` + `top_extra_inches` + hand-anchored `legend_y = 1.0 - 1.05/H` combination drifted and was the cause of header/legend gaps). The visual target is the FX charts: compact bold title at the top, a single frameless legend row tucked beneath it when needed, generous-but-even breathing room, muted source bottom-left.

```python
def layout_chart(fig, title, source='Source: Keyrock Research',
                 legend_handles=None, legend_ncol=None,
                 title_align='center', title_fontsize=17,
                 bottom_extra_inches=0.0):
    """Apply Keyrock chart layout (title + optional legend + source) with
    inch-based, deterministic spacing matching the Stablecoin FX charts.

    Call AFTER all chart content is drawn, BEFORE export_chart(). No logo is added.

    NO SUBTITLE — by design. Keyrock charts never use one.

    legend_handles: pass a list of Patch/Line2D handles and the helper places a
        single frameless legend row in the band directly under the title (and
        lowers the chart top to fit it). This is the ONLY supported way to add a
        top-of-chart legend — do not call ax.legend()/fig.legend() yourself.
    legend_ncol: column count for that legend (defaults to len(legend_handles)).
    title_align: 'center' (default, FX style) or 'left'.
    bottom_extra_inches: extra padding below the chart for rotated x labels.

    Spacing budget (inches, scale-invariant):
        Top margin (figure top → title):              0.40
        Title height (17pt bold):                     0.34
        Title → legend gap:                           0.16  (only if legend)
        Legend row height:                            0.24  (only if legend)
        (legend or title) → chart top:                0.40
        Chart → source gap:                           0.40 (+ bottom_extra)
        Source height (9pt):                          0.18
        Source → figure bottom:                       0.30
    """
    H = fig.get_figheight(); W = fig.get_figwidth()
    def f(inch): return inch / H

    TOP_PAD   = f(0.40)
    TITLE_H   = f(0.34)
    LGND_GAP  = f(0.16)
    LGND_H    = f(0.24) if legend_handles else 0.0
    CHART_GAP = f(0.40)
    SRC_GAP   = f(0.40 + bottom_extra_inches)
    SRC_H     = f(0.18)
    BOT_PAD   = f(0.30)

    # Title
    title_y = 1.0 - TOP_PAD
    title_x = 0.5 if title_align == 'center' else 0.06
    ha = 'center' if title_align == 'center' else 'left'
    fig.text(title_x, title_y, title, ha=ha, va='top',
             fontsize=title_fontsize, fontweight='bold', color=TEXT_PRIMARY)

    # Optional legend row, centred in the band under the title
    if legend_handles:
        legend_y = title_y - TITLE_H - LGND_GAP - LGND_H / 2
        fig.legend(handles=legend_handles, loc='center',
                   bbox_to_anchor=(0.5, legend_y),
                   ncol=legend_ncol or len(legend_handles), frameon=False,
                   fontsize=10.5, labelcolor=TEXT_PRIMARY,
                   columnspacing=2.4, handletextpad=0.6)
        chart_top = legend_y - LGND_H / 2 - CHART_GAP
    else:
        chart_top = title_y - TITLE_H - CHART_GAP

    # Source bottom-left
    src_y = BOT_PAD + SRC_H
    if source:
        fig.text(0.02, src_y, source, ha='left', va='bottom',
                 fontsize=9, color=TEXT_MUTED)
        chart_bottom = src_y + SRC_GAP
    else:
        chart_bottom = BOT_PAD

    # Pin axes deterministically. left/right are inch-scaled; override after the
    # call for charts that need a wider left margin (e.g. horizontal bars).
    left = 0.75 / W
    right = 1.0 - (0.35 / W)
    fig.subplots_adjust(left=left, right=right, top=chart_top, bottom=chart_bottom)
```

### Spacing budget (inch-based)

| Element | Padding (inches) | Notes |
|---|---|---|
| Top margin (figure top → title) | 0.40 | Consistent across all chart sizes |
| Title text height | 0.34 | 17pt bold + leading |
| Title → legend gap | 0.16 | Only when a legend is passed |
| Legend row height | 0.24 | Only when a legend is passed |
| (legend or title) → chart top | 0.40 | Breathing room above the chart |
| Chart bottom → source | 0.40 (+ optional bottom_extra) | Mirrors the top gap |
| Source text height | 0.18 | 9pt |
| Source → figure bottom | 0.30 | Tight to bottom edge |
| Left margin | 0.75 inches | Scaled from figure width; widen for horizontal bars |
| Right margin | 0.35 inches | Scaled from figure width |

### `bottom_extra_inches`

Pass extra bottom padding when x-axis labels are rotated or wrap (date/category labels that extend below the axis line). Typical value `0.20`. There is no `top_extra_inches` any more — the legend is handled by `legend_handles`, so nothing else protrudes above the chart.

### Anti-patterns to avoid

- **Never add a subtitle / subheader.** The helper has no subtitle param. Do not reintroduce one with `fig.text`.
- **Don't** place the legend yourself with a hand-tuned `legend_y = 1.0 - 1.05/H` or `bbox_to_anchor=(0.5, 1.02)`. Pass `legend_handles` to `layout_chart` (see §8).
- **Don't** specify title/source positions in figure fractions directly — use the helper so spacing holds across figure sizes.
- **Don't** add a logo. `/keyrock-chart` never places the Keyrock logo on generated charts.
- **Don't** use a 22pt title — the brand title size is 17pt (handled by the helper).

**Usage in templates:**
```python
# Standard chart (no legend, single series)
layout_chart(fig, 'My Title')

# Custom source
layout_chart(fig, 'My Title', source='Source: CoinGecko, Keyrock Research')

# Multi-series chart — let the helper place the legend
from matplotlib.patches import Patch
handles = [Patch(facecolor=COL_A, label='Series A'),
           Patch(facecolor=COL_B, label='Series B')]
layout_chart(fig, 'My Title', legend_handles=handles)

# Left-aligned title (rare — default is centred, FX style)
layout_chart(fig, 'My Title', title_align='left')

# Rotated date labels below the axis
layout_chart(fig, 'Monthly Trend', bottom_extra_inches=0.20)

export_chart(fig, 'chart_name')   # no logo — /keyrock-chart never adds one
```

---

## Quick Reference — Colour Hex Cheat Sheet

```
Primary Series (blue tones, use first):
PRIMARY[0]  #3867FF   Default / vibrant blue
PRIMARY[1]  #7696FF   Mid-light blue
PRIMARY[2]  #A9BDFF   Soft blue
PRIMARY[3]  #DEE2FF   Pale blue
PRIMARY[4]  #001FFF   Pure blue
PRIMARY[5]  #3636BB   Deep blue-violet
PRIMARY[6]  #22227E   Navy
PRIMARY[7]  #303052   Dark slate

Secondary (purple, 9+ series only):
SECONDARY[0]  #A580FF  Light purple
SECONDARY[1]  #592DC5  Mid purple
SECONDARY[2]  #371096  Deep purple

Accent (highlighting only):
ACCENT_ORANGE        #FF7800
ACCENT_ORANGE_LIGHT  #FFBA7D

Semantic exceptions (inline hex only):
Positive   #10B981   (green)
Negative   #EF4444   (red)

Structural:
BG           #FFFFFF   TEXT_PRIMARY  #1F1F1F
TEXT_MUTED   #9B9B9B   GRID_COLOR   #5F5F5F
```
