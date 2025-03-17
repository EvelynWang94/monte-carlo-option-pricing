# monte-carlo-option-pricing
Monte Carlo Simulation for Option Pricing | Variance Reduction | Greeks Sensitivity Implementing Monte Carlo methods for European and barrier options, with variance reduction techniques and Greeks analysis.
# Monte Carlo Simulation for Option Pricing

## 📌 Project Overview
This project implements a Monte Carlo Simulation for option pricing, covering:
- **Biased European Options**: Convergence analysis with different random number generators (RNGs).
- **Up-and-Out Barrier Options**: Sensitivity analysis on $\partial V / \partial \beta$.
- **Variance Reduction Techniques**: Antithetic Variates, Moment Matching, Halton Sequence.
- **Computational Efficiency Analysis**: Performance trade-offs between methods.

Monte Carlo methods are widely used for pricing derivatives in financial markets, especially when closed-form solutions are unavailable. This project aims to enhance simulation efficiency and improve pricing accuracy.

## 📊 Mathematical Background

### 1️⃣ **Biased European Option Pricing & Convergence Analysis**
European option with piecewise constant payoff:

$$
 C(S_T, T) = g(S_T) =
    \begin{cases}
        X_1 - X_2, & \text{if } S_T < X_1, \\
        X_1, & \text{if } X_1 \leq S_T < X_2, \\
        X_2 - X_1, & \text{if } S_T \geq X_2.
    \end{cases}
$$

Using different variance-reduction methods:
- **Standard MC**: Baseline Monte Carlo estimation.
- **Antithetic Variates (AV)**: Using inverse pairs \( Z \) and \( -Z \) to reduce variance.
- **Moment Matching**: Adjusting samples to enforce zero mean and unit variance.
- **Halton Sequence**: Quasi-random low-discrepancy sequences for better convergence.
- **RNG Comparison**: Using different random number sequences for experiment.

Key finding: **Halton Sequence** significantly improves accuracy, reducing error by **90%**, although it increases computational time by **2.5x**.

### 2️⃣ **Up-and-Out Barrier Option Pricing**
A barrier option becomes worthless if the underlying asset crosses a predefined barrier level \( B \). The payoff is:

$$
V = \begin{cases}
  e^{-rT} \max(S_T - K, 0), & \text{if } S_t < B , \forall t \in [0, T] \\
  0, & \text{otherwise}
\end{cases}
$$

We analyze **sensitivity of Greeks $\partial V / \partial \beta$** by comparing variance reduction techniques:
- **Standard MC**
- **Quasi-Monte Carlo (QMC)**
- **Importance Sampling**
- **Antithetic Variates**
- **Control Variates**

Results show that **Halton Sequence (QMC) provides the best accuracy**, with the smallest confidence interval width, despite a higher computational cost.

## 💻 Implementation Details
- **Programming Language**: Python (NumPy, SciPy, Matplotlib, Pandas)
- **Key Components**:
  - `monte_carlo.py`: Monte Carlo simulation for biased European and barrier options.
  - `variance_reduction.py`: Antithetic Variates, Moment Matching, Halton Sequence.
  - `greeks.py`: Sensitivity analysis of Greeks.
  - `rng_analysis.py`: Examines bias in random number generation.
  - `plot_results.py`: Visualizes convergence and variance reduction impact.

## 📈 Experimental Results
### 1️⃣ **Convergence Analysis for European Options**
| Method | Error Reduction | Computation Time Increase |
|--------|----------------|------------------------|
| Standard MC | Baseline | 1x |
| Antithetic Variates | No Effect | No Effect |
| Moment Matching (N < 10⁴) | 20% | No Effect |
| Halton Sequence | 90% | 2.5x |

### 2️⃣ **Variance Reduction for Up-and-Out Call Option Sensitivity Analysis**
| Method | Mean \( \partial V / \partial \beta \) | CI Lower | CI Upper | CI Width |
|--------|-------------------|------------|------------|----------|
| Standard MC | 8.2525 | -4.8133 | 21.3184 | 26.1317 |
| Quasi-MC (QMC) | 10.9631 | 2.6146 | 19.3116 | 16.6971 |
| Importance Sampling | 5.2569 | -3.6974 | 14.2114 | 17.9088 |
| Antithetic Variates | 8.2497 | -0.5133 | 17.0127 | 17.5260 |
| Control Variate | 8.3199 | -4.6243 | 21.2641 | 25.8884 |


## 🚀 Running the Code & Viewing Results

All code, analysis, and results are contained in the Jupyter Notebook.  
📌 Open: [monte_carlo_option_pricing.ipynb](monte-carlo-option-pricing.ipynb)

### Run the Notebook Locally  
1️⃣ **Clone the repository**  
   ```bash
   git clone https://github.com/EvelynWang94/monte-carlo-option-pricing.git
   cd monte-carlo-option-pricing
   ```
2️⃣ **Install dependencies**  
   ```bash
   pip install numpy scipy pandas matplotlib
   ```
3️⃣ **Launch Jupyter Notebook**  
   ```bash
   jupyter notebook monte_carlo_option_pricing.ipynb
   ```
4️⃣ **Run the cells** in the Notebook to generate results. 

## 📂 Project Structure
```
monte-carlo-option-pricing/
│── README.md
│── requirements.txt  # Dependency list
│── monte_carlo_option_pricing.ipynb  # Jupyter Notebook containing all code & analysis
└── data/  # Stores experimental results
```

## 🔜 Future Improvements
- Implement **Quasi-Monte Carlo (Sobol Sequences)** for further convergence improvements.
- Optimize performance with **Numba/Cython**.
- Extend to **American Options** using Least Squares Monte Carlo (LSMC).

## 📬 Contact
📧 Feel free to reach out for collaboration or discussions!
- **LinkedIn**: [Yuchen Wang](https://www.linkedin.com/in/yuchen-wang-2aa64327b/)
- **Email**: 18710117882@163.com
- **GitHub**: [EvelynWang94](https://github.com/EvelynWang94/)
