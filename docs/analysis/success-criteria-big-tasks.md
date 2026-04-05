# Success Criteria — BIG Tasks (2026-04-05)

Written before the work begins. After each task lands, Builder will read the output against these criteria and write a pass/fail/partial assessment as an appendix to this file. The point is to prevent goal creep and overclaiming: if the deliverable doesn't hit the "Pass" bar below, we say so rather than declaring victory.

---

## BIG-1. Sign Behavior Atlas (all 207 signs)

**Input data:** `linear_a/data/gorila_sign_index_rows.json` (3,936 rows), `linear_a/data/signs.json`, `linear_a/data/signs_to_gorila_index.json`, corpus concordance (468 Vol 5 entries).

### Pass (minimum to claim success)
1. **Coverage.** All 207 sign identifiers in the GORILA sign index have a profile entry. Not "the interesting 50 signs" — all 207.
2. **Per-sign profile fields.** Each profile contains, as structured data:
   - Total attestation count (index rows)
   - Positional distribution: counts for `alone` / `first` / `non-initial` / `last` / `composite`
   - Top 5 neighbor signs (pre- and post-) with counts
   - Log-vs-syll split (where determinable)
   - Site distribution (attestation count per site)
   - Document-type distribution (nodule / tablet / stone vessel / seal / other)
3. **Deliverable artifacts.**
   - A JSON file: `linear_a/data/sign_behavior_atlas.json` with one object per sign
   - A human-readable analysis doc: `docs/analysis/sign-behavior-atlas.md` containing methodology, summary statistics across the 207, and at least **3 observational findings** derived from the dataset
   - A public browsable page: `docs/sign-behavior-atlas.html` (or extension of `sign-concordance.html`) that lets a visitor sort/filter the 207 profiles
4. **Reproducibility.** The JSON file regenerates from a documented script, committed to the repo, so that when new data lands the atlas can be rebuilt without hand work.

### Stretch (exceptional)
- Quantitative clustering of signs into functional groups (e.g. k-means or hierarchical clustering on the positional + distributional features), with at least one cluster that matches a prior known category (syllabograms vs logograms) as an internal validity check.
- At least one finding that is not already in any existing project doc — a signal that the atlas produced new knowledge rather than repackaging known facts.
- Statistical significance testing for any site-level or hand-level claim (e.g., "*301 clusters at HT" tested against random baseline).

### Fail / overclaim (do not do)
- Assigning phonetic values to undeciphered signs based on distribution alone.
- Claiming a sign is "clearly" a logogram or syllabogram when the data is ambiguous — use confidence ranges.
- Cherry-picking the 20 most interesting signs and leaving the other 187 as stubs.
- Using the word "proves" anywhere in the output. Distributional data supports; it does not prove.

### Measurable pass bar
- 207/207 signs profiled.
- Each profile has ≥6 of the 7 specified fields populated.
- Analysis doc contains ≥3 observational findings, each tied to a specific data point or subset.
- Script to rebuild the atlas is committed and runs end-to-end without manual intervention.

---

## BIG-2. Three-Way Corpus Audit (ours vs Younger vs GORILA)

**Input data:** `linear_a/data/corpus.json` (1,880 docs), Younger's Lexicon of Linear A (online), GORILA Vol 1–5 concordance tables (468 entries) plus GORILA sign-index document references.

### Pass (minimum to claim success)
1. **Coverage.** Every document in `corpus.json` has been checked against *at least one* external source (Younger or GORILA). Documents unmatched in any external source are flagged as "only ours" — not silently dropped.
2. **Disagreement matrix.** A structured output (`linear_a/data/corpus_audit_matrix.json`) with one row per document, columns:
   - `our_id`, `younger_id`, `gorila_ref`
   - `reading_ours`, `reading_younger`, `reading_gorila`
   - `agreement_level`: `exact` / `minor` / `major` / `ours-only` / `external-only`
   - `resolution`: text field explaining what we believe is correct and why
3. **Known gaps closed.** The Nerokourou `NO Za 1` gap (flagged in `sign-301.md`) is resolved — either ingested or documented with reason not to ingest. Likewise the three unmatched composite signs from `verifier-gorila-signs.md` (A 506, A 684, A 718) are addressed.
4. **Human-readable summary.** `docs/analysis/three-way-corpus-audit.md` with: methodology, coverage statistics, top 10 disagreement cases with resolutions, list of "only ours" documents (what we have that nobody else does — this is a potential scientific contribution and should be highlighted), list of "missing from ours" documents.

### Stretch (exceptional)
- Disagreements resolved for ≥80% of cases (not just flagged).
- Reading disagreements split by type: tokenization differences vs genuine sign-value disagreements vs damage/uncertainty disagreements.
- Cross-references added to `corpus.json` entries so each document carries its `younger_id` and `gorila_ref` inline for future users.

### Fail / overclaim (do not do)
- Declaring "agreement" for documents where only museum inventory matches but readings weren't actually compared.
- Treating Younger's Lexicon as gold truth. It isn't — it's a thorough but secondary compilation with known errors.
- Counting "we couldn't find it in the external source" as "we have unique documents" without verifying the external sources actually don't have it.
- Leaving >10% of the corpus in "agreement_level: unknown".

### Measurable pass bar
- ≥95% of `corpus.json` documents have been checked against ≥1 external source.
- The `agreement_level` column is populated for ≥95% of documents.
- ≥1 previously undocumented "only ours" document is identified (or a documented finding that none exist).
- `NO Za 1` and the three composite signs are resolved.

