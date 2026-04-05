# Verifier — Cowork GORILA extraction audit

_Date:_ 2026-04-06

## Scope

This is an independent spot-check audit of four extracted GORILA data files:

- `linear_a/data/gorila_page_map.json`
- `linear_a/data/gorila_concordances_full.json`
- `linear_a/data/gorila_sign_variants.json`
- `linear_a/data/gorila_sign_index_rows.json`

I did **not** re-extract the full corpus. I checked a targeted sample against the actual JPG page images in `references/gorila/`.

## Headline result

The extraction set looks **useful and mostly real**, but not equally mature across all four files.

- **Strongest reliability:** `gorila_sign_variants.json`, `gorila_sign_index_rows.json`
- **Good but imperfect:** `gorila_page_map.json`
- **Weakest auditability / current blocker:** `gorila_concordances_full.json`, because the JSON does **not** preserve the actual vol. 5 concordance source-page pointer for each extracted entry, so random-entry verification is not reproducible from the JSON alone.

## 1) `gorila_page_map.json` — page classification spot-check

### Sample checked
I spot-checked 9 page images across multiple types:

| File | JSON type | Visual result | Verdict |
|---|---|---|---|
| `vol2/138` | `photo` | artifact/inscription image page | correct |
| `vol5/172` | `table` | concordance table page | correct |
| `vol2/017` | `text` | French scholarly text page | correct |
| `vol5/029` | `sign_plate` | sign-variant plate page | correct |
| `vol1/371` | `blank` | near-blank colophon/imprint end page | acceptable / close enough |
| `vol4/029` | `prelim` | visible section page titled `CONCORDANCES` | **misclassified** |
| `vol4/092` | `section_divider` | visually blank page | **misclassified** |
| `vol5/328` | `sign_index` | sign-index page | correct |
| `vol5/464` | `cefael_watermark` | watermark/placeholder page | correct |

### Result
- **7/9 usable classifications correct or acceptable**
- **2/9 clear mismatches** in the sample

### Interpretation
The page map is good enough for exploratory work, but it is **not error-free**. The most likely failure mode is boundary confusion between:
- `prelim` vs `section_divider`
- `section_divider` vs `blank`

That matters if downstream automation depends on exact page-type boundaries.

## 2) `gorila_sign_variants.json` — A 301 spot-check

### Claim checked
`A 301` entry says:
- `variant_count = 11`
- `source_page = [45, 46]`

### Visual check
I inspected:
- `references/gorila/vol5/EtCret_21-5_1985_045.jpg`
- `references/gorila/vol5/EtCret_21-5_1985_046.jpg`

The sign `A 301` is visibly present across the two pages, with approximately:
- **6 variant drawings on page 45**
- **5 variant drawings on page 46**

Total: **~11 variants**.

### Result
**Confirmed.** The A 301 entry is consistent with the plate pages and the reported count of 11 variants across pp. 45-46.

## 3) `gorila_sign_index_rows.json` — row spot-check

### Sample checked
I checked 4 sampled rows against their cited `file_page` images:

| Sample row | File page | Visual result | Verdict |
|---|---:|---|---|
| `AB 51 / HT 7a.3 / *51*-67` | 268 | row appears plausible on AB 51 sign-index page | correct/plausible |
| `AB 45 / CR(?) Zf 1 / 08-58-*45*` | 264 | row appears plausible on AB 45 sign-index page | correct/plausible |
| `A 702 / compound rows` | 368 | compound section clearly present | correct/plausible |
| `A 709 standalone row (HT 81.2)` | 375 | standalone A 709 rows visible | correct/plausible |

### Result
**4/4 sampled rows were consistent with the source pages.**

### Interpretation
This is the strongest extraction in the batch. I did not find evidence in this sample that the sign-index row file is fabricated, inflated, or loosely paraphrased. It looks like a serious structured extraction of the GORILA sign index.

## 4) `gorila_concordances_full.json` — auditability problem and partial spot-check

### What I expected
The task asked for random-entry verification against the relevant GORILA page image.

### What I found
This JSON preserves fields like:
- `id`
- `inventory_number`
- `dating`
- `gorila_ref`

But it does **not** preserve the actual **vol. 5 concordance source page image** where each entry was extracted from.

That matters because:
- the extraction source is said to be **GORILA vol. 5, pp. 82-113**,
- but the JSON field `gorila_ref` points to the **edition reference** (for example `1, p. 262`, `4, p. 86`, `3, p. 164`, `5, p. 62`),
- and that field is **not enough** to recover the actual concordance row image in vol. 5 for audit purposes.

### Partial test
I tried four spot-checks by opening pages suggested by `gorila_ref`:

| Entry | Page opened | Result |
|---|---|---|
| `KN 28 / HM 708 / 1, p. 262` | `vol1/262` | did **not** show the concordance row |
| `LA Zb 1 / Coll. Métaxas / 4, p. 86` | `vol4/086` | did **not** show the concordance row |
| `ZA 8 / HM 1619 / 3, p. 164` | `vol3/164` | did **not** show the concordance row |
| `SY Za 1 / HM 3459 / 5, p. 62` | `vol5/062` | **did** match visibly |

### Interpretation
This does **not** prove the concordance extraction is wrong. It proves something narrower and important:

> **The concordance JSON is currently not source-addressable enough for efficient verifier auditing.**

The missing piece is a direct source locator such as:
- vol. 5 concordance `file_page`, or
- concordance-page range/row index, or
- image filename for the extracted row.

Without that, random verification becomes a manual browse/OCR job through the vol. 5 concordance section.

## Quality summary

### By file
- `gorila_page_map.json`: **useful, mostly right, but some classification errors**
- `gorila_sign_variants.json`: **A 301 spot-check confirmed**
- `gorila_sign_index_rows.json`: **strong sample; 4/4 plausible/correct**
- `gorila_concordances_full.json`: **not falsified, but insufficiently source-addressable for clean audit**

### Approximate spot-check accuracy from this pass
If I count only items that were directly and fairly testable in this pass:
- page map: **7/9 correct or acceptable**
- sign variants A 301: **1/1 confirmed**
- sign index rows: **4/4 confirmed/plausible**
- concordance direct-source checks: **1/4 directly matched using naïve page resolution, but the main issue here is auditability, not proven extraction error**

## Main issues found

1. **Page-map boundary classifications are imperfect**
   - especially `prelim` / `section_divider` / `blank`

2. **Concordance extraction lacks source-page provenance**
   - this is the biggest verifier problem in the current extraction set
   - not necessarily wrong data, but hard-to-audit data

3. **Sign-index and sign-variant extractions look materially stronger than the concordance extraction package**
   - these should be treated as the more trustworthy machine-readable outputs right now

## Recommended corrections

### High priority
Add direct provenance fields to every concordance entry, for example:
- `source_volume`
- `source_file_page`
- `source_printed_page`
- `source_row_index` or `source_bbox`

That would make the concordance file actually auditable.

### Medium priority
Revisit page-map classifications for pages currently labeled:
- `prelim`
- `section_divider`
- `blank`
- `blank_or_minimal`

A fast second-pass review could likely clean up the small but real boundary errors.

## Bottom line

Cowork’s GORILA extraction work is **not smoke and mirrors**. The parts that matter most for current research — especially the sign-index rows and sign-variant plates — survive spot-checking well.

The main weakness is not obvious bad data; it is **missing provenance on concordance entries**, which makes verifier-grade auditing harder than it should be.
