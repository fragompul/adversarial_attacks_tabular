# 🛡️ Adversarial Attacks on Tabular Regression Models

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Scikit--Learn](https://img.shields.io/badge/Scikit--Learn-Dataset-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **The structured-data analogue of [adversarial_attacks_vision](https://github.com/fragompul/adversarial_attacks_vision): how small, deliberate changes to a handful of numeric features can swing a regression model's prediction.**

## 📖 Project Overview

Every other repo in this family attacks a model that looks at raw signal, pixels, waveform samples, tokens. This one attacks a model that looks at a handful of named, human-meaningful numbers: income, room count, occupancy, location. That difference changes the threat model completely. Nobody "misperceives" a spreadsheet row the way a human misses an adversarial patch on a stop sign; the realistic attacker here is not trying to fool a human's eyes, they are trying to game an automated decision, an automated valuation model over-appraising a property, a credit-scoring model under-estimating risk, an insurance pricing model quoting the wrong premium, by nudging a few reported inputs just enough to move the number, while staying inside values that still look individually plausible.

This repo works through that threat model concretely on a real task: predicting median house value from the classic California Housing dataset (8 numeric features: median income, house age, average rooms, average bedrooms, population, average occupancy, latitude, longitude). A small neural network is trained to do the appraisal; the attacks then ask how much a handful of *reportable* features (the ones an individual filling out a form could plausibly misstate; not latitude and longitude, which are not something you get to lie about) need to move before the predicted value shifts substantially, and by how much.

**Origin & Scope:**
This is the fourth repository in the family that started with my Bachelor's Thesis on adversarial vision, after `adversarial_attacks_nlp` and `adversarial_attacks_audio`, extending the same rigor (hand-derived math, from-scratch implementations, honest quantitative evaluation) to structured/tabular data and to regression rather than classification, both firsts for this family.

---

## ✨ Key Features & Research Areas

1. **Gradient-Guided Feature Manipulation:** An FGSM-style attack adapted to regression, perturbing only the features an individual could plausibly misreport, to inflate a model's predicted house value, the tabular analogue of `attacks/whitebox/01_FGSM.ipynb` in the vision repo.
2. **A Genuinely Different Success Metric:** Regression has no "wrong class" to flip to, so success here is measured as predicted-value inflation (in dollars and in percent) rather than a binary attack success rate, alongside a threshold-based ASR-like number for comparability with the rest of the family.
3. **Domain-Specific Perturbation Constraints:** Unlike a pixel grid, tabular features have wildly different scales and units, and not every feature is something an attacker can plausibly change; this repo standardizes features before perturbing and explicitly restricts the attack to a "reportable" feature subset, a constraint with no equivalent in the vision/audio repos and only a loose one (fluency) in the NLP repo.

---

## 📂 Repository Guide

Notebooks are numbered in the order they are meant to be read, and every folder has its own README.

1. **[`models/`](models/)**: trains the base house-price regression network from scratch on California Housing.
2. **[`attacks/`](attacks/)**: gradient-guided feature manipulation to inflate a predicted price.

More notebooks (defenses, a query-only black-box attack, robustness evaluation, latent-space analysis of the feature manifold) are being added to reach the same structural depth as the vision/NLP/audio repos; see each folder's own README for what exists today.

---

## 🚀 Getting Started

```bash
git clone https://github.com/fragompul/adversarial_attacks_tabular.git
cd adversarial_attacks_tabular
python -m venv .venv
.venv\Scripts\activate   # or: source .venv/bin/activate on Linux/macOS
pip install -r requirements-dev.txt
jupyter lab
```

The California Housing dataset is fetched directly through `sklearn.datasets.fetch_california_housing` (cached locally by scikit-learn on first use), so there is no `data/` folder to track in git.

---

## 🛠️ Technology Stack

* **Deep Learning Framework:** PyTorch
* **Dataset & Preprocessing:** Scikit-Learn (California Housing, `StandardScaler`)
* **Data Science & Visualization:** NumPy, Pandas, Matplotlib, Seaborn

---

## 🌐 Part of a Research Family

Adversarial vulnerability is not specific to any one input type; the same core idea, small deliberate input changes causing disproportionate output changes, shows up wherever a model makes a decision. This repo has sibling projects applying the same rigor elsewhere:

* **[adversarial_attacks_vision](https://github.com/fragompul/adversarial_attacks_vision)** — the flagship of the family: FGSM/PGD/C&W and more on image classifiers, plus defenses, explainability, and a live dashboard.
* **[adversarial_attacks_nlp](https://github.com/fragompul/adversarial_attacks_nlp)** — fooling a sentiment classifier with gradient-guided word substitution and black-box synonym swaps.
* **[adversarial_attacks_audio](https://github.com/fragompul/adversarial_attacks_audio)** — fooling a keyword-spotting model with imperceptible waveform perturbations.

---

## Author

**Francisco Javier Gómez Pulido**

*AI Lead @ AAPEX | Double Major in Mathematics & Computer Science* | Master's in Artificial Intelligence

📫 **Let's connect:**
* **LinkedIn:** [linkedin.com/in/frangomezpulido](https://www.linkedin.com/in/frangomezpulido)
* **GitHub:** [github.com/fragompul](https://github.com/fragompul)
* **Email:** [frangomezpulido2002@gmail.com](mailto:frangomezpulido2002@gmail.com)

---
*Sibling project to [adversarial_attacks_vision](https://github.com/fragompul/adversarial_attacks_vision), [adversarial_attacks_nlp](https://github.com/fragompul/adversarial_attacks_nlp), and [adversarial_attacks_audio](https://github.com/fragompul/adversarial_attacks_audio). If you find this interesting, feel free to ⭐ star it!*
