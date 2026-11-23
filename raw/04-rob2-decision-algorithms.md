# Source 04: RoB 2 Deterministic Decision Algorithms (Domain & Overall Risk Mapping)

- **Citation**: Sterne JAC, Higgins JPT, Savović J, Page MJ, et al. *RoB 2: Algorithms for Reaching Risk-of-Bias Judgements*. Cochrane Risk of Bias 2 Documentation (2019).
- **Official URL**: https://www.riskofbias.info/welcome/rob-2-0-tool/current-version-of-rob-2
- **Deterministic Algorithm Rules (Basis for Rule Validation Skill)**:
  - **Overall Risk of Bias Algorithm**:
    - `Low risk of bias`: The trial is judged to be at **low risk of bias for ALL domains** for this result.
    - `Some concerns`: The trial is judged to raise **some concerns in at least one domain** for this result, **but not to be at high risk of bias for any domain**.
    - `High risk of bias`: The trial is judged to be at **high risk of bias in at least one domain** for this result, OR judged to have some concerns for multiple domains in a way that substantially lowers confidence in the result.
  - **D1 Algorithm Highlights**:
    - `1.2 = N/PN` (not concealed) → **High risk**.
    - `1.2 = Y/PY` AND `1.1 = Y/PY/NI` AND `1.3 = N/PN/NI` → **Low risk**.
    - `1.2 = NI` AND `1.3 = N/PN/NI` → **Some concerns** (cannot be Low!).
    - `1.2 = NI` AND `1.3 = Y/PY` (problematic baseline/allocation imbalance) → **High risk**.
  - **D4 Algorithm Highlights**:
    - `4.1 = Y/PY` (inappropriate measurement method) → **High risk**.
    - `4.3 = Y/PY/NI` (unblinded assessor) BUT `4.4 = N/PN` (knowledge of intervention could NOT influence objective measurement) → **Low risk**!
    - `4.3 = Y/PY/NI` AND `4.4 = Y/PY/NI` AND `4.5 = N/PN` → **Some concerns**.
    - `4.3 = Y/PY/NI` AND `4.4 = Y/PY/NI` AND `4.5 = Y/PY` → **High risk**.
