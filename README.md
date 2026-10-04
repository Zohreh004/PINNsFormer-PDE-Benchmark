Evaluating PINNsFormer for Solving Partial Differential Equations

A comparative study and implementation of Physics-Informed Neural Networks (PINNs) and PINNsFormer, a Transformer-based architecture for solving partial differential equations (PDEs).

This project was developed as a bachelor's thesis at Amirkabir University of Technology (Tehran Polytechnic).

Overview

Physics-Informed Neural Networks (PINNs) provide a mesh-free approach for approximating solutions to partial differential equations by incorporating the governing equations and their boundary/initial conditions directly into the training objective.

This project implements PINNsFormer, which introduces a pseudo-temporal sequence and a self-attention mechanism into the PINN framework. The goal is to investigate whether explicitly modeling dependencies between nearby time points can improve the accuracy of PINNs on challenging time-dependent PDEs.

The implementation is evaluated against a standard PINN baseline on five benchmark problems:

Burgers' equation
Allen–Cahn equation
Nonlinear Schrödinger equation
Kuramoto–Sivashinsky equation
Korteweg–de Vries (KdV) equation

The PINNsFormer architecture uses a pseudo-sequence generator, spatio-temporal embedding, multi-head self-attention, an encoder–decoder structure, and a learnable Wavelet activation function.

Project Objectives

The main objectives of this project are:

Implement the PINNsFormer architecture from the original paper.
Implement a standard PINN as a baseline model.
Evaluate both models on five different PDE benchmarks.
Compare their numerical accuracy using relative MAE (rMAE) and relative RMSE (rRMSE).
Analyze the computational cost and training time of the two approaches.
Investigate the effect of the attention-based architecture on PDEs with different characteristics.
Methodology
Standard PINN

The baseline model is a fully connected neural network with:

4 hidden layers
512 neurons per hidden layer
Tanh activation
Point-wise (x, t) input
PINNsFormer

The implemented PINNsFormer model consists of:

Pseudo-sequence generator
Converts each (x, t) input into a sequence of nearby time points.
Spatio-temporal mixer
Projects the two-dimensional inputs into a 32-dimensional representation.
Transformer-based encoder–decoder
Uses self-attention and cross-attention to model dependencies between the elements of the temporal sequence.
Wavelet activation
Uses a learnable combination of sine and cosine functions.
Output layer
Produces the approximate PDE solution for each element of the sequence.

The main configuration used in the experiments is k = 5, d_model = 32, 2 attention heads, and one encoder layer.

PDE Benchmarks
Problem	Main characteristic
Burgers	Nonlinear convection and rapid variation
Allen–Cahn	Stiff reaction–diffusion dynamics
Nonlinear Schrödinger	Complex-valued solution and nonlinear dynamics
Kuramoto–Sivashinsky	Fourth-order PDE with challenging dynamics
KdV	Third-order nonlinear PDE

Reference solutions were obtained from the datasets associated with the original PINN work for four equations, while a closed-form analytical solution was used for the Kuramoto–Sivashinsky equation.

Results

PINNsFormer achieved a lower rMAE than the standard PINN on all five benchmark problems.

Equation	PINN rMAE	PINNsFormer rMAE	Reduction
Burgers	0.0262	0.0120	54%
Allen–Cahn	0.9916	0.3790	62%
Nonlinear Schrödinger	0.0601	0.0032	95%
Kuramoto–Sivashinsky	0.3012	0.0001	>99%
KdV	0.0820	0.0184	78%

These results show that the attention-based architecture improved the numerical accuracy across all five experiments, although the magnitude of the improvement varied substantially between equations.

Computational Cost

The improved accuracy comes with a significant increase in training time.

Equation	PINN	PINNsFormer
Burgers	4m 1s	28m 25s
Allen–Cahn	1m 28s	32m 53s
Schrödinger	7m 12s	49m 59s
Kuramoto–Sivashinsky	2m 53s	53m 57s
KdV	10m 38s	1h 49m

On average, PINNsFormer required approximately 13.1× more training time than the standard PINN.

Key Findings
PINNsFormer achieved lower relative error on all five PDEs.
The improvement ranged from 54% to more than 99% in rMAE.
The largest improvement was obtained for the Kuramoto–Sivashinsky equation, where rMAE decreased from 0.3012 to 0.0001.
The nonlinear Schrödinger equation also showed a substantial improvement, with rMAE decreasing by approximately 95%.
For Allen–Cahn, PINNsFormer significantly improved the approximation, although the final error remained relatively high.
The improved accuracy came at a substantial computational cost, with approximately 13× longer training time on average.
