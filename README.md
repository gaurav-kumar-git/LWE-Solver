# 🔐 LWE Cryptanalysis: Hybrid LLL & MILP Solver

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/Status-Educational-yellow.svg)

---

## 📌 Project Overview

This project implements a **hybrid cryptanalytic solver** for small-scale instances of the
**Learning With Errors (LWE)** problem, a foundational hardness assumption in
**Post-Quantum Cryptography (PQC)**.

The solver combines:

- **Lattice basis reduction (LLL)** for heuristic approximation
- **Mixed-Integer Linear Programming (MILP)** for exact recovery

The goal is to demonstrate how **approximate lattice attacks can be refined into exact
solutions** using deterministic integer optimization.

This repository is intended for **educational, experimental, and research purposes**.

---

## 🧮 The Learning With Errors (LWE) Problem

Given:
- A public matrix \( A \in \mathbb{Z}_q^{m \times n} \)
- A public vector \( b \in \mathbb{Z}_q^{m} \)
- A modulus \( q \)

The task is to recover:
- A secret vector \( x \in \mathbb{Z}^n \)
- A small error vector \( e \in \mathbb{Z}^m \)

such that:

\[
A \cdot x + e \equiv b \pmod q
\]

For sufficiently large dimensions, recovering \( x \) is believed to be computationally
hard, forming the security basis of modern lattice-based cryptosystems such as
**Kyber** and **Dilithium**.

---

## 🚀 Hybrid Methodology (Warm-Start Strategy)

The solver follows a **two-stage attack pipeline**.

---

### 🔹 Phase I: Lattice Reduction (Approximate Solution)

The LWE instance is embedded into a lattice whose short vectors encode candidates
for the tuple \( (x, e, -1) \).

- **Algorithm:** Lenstra–Lenstra–Lovász (LLL)
- **Reduction parameter:** \( \delta \approx 0.75 \)
- **Library:** `fpylll`

**Purpose:**
- Improve basis orthogonality
- Recover a short vector close to the true secret
- Provide tight bounds for the optimization phase

This stage provides a **heuristic approximation** used as a warm start.

---

### 🔹 Phase II: MILP Refinement (Exact Solution)

The approximate solution from Phase I is refined using **Mixed-Integer Linear Programming**.

Each LWE equation is rewritten as:
\[
A_i \cdot x + e_i = b_i + q \cdot k_i
\]
where \( k_i \in \mathbb{Z} \) are integer slack variables.

#### Optimization Objective
\[
\min \sum_i |e_i|
\]

#### Solver Characteristics
- Exact integer arithmetic
- Branch-and-Bound optimization
- Guaranteed global optimum within bounds
- **Library:** `PuLP`

---

## 🧠 Why the Hybrid Approach Works

| Component | Role |
|--------|------|
| LLL | Narrows the search space efficiently |
| MILP | Guarantees correctness and optimality |
| Integer slack variables | Preserve modular arithmetic |
| L1-error minimization | Matches LWE noise assumptions |

This mirrors real cryptanalysis pipelines where **heuristics guide exact solvers**.

---

## 🛠️ Installation & Prerequisites

### System Dependencies (Linux / Colab)

```bash
sudo apt-get install -y libgmp-dev libmpfr-dev libmpc-dev

