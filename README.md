Pulsar Conformal Triage Pipeline
A statistical systems software pipeline that applies Mondrian Conformal Prediction (CP) to high-throughput radio astronomy data streams. This architecture guarantees a class-conditional error bound ($1 - \alpha = 0.95$) to systematically triage pulsar telemetry, drastically reducing downstream computational infrastructure costs.

The Problem
Modern radio telescopes generate massive pipelines of candidate events, the vast majority of which are dead noise (RFI). Standard Machine Learning baselines (e.g., LightGBM) optimize for global accuracy, causing them to systematically drop rare minority-class signals (Pulsars) due to massive class imbalance (~1.3% positive class ratio).
Heuristic reweighting (Balanced ML) controls False Negatives but spikes False Positives, wasting expensive telescope pointing hours on unvetted noise anomalies.

The Solution: Mondrian Conformal Co-Triage -This software applies a class-conditional non-conformity score framework to split data processing into mathematical certainty tiers:

1. Definitive Noise (Discard): Instantly filtered out with mathematical guarantees, saving downstream compute costs.
2. Definitive Pulsar (Telescope Pointing): Automatically queued for high-priority confirmation.
3. Ambiguous (Defer): Buffered for human-in-the-loop review.

Empirical Performance Gains (HTRU2 & MedLat Replications)
Target Coverage Floor: 95.00%
Standard Marginal CP Pulsar Coverage: ~2.38% (Catastrophic coverage failure under minority imbalance)
Mondrian Class-Conditional Pulsar Coverage: 96.05% (Statistically valid)
Infrastructure Cost Vector: Mondrian Co-Triage mathematically out-efficiencies Balanced Heuristic baselines whenever the operational penalty of missing a true pulsar exceeds 2 telescope pointing hours.

Repository Architecture
`medlat_data_pipeline.ipynb`: High-throughput binary array parsing from `.phcx` / `.xml` telescope files to extract statistical telemetry (skewness, kurtosis, profile moments).
`main_triage_pipeline.ipynb`: The core Conformal Triage engine, quantile calibration loops, and cost-vector evaluation profiles.
`baseline_model.ipynb`: Evaluation metrics for uncalibrated LightGBM and Logistic Regression models.

Dependencies & Core Stack
Python 3.10+
LightGBM / Scikit-Learn
Scipy / Numpy / Pandas
Matplotlib (Cost-efficiency visualization)
