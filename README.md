# MNIST‑Playground

An end‑to‑end, **typed** PyTorch playground that demonstrates classic and modern machine‑learning techniques on the humble MNIST digits dataset while following solid engineering practice.

![CI](https://github.com/yourname/mnist-playground/actions/workflows/python-app.yml/badge.svg)
![Docs](https://img.shields.io/badge/docs-gh--pages-brightgreen)

---

## ✨  What this repo shows

| Category | Technique | Module / Script |
|----------|-----------|-----------------|
| **Supervised** | Baseline CNN, MLP, Vision‑Transformer | `train/classifier.py --arch cnn|mlp|vit` |
| | Linear Probes on penultimate features | `models/probe.py`, `examples/linear_probe.ipynb` |
| **Generative** | DC‑GAN | `train/gan.py` |
| | Deep‑Dream & Neuron Maximisation | `interpret/deep_dream.py`, `interpret/neuron_max.py` |
| | Style‑transfer into MNIST space | `interpret/style_transfer.py` |
| **Robustness** | FGSM adversarial attacks | `interpret/adversarial.py` |
| **Interpretability** | Saliency & Grad‑CAM | `interpret/saliency.py` |
| | Activation Atlases | `interpret/atlas.py` |
| **Preference‑learning** | Simple “RLHF” reward‑model loop | `rlhf/learn_preferences.py` |

> **Try it live:** every feature above ships with a Jupyter notebook in `examples/` that you can run with `poetry run jupyter lab`.

---

## 📦  Installation

```bash
# clone and enter
$ git clone https://github.com/yourname/mnist-playground.git && cd mnist-playground

# set up environment (Python ≥3.9)
$ curl -sSL https://install.python-poetry.org | python3 -  # install Poetry
$ poetry install --all-extras  # installs dev + docs extras too

# activate venv
$ poetry shell
```

### Optional extras

```bash
poetry install -E web      # to build ONNX + React demo
poetry install -E wandb    # experiment tracking
```

---

## 🚀  Quick‑start

Train a **CNN** for 5 epochs on GPU 0:

```bash
poetry run mnist-train --arch cnn --epochs 5 --device cuda:0
```

Switch to a **Vision Transformer** with 8 heads:

```bash
poetry run mnist-train --arch vit --vit-heads 8
```

Generate digits with the **GAN**:

```bash
poetry run mnist-gan --epochs 30 --save-gif out/gan.gif
```

Run **FGSM** adversarial attack and view fooling rate:

```bash
poetry run python -m mnist_playground.interpret.adversarial --eps 0.3
```

Full CLI reference is available via `--help` flags and in the [docs site](https://yourname.github.io/mnist-playground).

---

## 🗂️  Project layout

```
mnist_playground/
 ├── data.py               # loaders & helpers
 ├── models/               # CNN, MLP, ViT, GAN, Probe …
 ├── train/                # high‑level training CLIs
 ├── interpret/            # dreaming, saliency, atlases, etc.
 ├── rlhf/                 # preference‑learning loop
 └── __init__.py           # library facade
```

---

## 🛠️  Engineering best practices

* **Static typing** – mypy passes with `strict = True`; public APIs use [PEP‑561]‑compatible stub exports.
* **Pre‑commit** – `ruff`, `black`, `isort`, `docformatter`, and `mypy` run on every commit.
* **CI** – GitHub Actions lint, type‑check, test, and build docs on *push* & *PR*.
* **Tests** – `pytest` + `pytest‑cov` hit ≥ 80 % coverage; fixtures keep runtime < 30 s.
* **Docs** – `mkdocs‑material` renders notebooks and API docs to GitHub Pages.
* **Reproducibility** – seeds, deterministic cuDNN, and `torch.compile` flags are centralised in `utils/torch_helpers.py`.

---

## 🧪  Development workflow

```bash
poetry run pytest          # run unit tests
poetry run pytest -q       # quiet mode
poetry run mypy src/       # static type checking
```

Auto‑format before committing:

```bash
git add -u && git commit -m "feat: new interpretability demo"
```

---

## 📖  Documentation

```bash
poetry run mkdocs serve   # live preview on http://localhost:8000
poetry run mkdocs gh-deploy
```

---

## 🤝  Contributing

Pull requests are welcome!  Please run `pre-commit` and ensure CI passes.

---

## 📝  License

[MIT](LICENSE)

---

> © 2025 Your Name.  Released under the MIT License.

