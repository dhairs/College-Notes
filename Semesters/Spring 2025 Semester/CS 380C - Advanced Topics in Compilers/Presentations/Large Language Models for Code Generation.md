## Evaluation

### What does it mean to do a good job?

Generated code matches a reference solution?

Generated code *resembles* a reference solution? (CodeBLEU)

Generate code passes some test cases: pass@1, pass@k.

Is the generated code algorithmically optimal? Test against competitive programming problems.

Does the generated code compile and pass static analysis checks?

Is the generated code aesthetically pleasing? (HumanEval)

## Training

### Data Collection

Data set is mostly source code but also an English code related natural language corpus
- Public repositories on GitHub
- Github Markdown and StackExchange

Pre-trained on repository-level code to better learn the nuances of file-dependencies

Filter code
- **Syntax**: syntax errors and StarCoder filtering rules
- **Semantic**: filter out code that has poor readability and low modularity

Dependency parsing: parse dependencies between files and then arrange them in the proper order.

Repository-Level De-depulication: remove "duplicate" repositories.

### Techniques

Next Token Prediction (NTP): given an entry, predict what comes next. Goal is to predict the subsequent token based on the provided context.

Fill in the Middle (FIM).

### Grounding

Want to connect code with natural language. So we also collect tutorials, blog posts, documentation, StackOverflow answers, etc. Use pull requests, commit messages, GitHub discussions to provide context to the code. Computer Science textbooks can be used as well.

Want to also make this model aware of the world and logically sound, so we train it on large text corpus (the same way as with standard LLMs) and on math word problems (to teach it logic).

## Post Training

### Alignment

Instruction fine tuning: retrain the model on instructions with correct output. This is usually with a manually curated dataset.

Chain-of-Thought: add the phrase "You need to write a step-by-step outline and then write the code" following the initial prompt. This allows it to think through the actual problems with more inference time.

### Synthetic Instruction Datasets

We can use LLMs to generate instruction datasets in instruction, response pairs.

1. Pick a code snippet from GitHub
2. Ask the LLM to provide an instruction that matches this code
3. Ask the LLM to provide the response to the instruction
4. Ask the LLM to score this pair of instruction and response
5. Create a dataset of only the highest scoring pairs.

### Multilingual Code Generation

The datasets can be skewed towards a few languages (i.e. Python). How can we extend what is learnt for one language to every language?

- Have one model specialized for each language
- Identify instructions that one model can handle very well while others struggle. use that model to create test cases and train other models to get better on that instruction. Finally, identify knowledge gaps across languages and fix them.