---

## BIG-3. Scribal Hand Atlas

**Input data:** Vol 5 concordance hand assignments (subset of 468 entries that carry hand info), `corpus.json`, the Sign Behavior Atlas output if BIG-1 has landed.

### Pass (minimum to claim success)
1. **Full hand ingestion.** Every hand assignment in the Vol 5 concordance is mapped to our corpus documents. Output: `linear_a/data/scribal_hands.json` with `hand_id → [document_ids]`.
2. **Per-hand profile.** Each hand with ≥5 attributed documents has a profile:
   - Site(s) where the hand appears
   - Period (if determinable from the documents)
   - Document types (tablet / nodule / stone vessel / etc.)
   - Sign inventory used by that hand (top 20 signs by frequency)
   - Admin vs ritual classification of attested documents
3. **At least one tested hypothesis.** One of:
   - "Hands cluster by site" — tested by checking cross-site hand occurrences
   - "Hands cluster by document type" — tested by purity metrics
   - "*301 hand-distribution is non-random" — tested against a random baseline
   Report includes pass/fail of the hypothesis with supporting numbers.
4. **Human-readable output.** `docs/analysis/scribal-hand-atlas.md` with methodology, major hands profiled, the tested hypothesis, and at least 2 observational findings.

### Stretch (exceptional)
- A genuinely new finding: a specific hand crosses two sites not previously linked in the literature, or a hand's sign inventory differs from other hands at the same site in a structurally meaningful way.
- Public hand-browser page on the site.
- Integration with `sign-behavior-atlas` such that each sign profile shows which hands use it most.

### Fail / overclaim (do not do)
- Enumerating hands as a list without any analysis (that's just data ingestion).
- Claiming a "finding" that is actually just a restatement of what's already in Godart & Olivier's own hand catalog.
- Using small-sample hands (n < 5 documents) to make strong claims about hand behavior.

### Measurable pass bar
- ≥90% of Vol 5 concordance hand assignments are mapped to corpus documents.
- All hands with ≥5 attributed documents have full profiles.
- ≥1 tested hypothesis with reported result.
- ≥2 observational findings in the analysis doc.

---

## BIG-4. Phonological Inventory Reconstruction

**Input data:** Everything. Sign Behavior Atlas (BIG-1), Three-Way Audit (BIG-2), `glossary.json`, `libation-formula.md`, `sign-301.md`, Linear B phonetic values, published work on Luwian borrowings in Linear A, the 36 reference papers in our bibliography.

### Pass (minimum to claim success)
1. **A proposed phonemic inventory.** Specific consonants (with features: place, manner, voicing) and specific vowels (with features: height, backness, rounding). Not "probably has a pharyngeal" — "the inventory includes /ħ/ or /ʕ/ with confidence level X, evidence Y."
2. **A syllable-structure hypothesis.** What syllable shapes are permitted (CV, CVC, CCV, etc.)? What constraints on sequences?
3. **Treatment of every "lost" sign.** Every Linear A sign with no Linear B equivalent (including *301) gets a phonological hypothesis with stated confidence. "Unknown" is a valid hypothesis for some, but has to be argued rather than defaulted to.
4. **Per-claim citation.** Every phonological claim in the document has an inline citation: either to a specific dataset in our data layer, a specific published paper, or both. No unsourced assertions.
5. **Falsifiability.** At least 3 specific falsifiable predictions: "If X is discovered, this reconstruction is wrong." Without these, the reconstruction is not science.

### Stretch (exceptional)
- Quantitative comparison of the reconstructed inventory against candidate substrate language inventories (Hurrian, Hattic, Luwian, proto-Semitic), with a similarity metric and confidence intervals.
- A specific claim about Minoan's genetic affiliation or isolation, with the evidence required to test it.
- Predictions about what a future bilingual inscription would reveal, derived from the reconstruction.

### Fail / overclaim (do not do)
- Any phonetic value assigned to an undeciphered sign as a "decipherment" rather than a hypothesis.
- Any claim written with "is" where "may be" is more accurate.
- Any section that reads as a list of speculation without a clear "here is the evidence" paragraph.
- Any Borges-style taxonomy where categories are asserted without demonstrated empirical necessity.
- Claiming to have "solved" anything.

### Measurable pass bar
- Every phonological claim has an inline citation.
- Every "lost" sign has a hypothesis with stated confidence.
- ≥3 falsifiable predictions.
- An independent reader (Clawdia, or another auditor) can walk the argument from data to conclusion without hitting an unsupported step.

---

## Cross-cutting rules (apply to all four tasks)

1. **Every BIG task produces a JSON or machine-readable dataset, not just prose.** The analysis doc cites the dataset.
2. **Every BIG task has a reproducibility guarantee.** The scripts or queries used to produce the dataset are committed in the repo. If the data changes, the output regenerates.
3. **Every BIG task names its limitations section.** "What this atlas/audit/reconstruction does not show."
4. **No BIG task declares success in its own document.** Builder (or whoever is auditing) writes the success assessment in this file, as an appendix.
5. **Overclaim is worse than under-deliver.** A task that produces less but is honest about what it produced is higher quality than a task that claims coverage it doesn't have.

---

## Appendix: Post-hoc assessments

*(This section is filled in after each BIG task completes.)*

### BIG-1 assessment
*(not yet complete)*

### BIG-2 assessment
*(not yet complete)*

### BIG-3 assessment
*(not yet complete)*

### BIG-4 assessment
*(not yet complete)*
