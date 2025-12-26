# 🔐 LWE Cryptanalysis: Hybrid LLL & MILP Solver

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

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

See **Report.pdf** for the better understanding of the concepts involved.

---
