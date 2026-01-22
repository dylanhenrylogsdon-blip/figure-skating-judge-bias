# Figure Skating Judge Bias Analysis

## Overview
Figure skating scoring relies on subjective evaluations by panels of judges, raising persistent questions about bias, consistency, and fairness. This project analyzes official ISU judging data using hierarchical statistical models to decompose scoring variance into skater effects, judge effects, and random noise.

The goal is to quantify how much observed score variation is attributable to judges rather than athletes, and to identify systematic patterns of judge bias or inconsistency.

---

## Research Questions
This project focuses on the following questions:

1. How much of score variation can be explained by:
   - true skater ability,
   - individual judge effects,
   - residual randomness?
2. Are some judges systematically harsher or more lenient than others?
3. Is judging more consistent for GOE than for PCS?
4. Do judges exhibit statistically significant bias when evaluating skaters of certain countries?

---

## Data
The dataset consists of publicly available ISU competition protocols, parsed from official PDF score sheets.

Each observation corresponds to a single judge’s score for a given skater in a specific competition segment.

**Key fields include:**
- Competition and segment
- Skater identifier and nationality
- Judge identifier and nationality
- Score type (PCS or GOE)
- Raw score value

Only officially published ISU data is used.

---

## Statistical Model

### Baseline Hierarchical Model
Scores are modeled using a two-way mixed-effects framework:

Score_ij = μ + α_i + β_j + ε_ij

where:
- Score_ij is the score assigned by judge j to skater i  
- α_i represents latent skater ability  
- β_j represents judge-specific effects  
- ε_ij is random noise  

Both skater and judge effects are modeled as mean-zero random variables with their own variance components.

This formulation enables variance decomposition into skater-driven, judge-driven, and residual components.

---

## Variance Decomposition
The fitted model estimates:
- variance attributable to skater ability
- variance attributable to judge effects
- unexplained residual variance

The proportion of variance due to judges is computed as:

Judge variance / (Skater variance + Judge variance + Residual variance)

---

## Judge Bias Analysis
Judge effects are extracted from the fitted model and interpreted as systematic deviations from the panel mean after controlling for skater ability.

This approach accounts for unequal numbers of observations per judge, shrinkage toward the global mean, and noise in individual scoring decisions.

Confidence intervals are used to identify judges whose effects are statistically distinguishable from zero.

---

## Limitations
- The model assumes normally distributed errors.
- Latent skater ability is treated as time-invariant within the analyzed period.
- Causal interpretations of bias are limited by observational data.

---

## Motivation
This project combines domain expertise in figure skating with applied statistical modeling to study fairness and subjectivity in real-world evaluation systems. The methods used are broadly applicable to judging, rating, and ranking problems in sports, finance, and the social sciences.
