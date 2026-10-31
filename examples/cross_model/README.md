# Cross-model pilot

Eleven models each produced a baseline, an off-topic insertion, and two answers for the same MATH-500 problem:

> What is the value of \(513^2 - 487^2\)?

The reference answer is 26000. Each model folder contains `task.jsonl`, `baseline.jsonl`, `injections.jsonl`, and `complete_dialogues.jsonl`. The dialogue file has two records, one insertion and two insertions.

In 21 of the 22 answer pairs, both the immediate answer and the continued-reasoning answer are `\boxed{26000}`. In the GLM-Z1-9B record with two insertions, the continued-reasoning output does not contain a gradable boxed answer. The immediate answer in that record is still 26000.

This folder shows that the workflow ran across these models. It is one problem, not a full comparison of model robustness.
