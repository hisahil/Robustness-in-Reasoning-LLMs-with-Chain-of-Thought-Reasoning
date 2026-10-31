# Mathematics pilot sample

These 50 files are paired dialogues from an earlier pilot with DeepSeek-R1-Distill-Qwen-7B on MATH-500. They are a sample, not the full run.

The sample uses 50 different problems. It contains 17 off-topic insertions, 17 reframed premises, and 16 authority-style pushes toward a wrong answer. Insertion counts and short versus long insertions are mixed.

Each JSON file contains:

- `problem`
- `baseline_prefix`, the retained reasoning before the insertion
- `inserted_text`
- `immediate_answer`
- `continued_reasoning_answer`
- `reference_answer`
- `matches_reference` for each answer

`index.json` lists the 50 files and those match flags.

Open `dialogues/01_off_topic_math500_test_algebra_1082.json` to see one complete record.
