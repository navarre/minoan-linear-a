## Checkpoint 2026-04-03 22:08 EEST
- Status: IN PROGRESS
- Current section: Quantitative verification against corpus data
- Completed sections: [Assignment intake and source inventory, Analysis document review]
- Next: Verify counts/claims with corpus JSON and targeted PDF extraction; then challenge conclusions and draft review

## Checkpoint 2026-04-04 07:xx EEST
- Status: DRAFT REVIEW COMPLETE
- Completed in this pass:
  - Re-verified core repo counts from `linear_a/data/`:
    - `corpus.json` = 1,880 documents
    - `signs.json` = 386 signs
    - `A301` = 48 occurrences on 48 documents
    - `morphological_analysis.json` = 758 extracted forms, 210 suffixed, 27.7%, 8 suffixes
    - `morphological_analysis.json` also confirms 27 stacking patterns and 34 reduplicated forms
  - Reviewed analysis docs across the current April 2026 set
  - Wrote `docs/analysis/verifier-review-2026-04.md`
- Main findings from this pass:
  - real quantitative work exists and is recoverable
  - biggest immediate issue is mixed denominators / mixed taxonomies across documents
  - several strong claims should be reframed as data-verified vs source-reported vs interpretive
- Remaining work:
  - targeted PDF/source verification for the highest-profile published claims
  - normalization of count provenance across analysis docs

## Checkpoint 2026-04-05 06:xx EEST
- Status: R11 CHECK ATTEMPTED / BLOCKED
- State change:
  - `references/gorila/vol5/` now exists, so the formerly missing source directory has appeared.
- What I did:
  - confirmed vol. 5 contains 524 JPG files
  - sampled multiple tail-end pages where the sign plates should normally appear
  - checked those pages with vision to see whether they were actual plate pages
- Result:
  - sampled late pages are placeholder/watermark images rather than readable GORILA sign plates
  - R11 is therefore still blocked in practice even though the directory now exists
- Output written:
  - `docs/analysis/verifier-gorila-signs.md`
- One-line finding:
  - **Meaningful state change but still blocked:** vol. 5 arrived, yet the current JPG payload does not appear to contain usable sign-plate pages.

## Checkpoint 2026-04-05 10:xx EEST
- Status: V1 COMPLETE
- Task: Audit the rewritten `gorila-301-findings.md` against `linear_a/data/gorila_sign_index_rows.json`
- Verified directly:
  - A 301 row count = 35
  - the canonical formula opening is supported by converging `AB 28` / `AB 54` / `AB 57` rows rather than one single plain-string row
  - KH administrative compounding with *301 is real (`*301*+311`, `'73''301'`, `'301''351'`)
- Main correction/caution:
  - exact AP Za 1 normalization still needs softer wording than a single fully settled normalized reading
  - exact total attestation count should remain approximate unless explicitly deduped across sign rows
  - some extraction-normalization artifacts remain visible in raw refs (for example `SY Zm` vs expected `SY Za`)
- Output updated:
  - `docs/analysis/gorila-301-findings.md` (verifier audit section corrected to match raw row evidence)

## Checkpoint 2026-04-05 10:xx EEST
- Status: V2 COMPLETE
- Task: Re-run *301 phonotactics using the full GORILA sign-index dataset
- Dataset size:
  - 102 relevant rows selected
  - 91 rows parseable for positional context
- Main results:
  - positional distribution = 16 initial / 65 medial / 10 final
  - strongest left context remains sign 28
  - strongest right contexts are 54, 10, and 64
  - 11 ligature/compound rows now visible in the broader dataset
- Superseded Round 2 claims:
  - *301 is not non-initial
  - final-position examples are more numerous than the small Round 2 sample suggested
  - Round 2 remains historically useful but is now superseded in breadth
- Output written:
  - `docs/analysis/verifier-301-phonotactics-round3.md`

## Checkpoint 2026-04-06 00:xx EEST
- Status: V3 COMPLETE
- Task: Audit Cowork's GORILA extraction files
- Main results:
  - `gorila_sign_variants.json`: A 301 spot-check confirmed (11 variants across vol. 5 pp. 45-46)
  - `gorila_sign_index_rows.json`: 4/4 sampled rows were visually consistent with cited sign-index pages
  - `gorila_page_map.json`: mostly right, but sample included real boundary-type misclassifications (`prelim` / `section_divider` / `blank`)
  - `gorila_concordances_full.json`: main verifier problem is missing direct source-page provenance for each entry, making random-entry audit hard to reproduce from the JSON alone
- Main caution/blocker:
  - concordance extraction is not shown false by this pass, but it is **insufficiently source-addressable** for clean verifier auditing
- Output written:
  - `docs/analysis/verifier-gorila-extraction-audit.md`
