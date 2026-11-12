# Evaluating PINNsFormer for Solving Partial Differential Equations

This repository contains the implementation and evaluation of PINNsFormer on five benchmark partial differential equations (PDEs), comparing its performance with standard Physics-Informed Neural Networks (PINNs).

The project was conducted as part of a bachelor's thesis in Mathematics and Applications at Amirkabir University of Technology.

## Project Overview

PINNsFormer is a Transformer-based framework for solving PDEs using physics-informed neural networks. Unlike standard PINNs, which process individual space-time points, PINNsFormer uses short pseudo-time sequences and attention mechanisms.

This project investigates the performance of this approach on five PDE benchmark problems, with particular attention to accuracy, computational cost, and its application to equations involving higher-order derivatives.

## Repository Structure

The repository contains five independent Jupyter notebooks:

| Notebook | PDE Problem |
|---|---|
| `PINNsFormer_Burgers.ipynb` | Burgers Equation |
| `PINNsFormer_AllenCahn.ipynb` | Allen–Cahn Equation |
| `PINNsFormer_Schrodinger.ipynb` | Nonlinear Schrödinger Equation |
| `PINNsFormer_KS.ipynb` | Kuramoto–Sivashinsky Equation |
| `PINNsFormer_KdV.ipynb` | Korteweg–de Vries Equation |

Each notebook implements the corresponding problem using both standard PINNs and PINNsFormer and evaluates their predictions against reference solutions.

## Methodology

### Standard PINN

The standard PINN uses a fully connected neural network that takes spatial and temporal coordinates as input and predicts the solution of the corresponding PDE.

### PINNsFormer

PINNsFormer uses a sequence-based input representation and a Transformer architecture. Its main components include:

- Pseudo-sequence generation from space-time coordinates.
- Spatio-temporal embedding.
- Transformer encoder-decoder architecture.
- Learnable Wave Activation (WaveAct).

### Training Configuration

The main configuration used for PINNsFormer includes:

| Parameter | Value |
|---|---:|
| Sequence length (`k`) | 5 |
| Time step (`dt_step`) | 0.0001 |
| Embedding dimension (`d_model`) | 32 |
| Number of attention heads | 2 |
| Number of Transformer layers (`N`) | 1 |
| Hidden dimension (`d_hidden`) | 512 |
| Optimizer | L-BFGS |
| Maximum iterations | 500 |

The specific problem settings and network configurations are provided in the corresponding notebooks.

## Requirements

The project uses Python and the following main libraries:

- NumPy
- PyTorch
- Matplotlib
- SciPy
- tqdm
- Jupyter Notebook

The required packages are listed in `requirements.txt`.

## How to Run

1. Clone or download this repository.
2. Install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Open the notebook corresponding to the PDE problem you want to reproduce:

   ```bash
   jupyter notebook
   ```

4. Run the notebook cells sequentially.

Each notebook contains the implementation, training procedure, evaluation, and visualization for its corresponding PDE problem.

## Reference Data

The Burgers, Allen–Cahn, nonlinear Schrödinger, and KdV notebooks use reference datasets obtained from the original PINNs repository by Maziar Raissi and collaborators.

These datasets are downloaded automatically by the corresponding notebooks.

The Kuramoto–Sivashinsky notebook uses an analytical solution defined directly in the notebook and does not require an external reference dataset.

An active internet connection is therefore required to run the four notebooks that download external datasets.

## Evaluation Metrics

The models are evaluated using the relative Mean Absolute Error (rMAE) and relative Root Mean Squared Error (rRMSE).

The metrics are calculated as follows:

**Relative Mean Absolute Error:**

$rMAE = \frac{\sum_i |u_i^{pred}-u_i^{true}|}{\sum_i |u_i^{true}|}$

**Relative Root Mean Squared Error:**

$$
rMAE = \frac{\sum_i |u_i^{pred}-u_i^{true}|}{\sum_i |u_i^{true}|}
$$

For the nonlinear Schrödinger equation, the evaluation is performed using the magnitude of the complex-valued solution.

## Results

The following table summarizes the relative MAE obtained by both methods across the five benchmark problems.

| PDE Problem | Standard PINN rMAE | PINNsFormer rMAE | Reduction |
|---|---:|---:|---:|
| Burgers | 0.0262 | 0.0120 | 54% |
| Allen–Cahn | 0.9916 | 0.3790 | 62% |
| Nonlinear Schrödinger | 0.0601 | 0.0032 | 95% |
| Kuramoto–Sivashinsky | 0.3012 | 0.0001 | >99% |
| Korteweg–de Vries | 0.0820 | 0.0184 | 78% |

PINNsFormer achieved lower rMAE than the standard PINN in all five benchmark problems.

## Computational Cost

The measured training times are summarized below.

| PDE Problem | Standard PINN | PINNsFormer |
|---|---:|---:|
| Burgers | 4m 01s | 28m 25s |
| Allen–Cahn | 1m 28s | 32m 53s |
| Nonlinear Schrödinger | 7m 12s | 49m 59s |
| Kuramoto–Sivashinsky | 2m 53s | 53m 57s |
| Korteweg–de Vries | 10m 38s | 1h 49m |

These measurements reflect the computational cost observed in the original experiments and may vary depending on hardware and execution environment.

## Reproducibility Notes

- Each PDE problem is implemented in a separate notebook.
- Random seeds are set for NumPy, Python, and PyTorch.
- The notebooks include the data-loading, model-training, and evaluation procedures.
- External reference datasets are downloaded automatically where required.
- Training time and numerical results may vary slightly across hardware and software environments.

## Reference

Zhao, Z., Ding, X., & Prakash, B. (2024). *PINNsFormer: A Transformer-Based Framework for Physics-Informed Neural Networks*. International Conference on Learning Representations (ICLR 2024).

