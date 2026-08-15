# Domain Profile

<!--
HOW TO USE: Fill this in manually OR let /discover (interactive interview) generate it.
All agents read this file to calibrate their field-specific behavior.
Delete sections that don't apply. Add sections specific to your field.
If no field is specified, agents default to applied economics.
-->

## Field

**Primary:** Marketing / Consumer Behavior — AI-washing (misrepresentation or exaggeration of AI capability in consumer-facing product and corporate claims), studied with text-as-data and capital-market-reaction methods.
**Adjacent subfields:** Finance (disclosure, misrepresentation, event studies), Accounting (textual analysis of filings, MD&A), Strategy/Management (symbolic vs. substantive adoption, decoupling), Information Systems (AI adoption measurement).

**Analogy base:** Treat AI-washing as the AI-era counterpart to greenwashing — borrow measurement and identification approaches from that literature (claim–substance gaps, enforcement-action event studies, textual disclosure analysis) and adapt them to AI claims.

---

## Target Journals (ranked by tier)

<!-- The Orchestrator uses this for journal selection. The Librarian prioritizes these in searches. -->

| Tier | Journals |
|------|----------|
| Premier finance/accounting | Journal of Finance (JF), Journal of Financial Economics (JFE), Review of Financial Studies (RFS), Journal of Accounting Research (JAR), Journal of Accounting and Economics (JAE), The Accounting Review (TAR) |
| Strong field (finance/accounting) | Management Science, Review of Finance, Review of Accounting Studies, Contemporary Accounting Research (CAR), Journal of Corporate Finance |
| Marketing (secondary target, given consumer angle) | Journal of Marketing (JM), Journal of Marketing Research (JMR), Marketing Science |
| Specialty / interdisciplinary | Journal of Consumer Research (JCR), Strategic Management Journal (SMJ), Information Systems Research (ISR) |

---

## Common Data Sources

<!-- The Explorer prioritizes these. The explorer-critic knows their quirks. -->

| Dataset | Type | Access | Notes |
|---------|------|--------|-------|
| SEC EDGAR filings (10-K, 10-Q, 8-K, press releases) | Text/admin | Public | Source for "AI claim" text extraction; MD&A and product-description sections most relevant |
| SEC litigation releases / AAER database | Admin | Public | Ground-truth AI-washing enforcement actions (e.g., 2024 Delphia and Global Predictions cases) — small-N but high-credibility labels |
| Earnings call transcripts (Capital IQ / Refinitiv StreetEvents) | Text/panel | Restricted (institutional license) | Management AI claims in a less scripted setting than filings |
| Product marketing pages / web-scraped product listings / Common Crawl | Text | Public (scraping) | Consumer-facing "AI-powered" claims — the core AI-washing construct at the product level |
| USPTO / PatentsView patent data | Admin/panel | Public | Proxy for genuine AI capability investment (AI-classified patents) |
| Job postings (Lightcast/Burning Glass, or LinkedIn where licensed) | Admin/panel | Restricted (license) | AI-hiring intensity as a capability proxy (cf. Babina et al. 2024 approach) |
| CRSP/Compustat | Panel | Restricted (WRDS) | Stock returns, firm fundamentals for market-reaction and control variables |
| FTC consumer complaint data / product review platforms (Amazon, Trustpilot) | Text/admin | Public (complaints) / scraping (reviews) | Consumer-side outcome measures — trust, complaints, review sentiment following AI claims |
| I/B/E/S analyst forecasts | Panel | Restricted (WRDS) | Analyst reaction to AI claims, as a sophisticated-investor benchmark against retail market reaction |

---

## Common Identification Strategies

<!-- The Strategist considers these first. The strategist-critic knows field-specific threats. -->

