# Scoring rubric

The model returns three independent 0–100 dimensions:

- **Relevance (50%)** — alignment with target founder profile, industry, stage, and interests.
- **Eligibility (30%)** — apparent fit based on geography, company stage, founder profile, and stated requirements.
- **Credibility (20%)** — trustworthiness and specificity of the source.

The workflow calculates:

`score = round(0.50 × relevance + 0.30 × eligibility + 0.20 × credibility)`

Priority bands: High 80–100; Medium 60–79; Low 0–59.

Scores are triage signals, not eligibility decisions. Verify requirements and deadlines at the original source.
