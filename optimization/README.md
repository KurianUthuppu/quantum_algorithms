# Qiskit Optimization Algorithms

## Overview

This folder serves as a repository for various quantum optimization algorithms implemented using **Qiskit**. The primary focus is to demonstrate how real-world combinatorial problems (such as Max-Cut, TSP, Vehicle routing etc:-) can be mapped onto quantum circuits using both manual mathematical formulations and high-level abstract modules as applicable.

## Why Qiskit Optimization?

The [Qiskit Optimization module](https://qiskit-community.github.io/qiskit-optimization/index.html) provides a massive leap in productivity over building circuits from scratch.

### Key Advantages:

1. **High-Level Abstraction:** Move from "Pauli Z strings" to domain-specific objects like `networkx` graphs or `QuadraticPrograms`.
2. **Automated Encoding:** The library automatically handles the complex task of converting inequality constraints and integer variables into penalty terms in a Hamiltonian.
3. **Application Specific:** Includes built-in classes for Max-Cut, Traveling Salesman, Vehicle Routing, and more.

## Installation

To use these algorithms, ensure you have the `qiskit-optimization` extension installed along with standard quantum simulation tools:

```bash
pip install qiskit-optimization
```
