# Instructions for Verifier (Clawdia) — Round 2

## Context

You are Bot B (Verifier/Challenger) on the Linear A Research Project.
Repository: https://github.com/navarre/minoan-linear-a
Branch: master

The Builder (Bot A) has produced 9 analysis documents in `docs/analysis/`. Your Round 1 review (`verifier-review-2026-04.md`) correctly identified denominator and labeling issues. That editorial feedback is noted and will be addressed.

**Round 2 is different.** This round is about RESEARCH, not editing. You have 8 specific research tasks below. Each one requires reading source PDFs, running analysis, and producing findings.

## How to work

1. `git pull origin master` before starting
2. Read the specific files cited in each task
3. Do the analysis described
4. Write your findings to the specified output file
5. `git add` your output files, `git commit -m "Verifier: [task description]"`, `git push origin master`
6. Do NOT skip tasks. Do NOT substitute editorial commentary for research.

## Your source files

All reference PDFs are in `references/core/` and `references/comparative/`. Key files:
- `references/core/Younger_2024_Linear_A_Lexicon.pdf` — the complete Linear A word list
- `references/core/Younger_2024_Linear_A_Updates.pdf` — corrections to tablet readings
- `references/core/Salgarella_2022_Linear_A_OCD.pdf` — definitive LA reference article
- `references/core/Steele_2018_Pre_Alphabetic_Scripts.pdf` — cross-script relationships
- `references/core/Schurr_1973_KI_KI_RA_JA.pdf` — ki-ro morphology (in German)
- `references/core/RILA_Supplement_2025_Index_Only.pdf` — 2025 supplement table of contents
- `references/comparative/van_soesbergen_hurrian/` — 10 Hurrian hypothesis volumes

Corpus data is in `linear_a/data/`:
- `glossary.json` — 52-word glossary with confidence scores
- `signs.json` — 386 sign entries
- `corpus.json` — 1,880 document records (large file, use grep/search)
- `corpus_structured.json` — structured corpus data
- `morphological_analysis.json` — computational morphology results

Analysis documents to reference are in `docs/analysis/`.

---

## TASK R1: Test the -SE suffix as ergative marker

**Read:** `references/core/Younger_2024_Linear_A_Lexicon.pdf` (extract text with pdftotext)
**Read:** `linear_a/data/morphological_analysis.json`
**Read:** `docs/analysis/morphology.md`

**Do this:**
1. Extract every word ending in -SE from Younger's Lexicon
2. For each word, note its position on the tablet (heading? first entry? last entry? after ku-ro?)
3. Check: do -SE words appear in AGENT positions (the entity doing something) or PATIENT positions (the thing being acted upon)?
4. In Hurrian, the ergative suffix -s(e) marks the agent of transitive verbs. If LA -SE is ergative, words ending in -SE should appear as subjects/agents, NOT as objects or commodities.
5. Count: how many -SE words are personal names vs. transaction terms vs. commodities?

**Output:** `docs/analysis/verifier-se-ergative.md`

---

## TASK R3: Extract all data from RILA 2025 index

**Read:** `references/core/RILA_Supplement_2025_Index_Only.pdf` (extract with pdftotext)

**Do this:**
1. Extract the complete "Concordance générale" — this lists every document ID in the supplement
2. Extract the "Concordance typologique" — document IDs by type
3. Extract the "Concordance géographique" — document IDs by site
4. Extract the "Concordance muséographique" — which museum holds each document
5. Produce a JSON file mapping every extractable document ID to its type, site, and museum

**Output:** `linear_a/data/rila_2025_concordances.json` AND `docs/analysis/verifier-rila-extraction.md`

---

## TASK R4: Phonotactic constraints on *301

**Read:** `linear_a/data/morphological_analysis.json`
**Read:** `docs/analysis/sign-301.md`

**Do this:**
1. List every word containing *301 (from sign-301.md and morphological_analysis.json)
2. For each word, note what syllable comes BEFORE *301 and what comes AFTER
3. Build a table: which syllables can precede *301? Which can follow?
4. Compare these constraints against the known syllables. Are there gaps? (e.g., does *301 never follow a certain consonant class?)
5. If *301 represents a pharyngeal/laryngeal, what phonotactic patterns would we expect? Do the data match?
6. Check: does *301 appear word-initially in any word? Word-finally? Only medially?

**Output:** `docs/analysis/verifier-301-phonotactics.md`

---

## TASK R6: Cross-site dialect variation

**Read:** `linear_a/data/glossary.json` (check site distributions for each word)
**Read:** Younger's Lexicon (extract with pdftotext from `references/core/Younger_2024_Linear_A_Lexicon.pdf`)

**Do this:**
1. For each of the top 20 most frequent words, list which sites they appear at
2. Are there words that appear ONLY at one site? (These may be local vocabulary or dialect markers)
3. Do Khania (KH) tablets use different vocabulary from Haghia Triada (HT)?
4. Do the suffix frequencies differ by site? (e.g., is -SE more common at one site?)
5. The libation formula — do different sites use different variants? (word 2 is known to vary by location)

**Output:** `docs/analysis/verifier-dialect-variation.md`

---

## TASK R7: Luwian contact beyond the formula

**Read:** `docs/analysis/libation-formula.md`
**Read:** `docs/analysis/substrate-words.md`
**Read:** `docs/analysis/hypothesis-testing.md`

**Do this:**
1. ja-sa-sa-ra-me is confirmed as Luwian. DU-PU2-RE may connect to Hittite Tabarna. Are there OTHER words in the LA corpus that could be Anatolian/Luwian borrowings?
2. Search Younger's Lexicon for any words that resemble known Luwian, Hittite, or Lycian vocabulary
3. Check: is the Anatolian contact limited to religious vocabulary? Or does it appear in administrative terms too?
4. If Luwian contact is ONLY in the religious register, what does this tell us about the relationship? (Trade? Religious prestige borrowing? Shared priesthood?)

**Output:** `docs/analysis/verifier-luwian-contact.md`

---

## TASK R8: Propose a new testable hypothesis about the Minoan language

**Read:** All documents in `docs/analysis/`

**Do this:**
1. Review all findings from Builder and your own research tasks
2. Propose at least ONE new hypothesis about the Minoan language that:
   - Is specific (not vague)
   - Is falsifiable (can be tested against data)
   - Has not been proposed in the existing analysis documents
   - Makes a prediction that can be checked
3. Explain how to test it and what data would confirm or refute it

**Output:** Include in `docs/analysis/verifier-review-round2.md`

---

## TASK C-FIX: Create count provenance table

This is your own recommendation from Round 1. Do it.

**Do this:**
1. Create a table mapping every major number in the project to its source
2. Include: 1,880 / 1,534 / 758 / 1,463 / 386 / 389 / 315 / 178+164+47 / 48 / 52 / 21

**Output:** `docs/analysis/count-provenance.md`

---

## Summary of deliverables

You should produce these files:
1. `docs/analysis/verifier-se-ergative.md`
2. `linear_a/data/rila_2025_concordances.json` + `docs/analysis/verifier-rila-extraction.md`
3. `docs/analysis/verifier-301-phonotactics.md`
4. `docs/analysis/verifier-dialect-variation.md`
5. `docs/analysis/verifier-luwian-contact.md`
6. `docs/analysis/verifier-review-round2.md` (with new hypothesis)
7. `docs/analysis/count-provenance.md`

Commit and push each task as you complete it. Do not batch everything into one commit.
