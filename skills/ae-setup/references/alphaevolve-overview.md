# AlphaEvolve Overview

Google DeepMind evolutionary coding agent (May 2025). An LLM ensemble (Gemini Flash + Pro) iteratively mutates code, scores it against your evaluator, and evolves better solutions over hundreds/thousands of generations. Available via Google Cloud Early Access API.

## The Three Inputs

### 1. Prompt
Natural language describing the problem, task, and hints. Pattern from real examples:

> "Act as an expert in mathematics. Your task is to solve the following problem.
> **Problem Statement:** [math description].
> **Your Task:** You must write a Python function that [does X].
> **Evaluation:** Your proposed construction will be evaluated by [criteria]. A higher score is better.
> **Hints:** [encouragement, strategic guidance]"

### 2. Initial Program
A working but naive Python function — the seed the LLM evolves. Requirements:
- Clear function signature (e.g. `def search_for_best_construction(p, d)`)
- Actually runs and returns valid output (even if trivial/hardcoded)
- This is the *only* thing the LLM modifies

### 3. Evaluation (Scoring + Validation) Function
Written by us, never seen or touched by the LLM. It must:
- Call the evolved function
- Validate correctness (is the answer actually valid?)
- Return `{"score": float}` — higher is better
- Be **exploit-proof** (use exact/interval arithmetic, not floating-point tolerance checks — AlphaEvolve is extremely good at finding loopholes)

## Sandbox Constraints
- **Vanilla Python only** — no C extensions, no pip installs
- Libraries available (from 67 official examples): `numpy`, `scipy`, `itertools`, `collections`, `math`, `time`, `random`, `copy`, `numba`, `typing`, `re`, `logging`, `sympy`
- Time budget per evaluation is user-defined (common: 1000 seconds for search problems)
- Evaluator typically runs across multiple test cases (e.g., a range of parameter values)

## Key Practical Lessons (Tao/Gomez-Serrano, 67 math problems)
- Make the verifier **conservative** — AlphaEvolve will exploit any floating-point slop
- Let AlphaEvolve choose its own hyperparameters rather than pre-specifying them
- Explicit strategic hints in the prompt work better than uploading full papers
- The initial program can be deliberately bad/naive — evolution handles the rest

## Reference Material
- 67 real problems with all 3 inputs: https://github.com/google-deepmind/alphaevolve_repository_of_problems
- AlphaEvolve blog: https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/
- Paper: https://arxiv.org/abs/2506.13131
- Tao's writeup: https://terrytao.wordpress.com/2025/11/05/mathematical-exploration-and-discovery-at-scale/
