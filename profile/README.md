# Synapsys Lab

Open-source Python tooling for **modelling, analysis and real-time simulation
of linear control systems**.

---

## Projects

| Repository | Description | Status |
|---|---|---|
| [synapsys](https://github.com/synapsys-lab/synapsys) | Core library — LTI models, PID, LQR, multi-agent simulation | ![CI](https://github.com/synapsys-lab/synapsys/actions/workflows/ci.yml/badge.svg) |

---

## About

Synapsys provides a **MATLAB-compatible Python API** over SciPy, a
multi-agent simulation framework with pluggable transport (shared memory / ZMQ),
and a clear MIL → SIL → HIL progression path for control engineering workflows.

```python
from synapsys import tf, feedback, step, PID, lqr

G = tf([1], [1, 2, 1])          # G(s) = 1 / (s² + 2s + 1)
T = feedback(G)                  # closed-loop
t, y = step(T)                   # step response
```

**[Documentation](https://synapsys-lab.github.io/synapsys/) ·
[Quickstart](https://synapsys-lab.github.io/synapsys/docs/getting-started/quickstart) ·
[API Reference](https://synapsys-lab.github.io/synapsys/docs/api/core)**

---

## Stack

![Python](https://img.shields.io/badge/Python-3.10%2B-3b82f6?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.24%2B-013243?logo=numpy)
![SciPy](https://img.shields.io/badge/SciPy-1.10%2B-8caae6?logo=scipy)
![License](https://img.shields.io/badge/License-MIT-14b8a6)
