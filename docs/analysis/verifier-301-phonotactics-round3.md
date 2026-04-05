# Verifier V2 — *301 Phonotactics with Full GORILA Dataset

## Task
Re-run the *301 phonotactic analysis using the full GORILA sign-index dataset rather than the small surfaced sample used in Round 2.

## Sources used in this pass
- `linear_a/data/gorila_sign_index_rows.json`
- `docs/analysis/verifier-301-phonotactics.md` (Round 2 baseline)

## Method
This pass used the GORILA sign-index extraction directly.

Selection rule:
- include every row where `sign_id == "A 301"`
- include every other row where `context_numeric` or sign notes contain `301`

This yields a much broader distributional sample than the Round 2 analysis, which relied on a small surfaced list from `sign-301.md` and `morphological_analysis.json`.

## Dataset size
- total GORILA sign-index rows: **3,936**
- rows selected as relevant to *301: **102**
- rows with parseable *301 positional context: **91**

## Positional distribution
Across the parseable 91-row sample:

- **initial:** 16
- **medial:** 65
- **final:** 10

## Immediate consequence
*301 is still **predominantly medial**, but the larger dataset clearly shows that it is **not exclusively medial** and **not absent from initial position**.

That is the most important revision to the Round 2 picture.

## Immediate left neighbors of *301
Top left contexts in the parsed dataset:

| Left context | Count |
|---|---:|
| `28` | 22 |
| none / initial position | 16 |
| `58` | 10 |
| `01` | 7 |
| `37` | 5 |
| `08` | 5 |
| `07` | 4 |
| `79` | 4 |
| `59` | 4 |

### Interpretation
The strongest immediate left neighbor remains **28** (the sign corresponding to the earlier `I` observation in the canonical formula environment). So the Round 2 intuition that `I + *301` is a major pattern was real.

But the full dataset adds substantial additional environments:
- `58`
- `01`
- `37`
- `08`
- compound/ligature rows with no simple left-neighbor interpretation

This means the *301 distribution is richer than the earlier sample suggested.

## Immediate right neighbors of *301
Top right contexts in the parsed dataset:

| Right context | Count |
|---|---:|
| none / final position | 21 |
| `54` | 17 |
| `10` | 14 |
| `64` | 8 |
| `37` | 4 |
| `07` | 3 |
| `59` | 3 |
| `87` | 3 |
| `09` | 3 |

### Interpretation
The strongest right-neighbor environments are now much clearer than in Round 2:
- `54` is especially prominent in the canonical formula lane
- `10` and `64` also recur strongly in non-canonical contexts
- final position is much more visible than in the small Round 2 sample

## Ligatures / compounds / special contexts
The full GORILA dataset shows that *301 occurs in several structural modes:

### 1. Canonical formula use
Examples:
- `08-59-28-301-54-57`
- variants and neighboring rows that preserve the formula opening on sanctuary vessels

### 2. Non-canonical lexical contexts on ritual objects
Examples:
- `08-58-58-301-64-37`
- `58-06-58-301-37`
- `53-06-58-301`

### 3. Tablet / inscription contexts
Examples:
- `04-301`
- `81-301-82`
- `79-301-09-44-82-...-118`

### 4. Ligatures and compounds
Examples:
- `'28''301'`
- `28+301`
- `*301*+311`
- `'73''301'`
- `'301''351'`
- `[307+ *301*[`

### Count
Rows judged to be ligature/compound/special-composite contexts: **11**

This is one of the biggest differences from the Round 2 sample, which barely captured this category at all.

## What changed relative to Round 2

## Superseded Round 2 claims
The following Round 2 claims are now superseded by the larger dataset:

### Round 2 claim 1
> “No initial examples.”

**Round 3 result:** false under the larger dataset.  
There are **16 initial-position rows** in the broader parsed set, especially in ligature/compound or standalone A 301 contexts.

### Round 2 claim 2
> “One final example.”

**Round 3 result:** too narrow.  
There are **10 final-position rows** in the broader parsed set.

### Round 2 claim 3
> “Almost always medial (11/12).”

**Round 3 result:** still directionally true but now less absolute.  
The larger dataset is still **predominantly medial (65/91)**, but not overwhelmingly in the near-exclusive sense implied by the smaller sample.

### Round 2 claim 4
> “Strongest left context = I.”

**Round 3 result:** substantially confirmed.  
`28` remains the strongest left context in the expanded dataset.

## What still survives from Round 2

1. *301 is **not randomly distributed**.
2. It is still **most often medial**.
3. The canonical formula context remains central to its profile.
4. The strongest left-neighbor environment still corresponds to the earlier `I` observation.
5. Distributional analysis is still more secure than phonetic interpretation.

## Best current Round 3 conclusion
The strongest defensible statement now is:

> In the full GORILA-derived context set, *301 is still predominantly medial, but it also appears in initial and final position more often than the smaller Round 2 sample suggested. Its strongest left-neighbor environment remains sign 28, while its strongest right-neighbor environments include 54, 10, and 64. The larger dataset also shows that *301 participates in ligatures and administrative compounds, especially at Khania, so it cannot be treated as only a ritual formula sign.

## What this means for interpretation
This strengthens several points:

1. **Structural importance:** *301 is a real integrated sign with broad contextual life.
2. **Domain breadth:** it appears in ritual, tablets, nodules, and administrative compounds.
3. **Phonotactic caution:** earlier highly formula-weighted conclusions should be replaced by the broader Round 3 distribution.

It does **not** solve:
- phonetic value
- semantic value
- exact language-family placement

## Next useful follow-up
1. Cross-tab *301 graphic variants (`gorila_sign_variants.json`) against contextual environments.
2. Separate standalone/logogram-like A 301 rows from phonetic/word-internal rows and analyze them independently.
3. Build a document-level *301 inventory to distinguish unique words from repeated row-index sightings.

## Bottom line
Round 3 does not overthrow the earlier *301 work — it **deepens and corrects it**. The old picture of *301 as almost purely medial was an artifact of a narrow sample. The new GORILA-wide picture is stronger, broader, and more structurally informative.