| Strategy | Typical Application | Key Assumption to Defend |
|----------|-------------------|------------------------|
| Event study around SEC AI-washing enforcement actions | Market/behavioral response to enforcement (own-firm and industry spillovers) | No confounding news in the event window; enforcement timing is not anticipated/endogenous to firm performance |
| Claim–capability gap ("AI-washing score") regressed on outcomes | Firm- or product-level panel regression of the text-derived claim/capability gap on stock returns, sales, or consumer trust | The gap measure isolates misrepresentation rather than legitimate early-stage/forward-looking AI investment |
| Difference-in-differences around exogenous AI-hype shocks (e.g., ChatGPT launch, Nov 2022) | Shock to incentives to make AI claims, compared across ex ante AI-exposed vs. non-exposed firms/products | Parallel trends pre-shock; the shock affects claim incentives but not capability itself in the short run |
| Matched-sample comparison: high-claim/low-capability vs. genuine AI adopters | Cross-sectional comparison on market and consumer outcomes | Matching on observables (industry, size, prior AI activity) removes confounding; no unobserved selection into "washing" |
| Instrumental variable using industry-level AI attention/media hype | Isolates the claim-incentive channel from underlying capability | Instrument affects claims only through hype/incentive channel, not through capability or other confounds (exclusion restriction is the hardest sell to referees) |

---

## Field Conventions

<!-- The Coder and Writer follow these. The writer-critic checks for them. -->

- Construct the AI-washing measure as a **gap or residual**: `AIWashing_it = AIClaim_it - AICapability_it` (or the residual from regressing claims on capability proxies), not claims alone — referees will otherwise conflate washing with genuine adoption.
- Validate any LLM/dictionary-based text classification against a human-annotated subsample; report classifier precision/recall, not just the final score.
- Use event-study methodology (CAR, abnormal returns) for market-reaction results; report both raw and risk-adjusted (Fama-French/Carhart) abnormal returns.
- Cluster standard errors at the firm level for firm-panel regressions; two-way cluster (firm + time) when pooling across many events/periods.
- Always address reverse causality explicitly: are firms making AI claims *because of* stock price or investor pressure, rather than the claims causing market reactions?
- Distinguish "AI-washing" from legitimate marketing optimism / forward-looking statements (safe-harbor language) — referees will demand this distinction be operationalized, not just asserted.
- Report robustness to alternative claim-intensity measures (keyword/dictionary count vs. LLM classification vs. human coding) and to placebo/false-event dates.
- Where consumer-level outcomes are used (trust, purchase intent, complaints), report both observational (review/complaint data) and, if available, experimental/survey corroboration.

---

## Notation Conventions

<!-- The Writer and writer-critic enforce these. -->

| Symbol | Meaning | Anti-pattern |
|--------|---------|-------------|
| $AIClaim_{it}$ | Text-derived AI-claim intensity for firm/product $i$ at time $t$ (filings, press releases, or marketing text) | Don't use "AI score" inconsistently between claim-side and capability-side measures |
| $AICapability_{it}$ | Actual AI capability proxy for firm $i$ at time $t$ (AI-classified patents, AI job postings, R&D) | Don't conflate with $AIClaim_{it}$ — always keep claim and capability as separate constructs |
| $Washing_{it}$ | AI-washing gap, $Washing_{it} = AIClaim_{it} - \widehat{AICapability}_{it}$ (or regression residual) | Don't call raw $AIClaim_{it}$ "washing" without netting out capability |
| $CAR_{i}(\tau_1,\tau_2)$ | Cumulative abnormal return for firm $i$ over event window $[\tau_1,\tau_2]$ | Don't use $CAR$ without specifying the estimation window and benchmark model |
| $Y_{it}$ | Generic outcome (returns, sales, trust score) for unit $i$ at time $t$ | Don't use $y$ without subscripts in panel specifications |
| $Enforce_{i,t}$ | Indicator for SEC/regulatory AI-washing enforcement action against firm $i$ at time $t$ | Don't reuse for industry-wide enforcement waves — index those separately as $Enforce^{industry}_{j,t}$ |

---

## Seminal References

<!-- The Librarian ensures these are cited when relevant. The strategist-critic knows their methods. -->

