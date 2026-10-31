# Methodology

The experiment asks how robust a reasoning model is after misleading text is injected into its own generated reasoning, and whether continued reasoning restores the reference answer.

## Workflow

1. Generate a baseline solution and keep it when the final answer is correct.
2. Cut that trace and delete the remaining suffix.
3. Inject one controlled intervention. The three types are unrelated text, a reframed premise, and an authority-style push toward a wrong answer.
4. From the same prefix, generate an immediate answer and a separate answer after continued reasoning.
5. Grade both answers against the reference solution. An LLM judge is used together with deterministic answer checks.

The published examples are mathematical problems. A correct baseline answer does not mean every intermediate sentence was checked. The inserted text is unmarked. The cut shown in these examples is at the midpoint of the trace.

## What the examples are

`examples/math_pilot/` is a 50-dialogue sample from a larger 7B mathematics pilot. `examples/cross_model/` is a later check of the same workflow on one MATH-500 problem across eleven models. Neither folder is the full study.
