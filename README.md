# Figure Skating Judge Bias Analysis
Overview

Figure skating scoring relies on subjective evaluations by panels of judges, raising persistent questions about bias, consistency, and fairness. This project analyzes official ISU judging data using hierarchical statistical models to decompose scoring variance into skater effects, judge effects, and random noise.

The goal is to quantify how much observed score variation is attributable to judges rather than athletes, and to identify systematic patterns of judge bias or inconsistency.

Research Questions

This project focuses on the following questions:

How much of score variation can be explained by:

true skater ability,

individual judge effects,

residual randomness?

Are some judges systematically harsher or more lenient than others?

Is judging more consistent for GOE than for PCS?

Do judges exhibit statistically significant bias when evaluating skaters of certain countries?

Data

The dataset consists of publicly available ISU competition protocols, parsed from official PDF score sheets.

Each observation corresponds to a single judge’s score for a given skater in a specific competition segment.

Key fields include:

Competition and segment

Skater identifier and nationality

Judge identifier and nationality

Score type (PCS or GOE)

Raw score value

Only officially published ISU data is used.

Statistical Model
Baseline Hierarchical Model

Scores are modeled using a two-way mixed-effects framework:

𝑦
𝑖
𝑗
=
𝜇
+
𝛼
𝑖
+
𝛽
𝑗
+
𝜖
𝑖
𝑗
y
ij
	​

=μ+α
i
	​

+β
j
	​

+ϵ
ij
	​


where:

𝑦
𝑖
𝑗
y
ij
	​

 is the score assigned by judge 
𝑗
j to skater 
𝑖
i

𝛼
𝑖
∼
𝑁
(
0
,
𝜎
skater
2
)
α
i
	​

∼N(0,σ
skater
2
	​

) represents latent skater ability

𝛽
𝑗
∼
𝑁
(
0
,
𝜎
judge
2
)
β
j
	​

∼N(0,σ
judge
2
	​

) represents judge-specific effects

𝜖
𝑖
𝑗
∼
𝑁
(
0
,
𝜎
2
)
ϵ
ij
	​

∼N(0,σ
2
) is random noise

This formulation enables variance decomposition into skater-driven, judge-driven, and residual components.

Variance Decomposition

The fitted model estimates:

𝜎
skater
2
σ
skater
2
	​

: variance attributable to skater ability

𝜎
judge
2
σ
judge
2
	​

: variance attributable to judge effects

𝜎
2
σ
2
: unexplained variance

The proportion of variance due to judges is computed as:

𝜎
judge
2
𝜎
skater
2
+
𝜎
judge
2
+
𝜎
2
σ
skater
2
	​

+σ
judge
2
	​

+σ
2
σ
judge
2
	​

	​

Judge Bias Analysis

Judge effects are extracted from the fitted model and interpreted as systematic deviations from the panel mean after controlling for skater ability.

This approach accounts for:

Unequal numbers of observations per judge

Shrinkage toward the global mean

Noise in individual scoring decisions

Confidence intervals are used to identify judges whose effects are statistically distinguishable from zero.

Extensions

Additional analyses include:

Separate modeling of PCS and GOE to compare inter-judge reliability

Country-based interaction terms to test for national bias

Robustness checks via subsampling and bootstrap resampling

Limitations

The model assumes normally distributed errors.

Latent skater ability is treated as time-invariant within the analyzed period.

Causal interpretations of bias are limited by observational data.

Future Work

Potential extensions include:

Time-varying judge effects

Bayesian hierarchical modeling

Cross-season skill evolution models

Network analysis of judging panels

Repository Structure
figure-skating-judge-bias/
│
├── data/
│   ├── raw/
│   └── cleaned/
├── notebooks/
│   ├── exploration.ipynb
│   ├── modeling.ipynb
│   └── results.ipynb
├── src/
│   ├── parsing.py
│   ├── models.py
│   └── utils.py
├── figures/
└── README.md

Motivation

This project combines domain expertise in figure skating with applied statistical modeling to study fairness and subjectivity in real-world evaluation systems. The methods used are broadly applicable to judging, rating, and ranking problems in sports, finance, and the social sciences.
