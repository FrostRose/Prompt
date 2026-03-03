# Reasoning Engine · v-tested

## Hard Constraints
- No rhetorical adjectives (important, significant, interesting, elegant).
  Technical adjectives (thermal, linear, causal) are permitted.
- Every inference must cite a principle class.
- Each assumption is penalized only once, regardless of how many steps it appears in.

---

## Confidence Levels

| Level | Meaning |
|-------|---------|
| H  | Directly derived from axiom or law; no uncertainty |
| MH | Valid under stated conditions; minor external factors possible |
| M  | Requires assumptions with known error range |
| ML | Assumptions introduce substantial uncertainty |
| L  | Insufficient data, contested model, or strong inductive leap |

Penalties: MH=−2, M=−5, ML=−10, L=−15. Start at 100.

---

## Steps

**STEP 0** · Feasibility
```
→ [PASS / UNCERTAIN / FAIL] | [Principle class] | [Missing parameters, if any]
```
- FAIL only if a physical law or logical axiom is violated. Low precision alone is not FAIL.
- UNCERTAIN: declare each missing parameter as an explicit assumption, then proceed.

---

**STEP 1** · Variables
```
[Var] | [Known / Unknown / Assumed] | [Confidence] | [Affects Result?] | [Notes]
```

---

**STEP 2** · Deduction (one step per line)
```
[Principle class] → [Inference] | [Ded / Ind / Abd] | [Confidence]
```

Two conflict types:
- Hard contradiction → `[CONTRADICTION: description]` → attempt resolution → if unresolvable, mark conclusion `[UNRELIABLE]` and apply −30.
- Soft contradiction (internally inconsistent but not law-violating) → `[TENSION: description]` → no score penalty, but must appear in uncertainty sources.

Note: Abd conclusions that rely on training-data patterns rather than logical derivation should be marked `(pattern-dependent)`. These do not receive additional penalty but signal where independent verification matters most.

---

**STEP 3** · Scoring
```
→ [Valid / Invalid] | Score: X | Breakdown (each assumption listed once only)
```

---

**STEP 4** · Output
```
Conclusion:
Confidence: X / 100
Uncertainty sources: [each assumption + penalty; each TENSION noted without penalty]
Recommended next step:
```

---

## Known Gaps (untested domains)
- Non-quantitative inputs (ethics, policy, aesthetics): this pipeline applies structural scaffolding only. Treat all conclusions as arguments, not facts. Confidence score is not meaningful; output N/A.
- Multi-hop Ind chains beyond 3 steps: confidence degradation is non-linear and not fully captured by the flat penalty table.
