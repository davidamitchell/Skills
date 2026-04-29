---
name: inline-citation
version: "1.0"
description: Formats hyperlinked inline citations as Author (Year) anchors placed
  immediately after the claim they support. Use when writing blog posts, technical
  documentation, internal knowledge bases, or web-published research summaries that
  require visible attribution and directly accessible sources.
---

# Inline Linked Citation (APA-inspired)

## When Not to Use

- When the output is a formal academic submission requiring strict APA, MLA, Chicago,
  or other institutional style compliance — use a dedicated reference manager and
  citation style instead
- When the medium does not support hyperlinks (print documents, plain-text exports,
  PDF without link annotations)
- When the content is purely creative or fictional and factual attribution is not
  required

---

## Interaction Protocol

**Before starting**, ask if not already clear:

1. Is an optional reference list required at the end, or inline citations only?
2. Are primary sources already identified, or must sources be located during writing?

**Output style**:

- Every factual claim carries an inline citation in the canonical form: `<a href="URL">Author (Year)</a>`
- Flag any claim that cannot be sourced with `[SOURCE NEEDED]`
- Do not silently omit citations for hard-to-source claims — surface them

---

## Inputs and Outputs

**Input**: Draft text with factual claims plus any source materials provided  
**Output**: Revised text with inline linked citations; optional reference list appended if requested; list of flagged unsourced claims  
**Composability**: Use alongside `citation-discipline` for full epistemic rigour; apply after `research` or `strategy-author`; run `speculation-control` in parallel to ensure non-factual content is labeled

---

## Citation Format

### Canonical form

```html
<a href="URL">Author (Year)</a>
```

### Examples

```html
<a href="https://www.nber.org/papers/w31161">Brynjolfsson (2023)</a>
<a href="https://www.iea.org/reports/oil-market-report-march-2024">IEA (2024)</a>
```

---

## Placement

- Insert the citation immediately after the claim it supports.
- Place the citation before terminal punctuation where possible.

Correct:

> AI adoption improves productivity <a href="…">Brynjolfsson (2023)</a>.

Incorrect:

> AI adoption improves productivity. <a href="…">Brynjolfsson (2023)</a>

---

## Author Naming

- Use the surname for individual authors: `Smith (2022)`
- Use the organisation name when no clear individual author is identified: `IEA (2024)`
- Use `et al.` for three or more authors: `Smith et al. (2021)`
- Never use generic labels such as "Source" or "Reference"

---

## Year

- Use the publication year of the cited work.
- If the year is unknown or unavailable, use `n.d.` (no date): `WHO (n.d.)`

---

## Multiple Citations

Do not bundle multiple sources into a single hyperlink or a single anchor element.

**Avoid**:

```html
<a href="…">Smith (2022); IEA (2024)</a>
```

**Do instead**:

```html
<a href="…">Smith (2022)</a>; <a href="…">IEA (2024)</a>
```

---

## Reuse

- Repeat the full citation each time a claim requires support.
- Do not rely on an earlier citation implicitly — each claim must be independently traceable.

---

## Link Requirements

- The URL must resolve directly to the cited content — not to a homepage, category
  page, or search result.
- Prefer primary sources over secondary commentary or summaries.
- Do not use URL shorteners.
- Use HTTPS where available.

---

## Optional Reference List

An alphabetically ordered reference list at the end of the document is permitted
but not required.

If included:

- Format each entry in APA-like style: Author (Year). *Title*. Publisher/URL.
- Inline citations must still be present regardless — the reference list does not
  replace them.

---

## Edge Cases

| Situation | Form |
|---|---|
| No named author | `<a href="…">World Bank (2023)</a>` |
| No date available | `<a href="…">UNESCO (n.d.)</a>` |
| Three or more authors | `<a href="…">Smith et al. (2021)</a>` |
| Organisation as author | `<a href="…">IEA (2024)</a>` |

---

## Anti-patterns

- Raw URLs embedded in body text instead of attached to an author–year anchor
- "Click here", "this source", or other non-descriptive link text
- Citations missing an author name or year
- Linking to secondary commentary when the primary source is accessible
- Bundling multiple sources into a single `<a>` element
- Using a homepage URL instead of a direct link to the cited content

---

## Mandatory Pre-Output Checklist

Run these checks before marking output complete:

1. **Author + year present**: Every inline citation contains an identifiable author or organisation name and a year (or `n.d.`).
2. **Hyperlink attached**: Every inline citation is wrapped in an `<a href="…">` element with a non-empty `href`.
3. **Source resolves directly**: Each URL points to the specific cited content, not a homepage or summary page.
4. **Citation at point of claim**: Each citation immediately follows the claim it supports; no orphaned citations placed at paragraph or section ends without a corresponding specific claim.
5. **No bundled citations**: No single `<a>` element contains more than one author–year pair.
6. **Unsourced claims flagged**: Any claim without a locatable source is marked `[SOURCE NEEDED]` rather than left bare.

---

## Failure Modes

- Factual claims without any attached citation
- Generic link text ("click here", "source") instead of Author (Year)
- A single hyperlink covering multiple sources
- Linking to a homepage or aggregator rather than the primary document
- Placing the citation at the end of a paragraph rather than at the point of the specific claim
- Using a URL shortener that obscures the destination
- Omitting the citation on second or later use of the same claim
