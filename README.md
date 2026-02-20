# README

# Decoding the Energetic Grammar of Genetic Systems, a Hybrid Neural, Symbolic Framework for Quantum Informed Bioenergetics
## Generative-Bioenergetics
Neural symbolic modeling of how cellular energy flow governs gene expression, repair, and replication, bridging AI, quantum biology, and systems bioenergetics.
**Author** Mark I R Petalcorin  
**Contact** mark.petalcorin@a-aidea.com  

### Overview

This repository contains code and materials for a hybrid neural and symbolic framework that discovers compact equations linking cellular energetics to genome level processes. The system learns from simulated time series of ATP, NADH, and ROS, trains a neural ordinary differential equation, then extracts interpretable laws with symbolic regression. The approach defines a mechanistic grammar for energy informed gene expression, DNA repair, and replication.

### Key features

1. Generative bioenergetics simulator that produces realistic ATP and NADH oscillations and ROS dynamics
2. Neural ordinary differential equation training that captures continuous time behavior
3. Symbolic regression that recovers concise equations with high fidelity
4. Reproducible pipeline with seed control and saved artifacts
5. Publication quality tables and figures for manuscripts and slides

### Installation

Requirements, Python 3 point 10 or later

Outputs appear under artifacts. Look for hall of fame csv files, trained weight files, and figure images.

### What you get

* Top ranked symbolic equations for
  * gene expression rate
  * DNA repair efficiency
  * replication scaling with redox
* A ready to cite equations table in docx and pdf
* A heat map that visualizes the symbolic control law across ATP and NADH with fixed ROS
* Logs for seeds, configuration, and metrics

### Reproducibility

* Set seeds in config, all steps read the same config
* Each run writes a run id, a config copy, and checksums into artifacts
* Deterministic integrators are used where possible, any stochastic terms are logged with seeds

### Citing

**Petalcorin M.I.R. (2025)**. Decoding the Energetic Logic of Genetic Systems: A Hybrid Neural-Symbolic Framework for Quantum-Informed Bioenergetics. bioRxiv. https://www.biorxiv.org/content/10.1101/2025.10.15.682721v1.full.pdf
### Contact and support

Issues and questions, email the corresponding author

# DATA_SHEET

## Dataset name

Generative Bioenergetics Synthetic Time Series

## Summary

The dataset contains simulated single cell trajectories for ATP, NADH, ROS, and three genomic process proxies, gene expression, DNA repair, and replication. Trajectories include rhythmic energy behavior and stress responses that mirror live cell observations under metabolic adaptation.

## Motivation

The goal is to study how energy and redox variables control genome linked processes, and to recover interpretable laws through symbolic regression. Synthetic data provide full control of ground truth and allow safe exploration without experimental burden.

## Composition

* Variables per time step
  * ATP, normalized zero to one
  * NADH, normalized zero to one
  * ROS, normalized zero to one
  * G prime, gene expression rate, normalized
  * R prime, DNA repair rate, normalized
  * P prime, replication rate, normalized
* Typical length per trajectory, ten thousand time points
* Sampling cadence, constant spacing in simulation time units
* Number of trajectories per run, configurable, default one hundred
* Splits
  * train seventy percent
  * validation fifteen percent
  * test fifteen percent

## Data generation

* Base model, coupled stochastic differential equations for oxidative phosphorylation, redox cycling, ROS production and clearance
* Noise model, additive gaussian terms for enzyme fluctuations and heterogeneity
* Parameter tuning, set to reproduce plausible ATP and NADH oscillations with mild oxidative stress
* Units, arbitrary simulation units, all channels are scaled to zero to one for learning and symbolic search

## Collection and preprocessing

* No human or clinical data are used
* Scaling, min max per channel to zero to one
* Optional smoothing for visualization, never used for training or symbolic search
* Derivatives, numeric time derivatives are computed for G, R, and P to supervise symbolic search

## Data quality

