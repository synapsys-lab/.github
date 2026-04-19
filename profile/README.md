<div align="center">

<img src="https://raw.githubusercontent.com/synapsys-lab/synapsys/main/website/static/img/logo.svg" width="96" height="96" alt="Synapsys Lab" />

# Synapsys Lab

**Open-source Python tooling for modelling, analysis and real-time simulation of control systems**

[![PyPI](https://img.shields.io/pypi/v/synapsys.svg?color=2563eb&label=synapsys)](https://pypi.org/project/synapsys/)
[![CI](https://github.com/synapsys-lab/synapsys/actions/workflows/ci.yml/badge.svg)](https://github.com/synapsys-lab/synapsys/actions)
[![Coverage](https://img.shields.io/badge/coverage-100%25-brightgreen.svg)](https://github.com/synapsys-lab/synapsys)
[![Docs](https://img.shields.io/badge/docs-online-2563eb)](https://synapsys-lab.github.io/synapsys/)
[![Python](https://img.shields.io/pypi/pyversions/synapsys.svg)](https://pypi.org/project/synapsys/)
[![License: MIT](https://img.shields.io/badge/License-MIT-14b8a6.svg)](https://github.com/synapsys-lab/synapsys/blob/main/LICENSE)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit)](https://github.com/pre-commit/pre-commit)

</div>

---

## Quadcopter MIMO Neural-LQR

<div align="center">
<table>
<tr>
<td align="center">
<img src="https://raw.githubusercontent.com/synapsys-lab/synapsys/main/website/static/img/examples/06_quadcopter_3d.gif" alt="PyVista 3D — drone tracking a figure-8 trajectory" width="360" />
<br><sub>PyVista 3D — drone mesh, trajectory trail and live HUD at 50 Hz</sub>
</td>
<td align="center">
<img src="https://raw.githubusercontent.com/synapsys-lab/synapsys/main/website/static/img/examples/06_quadcopter_telemetry.gif" alt="matplotlib telemetry panel" width="420" />
<br><sub>matplotlib telemetry — position, Euler angles and control deviations</sub>
</td>
</tr>
</table>
</div>

> 12-state linearised quadcopter with residual Neural-LQR (`du = −K·e + MLP(e)`). Full walkthrough: [examples/advanced/quadcopter-mimo →](https://synapsys-lab.github.io/synapsys/docs/examples/advanced/quadcopter-mimo)

---

## Neural-LQR · 2-DOF mass-spring-damper

<div align="center">
<img src="https://raw.githubusercontent.com/synapsys-lab/synapsys/main/website/static/img/examples/03_sil_ai_controller.gif" alt="Neural-LQR on a 2-DOF mass-spring-damper" width="700" />
</div>

> MLP initialized with LQR optimal gains controlling a 2-DOF mechanical system in a real-time SIL loop. Full walkthrough: [examples/advanced/sil-ai-controller →](https://synapsys-lab.github.io/synapsys/docs/examples/advanced/sil-ai-controller)

---

## Projects

| Repository | Description | Status |
|---|---|---|
| [**synapsys**](https://github.com/synapsys-lab/synapsys) | Core library — LTI models, MIMO, PID, LQR, multi-agent simulation, SIL/HIL | [![CI](https://github.com/synapsys-lab/synapsys/actions/workflows/ci.yml/badge.svg)](https://github.com/synapsys-lab/synapsys/actions) |

---

## What is Synapsys?

Synapsys is a Python framework for the full control-design workflow — from continuous-time modelling to real-time closed-loop simulation and hardware deployment:

```python
from synapsys import tf, ss, feedback, step, c2d, PID, lqr
import numpy as np

# ── LTI model ──────────────────────────────────────────────────
G    = tf([1], [1, 2, 1])        # G(s) = 1 / (s² + 2s + 1)
T    = feedback(G)                # closed-loop
t, y = step(T)                    # step response

# ── MIMO transfer-function matrix ──────────────────────────────
G_mimo = tf([[[1], [0]], [[0], [1]]],
            [[[1, 1], [1]], [[1], [1, 2]]])
T_mimo = feedback(G_mimo)         # returns StateSpace

# ── Discretise and control ──────────────────────────────────────
Gd = c2d(G, dt=0.01)             # ZOH at 100 Hz
pid = PID(Kp=3.0, Ki=0.5, dt=0.01, u_min=-10.0, u_max=10.0)

# ── LQR optimal gains ──────────────────────────────────────────
A = np.array([[0., 1.], [-2., -3.]])
B = np.array([[0.], [1.]])
K, _ = lqr(A, B, Q=np.eye(2), R=np.eye(1))
```

### Key capabilities

| | Feature |
|---|---|
| ⚡ | **MATLAB-compatible API** — `tf()`, `ss()`, `step()`, `bode()`, `feedback()`, `c2d()` |
| 📐 | **LTI core** — `TransferFunction`, `StateSpace`, `TransferFunctionMatrix`, poles/zeros, stability |
| 🧮 | **MIMO support** — `TransferFunctionMatrix`, MIMO `feedback()`, transmission zeros (Rosenbrock pencil) |
| 🎛️ | **Control algorithms** — Discrete PID with anti-windup · LQR (ARE solver) |
| 🤖 | **Multi-agent simulation** — `PlantAgent` + `ControllerAgent` with wall-clock sync |
| 🔗 | **Pluggable transport** — Zero-copy shared memory · ZeroMQ (distributed) |
| 🔌 | **Hardware abstraction** — MIL → SIL → HIL with a single-line transport swap |
| 🧠 | **AI integration** — Any PyTorch, Keras or JAX model as a controller |

---

## Install

```bash
pip install synapsys          # pip
uv add synapsys               # uv
poetry add synapsys           # Poetry
conda install -c conda-forge synapsys   # conda / mamba
```

**Python ≥ 3.10** · NumPy · SciPy · pyzmq

---

## Links

| | |
|---|---|
| 📖 Documentation | https://synapsys-lab.github.io/synapsys/ |
| 📦 PyPI | https://pypi.org/project/synapsys/ |
| 💡 Examples | https://synapsys-lab.github.io/synapsys/docs/examples |
| 🗺️ Roadmap | https://synapsys-lab.github.io/synapsys/docs/roadmap |
| 🐛 Issues | https://github.com/synapsys-lab/synapsys/issues |
| 📋 Changelog | https://github.com/synapsys-lab/synapsys/blob/main/CHANGELOG.md |

---

## Stack

![Python](https://img.shields.io/badge/Python-3.10%2B-3b82f6?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.24%2B-013243?logo=numpy&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-1.10%2B-8caae6?logo=scipy&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-compatible-ee4c2c?logo=pytorch&logoColor=white)
![ZeroMQ](https://img.shields.io/badge/ZeroMQ-25%2B-df0000?logo=zeromq&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-14b8a6)

---

## Contributors

<div align="center">
  <a href="https://github.com/synapsys-lab/synapsys/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=synapsys-lab/synapsys" alt="Contributors" />
  </a>
  <br><sub>Contributions are welcome — see the <a href="https://github.com/synapsys-lab/synapsys/blob/main/README.md#contributing">contributing guide</a>.</sub>
</div>
