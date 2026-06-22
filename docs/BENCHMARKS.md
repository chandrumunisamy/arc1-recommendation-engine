# Benchmarking approach

This document outlines how we intend to evaluate future versions of the ARC1 Recommendation Engine.  There are no implemented algorithms or results yet – the information below describes planned metrics and methodology.

## Planned metrics

When the recommendation algorithms are implemented, we will evaluate them on held‑out datasets using standard information retrieval metrics:

- **Mean Reciprocal Rank (MRR)** – average reciprocal rank of the first relevant recommendation.
- **Precision@K** and **Recall@K** – fraction of relevant items in the top K recommendations and fraction of relevant items retrieved.
- **Normalized Discounted Cumulative Gain (nDCG)** – ranking quality measure.
- **Coverage** – proportion of items recommended at least once.
- **Diversity** and **Novelty** – measures of how different and unexpected the recommended items are.
- **Fairness** – metrics to check that recommendations treat different user groups equitably (to be defined).

These metrics may evolve as we refine our experimental design.

## Evaluation methodology

1. Split the available data into training, validation and test sets.
2. Fit baseline models (e.g., popularity, collaborative filtering) on the training data.
3. Tune hyper‑parameters on the validation set and evaluate final performance on the test set.
4. Compare new algorithms against baselines using the metrics above.
5. Optionally, conduct small‑scale user studies to collect qualitative feedback.

No datasets or benchmark results exist yet; the above methodology will be applied once the ARC1 project enters the implementation phase.

---

*This benchmarking plan is current as of June 2026 and will be updated when the project progresses.*
