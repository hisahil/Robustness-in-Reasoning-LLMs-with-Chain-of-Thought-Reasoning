# Robustness and Recovery Under Manipulated Reasoning

This project studies how robust reasoning language models are when misleading text is inserted into their own generated reasoning (Chain of Thought Reasoning). We examine when that manipulation changes the answer, and whether continued reasoning restores the correct answer or leaves the model influenced by the insertion.

The setting is mathematical problem solving. Each selected trace begins from a correct baseline solution. A controlled intervention is then injected into the open reasoning text. From that same prefix, the model produces an immediate answer and, separately, an answer after continued reasoning. Both answers are compared with the reference solution through an LLM-as-a-Judge approach.

## Experimental workflow

1. Generate a baseline solution and keep it when the answer is correct.
2. Cut the trace and delete the remaining suffix.
3. Inject one controlled intervention/attack. The three types are unrelated text, a reframed premise, and an authority-style push toward a wrong answer.
4. From the same prefix, generate an immediate answer and an answer after continued reasoning.
5. Grade both answers against the reference solution.

## What this repository contains

- `src/`: trace cutting, interventions, the two answer conditions, and grading
- `scripts/`: task preparation, baseline generation, intervention generation, paired runs, evaluation, and checks
- `configs/`: model settings and experiment scopes
- `prompts/`: baseline prompt templates
- `tests/`: automated checks for extraction, interventions, configuration, and evaluation (if you try to test it yourself, it might not work because API keys are private)
- `examples/math_pilot/`: 50 paired mathematics dialogues from an earlier pilot run (these here are just a small sample)
- `examples/cross_model/`: a short pilot in which eleven models each produced a baseline, an intervention, and both answers.

Model weights and full experimental outputs are not included. The dialogues here are selected examples from earlier pilots.

## Mathematics pilot

`examples/math_pilot/` contains 50 paired dialogues from a pilot with DeepSeek-R1-Distill-Qwen-7B on MATH-500. The dialogues are spread across different problems and the three intervention types.

Each record shows:

- the problem,
- the inserted text,
- the immediate answer,
- the answer after continued reasoning,
- the reference solution and whether each answer matched it.

These 50 dialogues are a readable sample from a larger mathematics pilot. As noted before, they are not the full run!!!

## Cross-model pilot

`examples/cross_model/` contains a later check across eleven models:

- DeepSeek-R1-Distill-Qwen, at 1.5B, 7B, 14B, and 32B
- DeepSeek-R1-Distill-Llama-8B
- EXAONE-Deep-32B
- GLM-Z1-9B
- Nemotron-Nano-8B
- OLMo-3-7B-Think
- Phi-4-reasoning-plus
- QwQ-32B

Every model received the same MATH-500 problem, \(513^2 - 487^2\), whose reference answer is 26000. The intervention was a short off-topic passage. For each model the folder keeps the baseline, the inserted text, and the two answers.

This run shows that the workflow can be carried out across these models. In the GLM-Z1-9B record with two insertions, the continued-reasoning output does not contain a gradable answer.

## How to inspect an example

Open `examples/math_pilot/README.md` for the 50 mathematics dialogues, and `examples/cross_model/README.md` for the eleven-model check. A single mathematics record is enough to see the problem, the manipulation, both answers, and the grade.

## Local checks

From the repository root, this prints the pipeline stages and does not launch them:

```bash
python scripts/run_pipeline.py --scope mini_run --dry-run
```

The automated tests are:

```bash
python -m pytest tests -q
```

A real generation run needs a CUDA machine, the packages in `requirements.txt`, and model weights. Intervention generation and judging also need an API key. Copy `.env.example` to `.env` and fill in the key locally. Do not commit `.env`.

## Limitations

The published dialogues are samples from earlier pilots. A correct baseline answer does not mean every intermediate sentence was checked. The inserted text is unmarked, so it is not the same thing as a labelled message from a tool or another agent. The cut used here is at the midpoint of the trace. Differences between models reflect each model's own baseline and its own intervention text.

## Next

The planned extension is broader model and task coverage, additional controls, and more systematic robustness checks. A more full version with more extensive code and results may be published in the future.