* Sanity checks ensure positivity for ATP and NADH, non negative ROS, bounded rates
* Outlier rejection is disabled by default, since rare energetic events can be informative
* Seeds are logged to allow exact regeneration

## Uses

* Training neural ordinary differential equations
* Symbolic regression for compact laws
* Sensitivity studies on energy and redox parameters
* Benchmarking interpretable models

## Distribution

* Format, csv files per trajectory and per split
* Metadata, yaml sidecars with seeds and parameters
* Location, data folder in this repository or generated on the fly

## Maintenance

* Primary contact, Mark I R Petalcorin, mark.petalcorin@a-aidea.com
* Update plan, periodic improvements to simulators and metadata

## Ethical and legal

* Synthetic only, no personal or sensitive data
* No restrictions on research use under the chosen open license

# MODEL_CARD

## Model overview

A hybrid system that learns continuous time bioenergetic dynamics with a neural ordinary differential equation and then discovers human readable equations through symbolic regression. The model encodes how ATP, NADH, and ROS govern gene expression, DNA repair, and replication.

## Intended use

* Explain and quantify energy informed control of genome linked processes
* Generate hypotheses for experimental validation
* Provide compact control laws for larger multiscale simulators
* Create publication figures and tables

Out of scope

* Clinical diagnosis or treatment decisions
* Direct prediction on patient data without prior validation
* Safety critical automation

## Inputs and outputs

* Inputs
  * ATP, scalar per time step, normalized
  * NADH, scalar per time step, normalized
  * ROS, scalar per time step, normalized
* Outputs
  * dG dt, gene expression rate proxy
  * dR dt, DNA repair rate proxy
  * dP dt, replication rate proxy
* Symbolic forms, examples
  * G prime equals alpha one times ATP times exp of minus beta one times ATP plus gamma one times sin of delta one times ATP
  * R prime equals alpha two times ATP squared times exp of minus beta two times ATP
  * P prime equals alpha three times open NADH over ROS close raised to gamma three

## Training data

* Source, synthetic single cell time series generated by the included simulators
* Coverage, oscillatory and non oscillatory regimes, mild stress, recovery
* Normalization, zero to one per channel

## Training procedure

* Neural ODE
  * three hidden layers, thirty two units each, tanh activation
  * RK45 integration
  * mean squared error loss across all channels
  * Adam optimizer with standard settings
* Symbolic regression
  * search space includes arithmetic, exponential, logarithmic, trigonometric, and rational operators
  * ranked by R squared and a parsimony cost
  * hall of fame tables record top expressions with scores

## Evaluation

* Metrics, R squared, mean squared error, Pearson correlation
* Typical scores
  * gene expression R squared about zero point nine three
  * DNA repair R squared about zero point nine one
  * replication R squared about zero point eight nine
* Robustness
  * five seeds show stable structure with small parameter variance
  * sensitivity analysis identifies ATP use and redox decay constants as major drivers

## Limitations

* Synthetic data do not capture full cellular complexity
* Units are normalized, mapping to absolute biochemical units requires calibration
* Equations describe proxies for processes, not direct transcription factor dynamics
* Quantum informed claims are exploratory and require experimental confirmation

## Risks and mitigation

* Risk, misinterpretation of symbolic laws as universal
  * Mitigation, restrict use to hypothesis generation and simulation
* Risk, overfitting to simulator quirks
  * Mitigation, use multiple parameter regimes and seeds, publish seeds and configs
* Risk, misuse in clinical contexts
  * Mitigation, include clear out of scope statement and license terms

## Ethical considerations

* No personal data
* Open science orientation, full reproducibility and interpretability
* Encourage validation on experimental systems before real world decisions

## Deployment

* Package as a python module with entry points for simulate, train, and discover
* Artifacts include trained weights, equations tables, and figures

## Versioning

* Semantic versioning, major, minor, patch
* Changelog maintained in docs

## Maintenance and contact

* Maintainer, Mark I R Petalcorin, mark.petalcorin@a-aidea.com
