# SVG Design System (Material Dark)

Use Material Dark's true-black themed SVG patterns for all diagrams in the HTML canvas.

## Color Palette

| Category | Fill | Stroke | Use For |
|----------|------|--------|---------|
| Primary | `rgba(68,136,255,0.12)` | `#448aff` (blue) | Inputs, user-facing, frontend |
| Secondary | `rgba(105,240,174,0.12)` | `#69f0ae` (green) | Services, processing, backend |
| Tertiary | `rgba(179,136,255,0.12)` | `#b388ff` (purple) | Database, storage, persistence |
| Accent | `rgba(255,215,64,0.12)` | `#ffd740` (amber) | Infrastructure, regions, groups |
| Alert | `rgba(255,82,82,0.12)` | `#ff5252` (red) | Errors, edge cases, warnings |
| Neutral | `rgba(117,117,117,0.12)` | `#757575` (gray) | External, generic |

## SVG Background

`#000000` with subtle grid:

```svg
<pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
  <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#1a1a1a" stroke-width="0.5"/>
</pattern>
```

## Component Box Pattern

```svg
<rect x="X" y="Y" width="160" height="60" rx="6" fill="#000000"/>
<rect x="X" y="Y" width="160" height="60" rx="6" fill="FILL" stroke="STROKE" stroke-width="1.5"/>
<text x="CX" y="Y+24" fill="#e0e0e0" font-size="11" font-weight="600" text-anchor="middle">Name</text>
<text x="CX" y="Y+40" fill="#757575" font-size="9" text-anchor="middle">description</text>
```

Note: the first rect is the masking layer preventing arrows from showing through semi-transparent component fills.

## Arrow Markers

Create color-specific arrowheads:

```svg
<marker id="arrow-blue" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
  <polygon points="0 0, 10 3.5, 0 7" fill="#448aff"/>
</marker>
```

Standard gray arrow:
```svg
<marker id="arrow" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
  <polygon points="0 0, 10 3.5, 0 7" fill="#616161"/>
</marker>
```

## Layering Order

SVG paints back-to-front. Draw in this order:

1. Background fill + grid pattern
2. Region/group boundaries (dashed outlines)
3. Connection arrows and lines
4. Opaque masking rects (same positions as boxes, `fill="#000000"`)
5. Component boxes (semi-transparent fill + stroke)
6. Text labels
7. Title block

## Spacing Rules

- Box height: 50-60px standard
- Min gap between boxes: 40px vertical, 30px horizontal
- Arrow label clearance: 10px from any box edge
- Region boundary padding: 20px inside edges
- viewBox: extend to fit all content + 30px padding

## Region Boundary

```svg
<rect x="X" y="Y" width="W" height="H" rx="12" fill="none" stroke="#ffd740" stroke-width="1" stroke-dasharray="8,4"/>
<text x="X+12" y="Y+16" fill="#ffd740" font-size="9" font-weight="600">Region Name</text>
```

## Database Cylinder

```svg
<g transform="translate(X, Y)">
  <rect x="0" y="10" width="120" height="50" rx="2" fill="#000000"/>
  <ellipse cx="60" cy="10" rx="60" ry="12" fill="#000000"/>
  <ellipse cx="60" cy="60" rx="60" ry="12" fill="#000000"/>
  <rect x="0" y="10" width="120" height="50" fill="rgba(179,136,255,0.12)"/>
  <ellipse cx="60" cy="10" rx="60" ry="12" fill="rgba(179,136,255,0.12)" stroke="#b388ff" stroke-width="1.5"/>
  <ellipse cx="60" cy="60" rx="60" ry="12" fill="rgba(179,136,255,0.12)" stroke="#b388ff" stroke-width="1.5"/>
  <line x1="0" y1="10" x2="0" y2="60" stroke="#b388ff" stroke-width="1.5"/>
  <line x1="120" y1="10" x2="120" y2="60" stroke="#b388ff" stroke-width="1.5"/>
  <text x="60" y="40" fill="#e0e0e0" font-size="11" font-weight="600" text-anchor="middle">Database</text>
</g>
```

## Decision Diamond (Flowchart)

```svg
<g transform="translate(CX, CY)">
  <polygon points="0,-35 50,0 0,35 -50,0" fill="#000000"/>
  <polygon points="0,-35 50,0 0,35 -50,0" fill="rgba(255,215,64,0.12)" stroke="#ffd740" stroke-width="1.5"/>
  <text y="4" fill="#e0e0e0" font-size="10" font-weight="600" text-anchor="middle">Condition?</text>
</g>
```

## Typography

Use system monospace font family for labels:
```svg
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&display=swap');
  text { font-family: 'JetBrains Mono', 'SF Mono', 'Cascadia Code', monospace; }
</style>
```

Font sizes by role:
- **Title:** 16px, weight 700
- **Component name:** 11-12px, weight 600
- **Sublabel / description:** 9px, weight 400, color `#757575`
- **Annotation / note:** 8px, weight 400
- **Tiny label (on arrows):** 7-8px
