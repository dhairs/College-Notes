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

### Self-Supervised Learning with BERT