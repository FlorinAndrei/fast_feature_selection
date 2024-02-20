# fast_feature_selection

Genetic algorithms and CMA-ES (covariance matrix adaptation evolution strategy) for efficient feature selection

This is the companion repository for a series of two articles I've published on Medium, on the topic of efficient feature selection for regression models:

[Efficient Feature Selection via CMA-ES (Covariance Matrix Adaptation Evolution Strategy)](https://towardsdatascience.com/efficient-feature-selection-via-cma-es-covariance-matrix-adaptation-evolution-strategy-ee312bc7b173)

[Efficient Feature Selection via Genetic Algorithms](https://towardsdatascience.com/efficient-feature-selection-via-genetic-algorithms-d6d3c9aff274)

The work described in the first article is mentioned (ref. [6]) in the paper [cmaes : A Simple yet Practical Python Library for CMA-ES](https://arxiv.org/abs/1604.00772) by Nomura M. and Shibata M. (2024) as a noteworthy application of CMA-ES with Margin.

**Tech details:**

I've used the [House Prices](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data) dataset from Kaggle. After some processing, the dataset yields 213 features with 1453 observations.

The model used for regression is `statsmodels.api.OLS()`. The objective function used to select the best features is BIC, or the Bayesian Information Criterion - less is better.

Three feature selection techniques are explored:

- Sequential Feature Search (SFS) implemented via the [mlxtend](https://github.com/rasbt/mlxtend) library
- Genetic Algorithms (GA) implemented via the [deap](https://github.com/DEAP/deap) library
- Covariance Matrix Adaptation Evolution Strategy (CMA-ES) implemented via the [cmaes](https://github.com/CyberAgentAILab/cmaes) library

SFS and GA used a multiprocessing pool with 16 workers to run the objective function. CMA-ES used a single process for everything.

**Results:**

Run time (less is better):

```
SFS:    42.448 sec
GA:     158.027 sec
CMA-ES: 48.326 sec
```

Number of times the objective function was invoked (less is better):

```
SFS:    22791
GA:     600525
CMA-ES: 20000
```

Objective function best value found (less is better):

```
baseline BIC: 34570.1662
SFS:          33708.9860
GA:           33705.5696
CMA-ES:       33703.0705
```
