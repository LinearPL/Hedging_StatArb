## Hedging for Stat Arb Strategies**

This repository provides a hedging environment for statistical arbitrage. It utilizes a deep policy gradient reinforcement learning (RL) algorithm to analyze this relationship. The repository consists of two primary components:

- Component 1: Environment generation using three market simulators— a discrete Black-Scholes market, GARCH dynamics, and GJR-GARCH dynamics.
- Component 2: Implementation of an RL-based hedging agent for European options.

## Overview

1. Market Environment Simulation (Component 1)
    - Located in the src/features/ directory.
    - The file features_simulation.py generates the RL environment, simulating stock returns, volatility, and risk factors that define the state space. Additional theoretical details are available in our paper.

2. Deep Reinforcement Learning Model (Component 2)
    - Found in the src/models/ directory.
    - The deep_rl_agent.py script contains a Python class that trains and evaluates RL agents based on a standard feedforward neural network (FFNN).

Example implementations of the pipeline can be found in the notebooks folder. A standalone Python script for executing the full pipeline is available in the pipeline directory.

## How to Run the Project

1. **Prerequisities**
    - Developed using Python 3.9.6.
    - Ensure pip is installed and up to date.

2. **Environment setup**

- Clone the repository:

```nohighlight
git clone https://github.com/OctavioPM/DeepHedging_StatisticalArbitrage.git
cd DeepHedging_StatisticalArbitrage
```

- Create and activate a virtual environment:

```nohighlight
python -m venv venv
source venv/bin/activate
```

- Install required dependencies:

```nohighlight
pip install -r requirements.txt
```

- Alternatively, start with an empty virtual environment and install packages during execution on as-required basis.

3. **Modify parameters**: The default parameters can be modified in the configuration files located in the cfgs folder:

- `config_simulation.yml`: General parameters for the simulation.

- `config_agent.yml`: Hyperparameters of the RL optimization problem.


4. **Running the script**: We provide two options to run the deep hedging JIVR pipeline:

- Option 1. Run each component separately using the provided Jupyter notebook `deep_hedging_pipeline.ipynb` included in the `notebooks` folder. This notebook outlines performance metrics, including those from Table 1 in François et al. (2024), for the RL-CVaR agent under Black-Scholes dynamics.

- Option 2. Execute the full pipeline from the terminal. Navigate to the `pipeline` folder and run the appropriate script.

Thank you to François et al. (2024) for providing the deep hedging framework. 

```nohighlight
cd pipeline
python deep_hedging_pipeline.py
```

## Directory structure

```nohighlight
├── LICENSE
├── README.md                   <- The top-level README for this project.
├── cfgs                        <- Configuration files for environment simulation and RL model parameters.
│
├── data
│   ├── raw                     <- Historical estimated parameters of the S&P 500 index.
│   ├── interim                 <- Temporary data used during simulation.
│   ├── processed               <- Simulated markets dynamics.
│   └── results                 <- Deep hedging strategies (RL sgents output).
│
├── notebooks                   <- Jupyter notebook with pipeline example.
│
├── pipeline                    <- .py pipeline script.
│
├── models                      <- Folder to store trained RL agents.
│
├── src                         <- Source code for use in this project.
│   │
│   ├── data                    <- Scripts to download and generate data.
│   │   └── data_loader.py         <- Script to transform data into the right format for the models.
│   │
│   ├── features                   <- Scripts to generate market environment.
│   │   └── features_simulation.py <- Script to generate state space.
│   │
│   ├── models                     <- Scripts to train models and then use trained models to make
│   │   │                             hedging strategies.
│   │   ├── deep_rl_agent.py       <- Script create RL agents as class objects.
│   │   └── deep_rl_training.py    <- Script to fit and make inference.
│   │
│   ├── visualization              <- Scripts to compute performance metrics of the models.
│   │   └── strategy_evalution.py  <- Scripts to compute performance metrics.
│   │
│   └── utils.py                   <- data utility for configuration files.
│ 
└── requirements.txt               <- The file for reproducing the pip-based virtual environment.
```
