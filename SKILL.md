---
name: update-media-kit-from-report
description: Use when asked to update, refresh, transfer, import, sync, or copy social media analytics/report PDF statistics into an existing media kit webpage, printable HTML media kit, or media kit PDF source. Use this for Metricool or similar Instagram/TikTok/YouTube report PDFs, especially when the user wants all numbers, demographics, top content, or percentage deltas replaced while preserving the layout and design.
---

# Update Media Kit From Report

Use this skill to transfer statistics from a social media analytics PDF report into an existing media kit webpage. The media kit is usually an `index.html` plus CSS that is printed to PDF with `Ctrl+P`.

The goal is to update content and data only. Preserve the existing page structure, visual design, CSS system, A4 print behavior, and pricing unless the user explicitly asks to change those.

## Inputs To Look For

- A report PDF in the current project, commonly named like `report_metricool.pdf`, `metricool.pdf`, `social-media-report.pdf`, or similar.
- A media kit HTML file, commonly `index.html`.
- A stylesheet, commonly `styles.css`.

If multiple reports exist, use the newest one by modification time unless the user specifies a file.

## Workflow

1. Read the report PDF and identify the reporting period.
2. Read the current media kit HTML before editing.
3. Extract platform-level metrics for each available platform.
4. Extract demographic data, including gender, age, countries, and cities when present.
5. Extract top-performing content from ranking tables, including title/text, views, and links if the PDF exposes them.
6. Decide the source-of-truth scope before editing. For high-level monthly cards, prefer metrics for all content viewed during the report period. For top content lists, use the ranking table the report provides unless the user asks for a specific sort.
7. Update only the relevant text, numbers, labels, inline chart values, and profile/content links in the HTML.
8. Keep CSS changes minimal and only make them when the existing chart/list markup requires it.
9. Preserve the one-page print layout. Do not add large new sections unless the user asks.
10. Verify that there are no stale placeholder values such as `Update`, old month names, old percentages, or old handles.
11. Summarize what was updated and list any values that could not be extracted exactly.

## Field Mapping

Use `references/field-map.md` as the canonical mapping guide.

General mapping rules:

- `Followers` maps to Instagram/TikTok follower count.
- `Subscribers` maps to YouTube subscriber count.
- `Views`, `Video views`, `Post views`, or equivalent maps to the platform's monthly views.
- `Likes` maps to monthly likes for the same scope as views when possible.
- Use the percentage delta shown directly under or near each metric.
- If a platform has both `published content` and `viewed content` sections, prefer the viewed-period metric for monthly performance cards.
- If the media kit card says `Views in <month>`, use the viewed-period views metric and pair likes/interactions from the same viewed-period scope when available.
- Top content should come from ranking tables sorted by views, likes, date, or report default ranking. Prefer the highest-view or highest-ranked entries.
- If exact post URLs are not extractable and the PDF only displays text like `Go`, keep or use the platform profile URL and mention this limitation.

## Chart Updates

When the media kit uses CSS or HTML charts:

- Update inline percentages and labels directly in the HTML.
- For horizontal bars, update both the visible percentage and the CSS variable or inline width, such as `style="--w:47.22%"`.
- For vertical age histograms, update the visible percentage inside the bar and the `height` value. If exact age values are unavailable in extracted PDF text, do not invent exact numbers. Either keep existing approximate values and label them as approximate, or state that age values were not extractable.
- For country distributions, follow the current media kit convention. If it shows top 3 plus Others, calculate Others as `100 - top1 - top2 - top3`.
- For gender distributions, include all categories shown by the report, commonly Male, Female, and Unknown.

## What Not To Change

- Do not redesign the page.
- Do not restructure the layout.
- Do not change pricing unless explicitly requested.
- Do not add responsive/mobile behavior if the media kit is fixed for print.
- Do not remove contact information.
- Do not replace platform profile links unless the report or user provides better links.
- Do not invent private analytics that are not in the report.
- Do not silently mix scopes, such as using viewed-period views with published-content likes, unless the report lacks a matching viewed-period likes metric. If forced to mix scopes, mention it in the final response.

## Verification Checklist

Before finishing:

- The report period shown in the media kit matches the PDF.
- Platform cards use the latest report values.
- Percentage deltas match the PDF.
- Top countries/cities match the PDF and Others is calculated correctly.
- Top content entries match the report ranking table.
- Old placeholders and old month labels are gone.
- The HTML still references the stylesheet correctly.
- The fixed print layout is preserved.

## Final Response

Keep the final response concise. Include:

- Which report was used.
- Which files were updated.
- Any values that could not be extracted exactly.
- Any manual follow-up needed, such as exact post URLs if the PDF did not expose them.
