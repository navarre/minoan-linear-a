# Extraction proof: Arkhanes pilot (`ARKH 6`)

## Target

After the Zakros pilot, I chose a **contrasting single-document pilot from Arkhanes**: `ARKH 6`.

Why this slice:
- It uses the same underlying website machinery, so it is a good test of method transfer.
- It comes from a different site and period (`LM I` rather than `LM IB`).
- It is compact but not trivial: six signs, three word pages, and one unresolved sign embedded in the final sequence.

Relevant source pages in the imported snapshot:
- `imported/lineara-website/site/location/Arkhanes/index.html`
- `imported/lineara-website/site/document/ARKH 6/index.html`
- `imported/lineara-website/site/document/ARKH 6/index-1.html` … `index-6.html`
- `imported/lineara-website/site/document/ARKH 6/index-word-0.html` … `index-word-2.html`

## What was parsed

### 1. Location-level context
From `location/Arkhanes/index.html`:
- Site label: `Arkhanes`
- Reported document count at that site: `10`

### 2. Document-level metadata
From `document/ARKH 6/index.html` I reliably extracted:
- document code: `ARKH 6`
- kind: `Tablet`
- location: `Arkhanes`
- period: `LM I`
- dimensions: `4.9 × 2.6 × 0.7 cm`
- external corpus link
- drawing image path
- reported totals: `6 signs / 3 words`

### 3. Sign-occurrence layer
From the main document page I extracted **6 occurrence records** with:
- occurrence number (`#1` … `#6`)
- site-provided role label (`Syllabogram` throughout)
- sign code when present (`AB01`, `AB06`, `AB69`, `AB81`, `AB53`)
- display reading when present (`da`, `na`, `tu`, `ku`, `ri`)
- exact SVG bounding box on the tablet image
- per-occurrence crop image path
- provenance back to source HTML pages

Occurrence `5` is explicitly `[?]` and was preserved as unresolved.

### 4. Sequence / word layer
From `index-word-0.html` to `index-word-2.html` I extracted **3 sequence records**:
- Sequence 1: `da-na-tu` (`AB01-AB06-AB69`)
- Sequence 2: `ku[` (normalized pattern `AB81`)
- Sequence 3: `][?]-ri[` (normalized pattern `[?]-AB53`)

Matched occurrence IDs by exact SVG coordinate equality:
- Sequence 1 → `[1, 2, 3]`
- Sequence 2 → `[4]`
- Sequence 3 → `[5, 6]`

This gives a useful contrast with the Zakros proof: the method still works, but the document is more purely syllabic and the uncertainty sits inside the final two-sign sequence rather than as a standalone unknown word.

## Fields that were reliably extracted

### Document
Reliable:
- `document_code`
- `kind`
- `location`
- `period`
- `dimensions_cm`
- `corpus_url`
- `drawing_image`
- `reported_sign_count`
- `reported_word_count`
- `source_page`

### SignOccurrence
Reliable:
- `occurrence_number`
- `role`
- `sign_code` when present
- `display_reading` when present
- `bbox_on_document_image`
- `source_occurrence_page`
- `source_crop_image`
- explicit uncertainty on occurrence `5`

### Sequence
Reliable:
- `sequence_number_within_document`
- `display_reading`
- `normalized_pattern`
- `reported_sign_count`
- `selected_word_bboxes`
- derived `matched_occurrence_numbers_by_bbox`
- `source_page`

## Ambiguities and caution points

1. **Unknown sign remains unknown**
   - Occurrence `5` is `[?]` and was not normalized beyond that.

2. **Bracket notation is source-facing**
   - Displays such as `ku[` and `][?]-ri[` were preserved literally from the site UI.
   - They are useful evidence, but they should not be mistaken for cleaned transliterations.

3. **Role labels are source assertions**
   - All six signs are labeled `Syllabogram` by the site.
   - I preserved that label as source data rather than treating it as an independently verified epigraphic judgment.

4. **Sequence linkage is derived**
   - As with the other proofs, word pages do not print occurrence numbers directly.
   - The linkage was reconstructed by exact coordinate matches and marked as derived.

## Why this matters to the project mission

This second proof matters because it shows the extractor logic is portable. The old site exposes the same latent data model across more than one site, so the project is not trapped in a Haghia Triada-only or Zakros-only proof of concept.

That makes the case for a corpus-wide relational import much stronger.

## Deliverable produced

Structured extraction file:
- `data/extraction-proofs/arkhanes-arkh6.json`