| Paper | Why It Matters |
|-------|---------------|
| Delmas & Burbano (2011), "The Drivers of Greenwashing" | Foundational conceptual framework for claim–substance decoupling; direct template for defining "AI-washing" |
| Marquis, Toffel & Zhou (2016), "Scrutiny, Norms, and Selective Disclosure: A Global Study of Greenwashing" | Methodological template for measuring selective/misleading disclosure at scale |
| Loughran & McDonald (2011), "When Is a Liability Not a Liability? Textual Analysis, Dictionaries, and 10-Ks" | Standard for finance-style textual analysis of corporate filings; dictionary construction and validation |
| Babina, Fedyk, He & Hodson (2024), "Artificial Intelligence, Firm Growth, and Product Innovation" (JFE) | Establishes job-postings-based AI investment/capability measurement — direct source for the capability-side proxy |
| SEC v. Delphia (USA) Corp. and Global Predictions Inc. (March 2024 enforcement actions) | First formal "AI-washing" enforcement actions; primary source of ground-truth labeled events |
| Milgrom (1981), "Good News and Bad News: Representation Theorems and Applications" | Cheap-talk/disclosure theory underpinning why unverifiable AI claims can be credible or not |

---

## Theoretical Foundational References

<!-- The Theorist and theorist-critic default to these anchors when building or reviewing a theory section.
     Only needed if the paper has a formal theory section (econometric methods, theory+empirics,
     structural identification, or methodological reduced-form).
     Leave empty to fall back to the generic econometric theory defaults baked into the theorist agent. -->

| Topic | Anchor references |
|-------|------------------|
| *(none yet — this project is designed as applied text-as-data + event-study, no formal theory section planned)* | Leave empty; theorist agent falls back to generic econometric-theory defaults if a theory section is added later (e.g., a signaling/cheap-talk model of disclosure). |

---

## Paper Author Team

<!-- Used by the theorist-critic to calibrate respect. If the authors are themselves among the reference
     literature on a topic, the critic avoids lecturing them on their own contributions.
     List author surnames + the topics they are foundational on. -->

| Author | Foundational on |
|--------|----------------|
| *(fill in once co-author team is finalized)* | |

---

## Field-Specific Referee Concerns

<!-- The domain-referee and methods-referee watch for these. -->

- "How do you distinguish AI-washing from legitimate marketing optimism or forward-looking statements?" — must be operationalized in the measure, not just asserted in text.
- "Your AI-claim measure could just capture salience/attention rather than deception" — address with the claim-minus-capability gap, not raw claim counts.
- "Selection: which firms/products choose to make AI claims in the first place?" — always a concern given non-random adoption of AI marketing language.
- "Why not just use SEC/FTC enforcement actions as ground truth?" — anticipate this; enforcement samples are small-N and non-random (only egregious/detected cases), so they can validate but not replace the broader text-based measure.
- "Reverse causality — are firms making AI claims because of prior stock price or investor pressure, rather than claims driving reactions?" — must be addressed directly, e.g. via event timing or exogenous shocks.
- "External validity — U.S. public disclosure-heavy sample may not generalize to private firms or non-U.S. markets," especially relevant given a Norway/EU-based research team; consider whether an EU disclosure angle (e.g., EU AI Act transparency requirements) strengthens or narrows the claim.
- "Confusion with genuine early-stage AI adoption that hasn't yet materialized into measurable capability" — capability proxies (patents, hiring) lag actual deployment, so timing assumptions need defending.

---

## Quality Tolerance Thresholds

<!-- Customize for your domain's standards. Used by quality.md. -->

| Quantity | Tolerance | Rationale |
|----------|-----------|-----------|
| Point estimates | 1e-6 | Standard numerical precision for replication checks |
| Standard errors | 1e-4 | Allows for minor solver/bootstrap variability |
| Abnormal return (CAR) estimates | ± 1 basis point (1e-4) | Standard event-study replication tolerance |
| Text-classification agreement (LLM vs. human-coded subsample) | ≥ 0.80 Cohen's kappa | Minimum acceptable validation threshold for the AI-claim/washing measure before it can be used as the paper's core construct |
