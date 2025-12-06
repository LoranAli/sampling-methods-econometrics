# Sampling Methods for Business Population in Sector G (Sweden)

This project compares two probability sampling designs—**Simple Random Sampling Without Replacement (OSU)** and **Stratified Random Sampling Without Replacement with Neyman Allocation (STOSU)**—using simulated data from Sweden’s business sector **G (Wholesale; repair of motor vehicles and motorcycles)**.

The goal is to estimate key economic parameters such as total turnover, average investment, and total employment, and to evaluate how sampling design affects precision and variance.

A domain analysis focusing on **small companies (≤ 20 employees)** is also included.

---

## Dataset

- **Source:** Simulated Excel dataset of companies in SNI2007 Sector G, segment 46  
- **Population size:** ~39,654 companies  
- **Sample size:** ~4,500 companies  
- **Key variables:**
  - `nace` — 4-digit industry code  
  - `Turn_admin` — administrative turnover (true values may include zeros)  
  - `turn` — survey-reported turnover  
  - `inv` — survey-reported investments  
  - `N_emp` — number of employees  
  - `emp_sbs` — employees in survey  
  - `scope` — target population indicator (1 = in scope)

---

## Research Questions

1. How well does OSU estimate:
   - Total turnover  
   - Average investment  
   - Total employees  
   - Domain estimates for small firms?

2. How does **STOSU** improve:
   - Variance  
   - Precision  
   - Stability of estimates?

3. What is the added value of **domain estimation** for small companies?

4. Which sampling method is most suitable for analyzing heterogeneous business populations?

---

## Methodology

### **OSU — Simple Random Sampling Without Replacement**
- Unbiased for totals and means  
- Higher variance due to high population heterogeneity  
- Estimates fluctuate more for turnover and investment

### **STOSU — Stratified Sampling (Neyman Allocation)**
- Stratification based on number of employees (`N_emp`)  
- Neyman allocation assigns larger sample fractions to strata with higher variance  
- Dramatically reduces variance and increases estimate precision  
- Especially effective for totals and domain values  

### **Estimators & Functions Used**
- **Horvitz–Thompson estimator (HT)**  
- **HT variance estimator**  
- Functions from R packages:
  - `strata()`, `getdata()`, `HTestimator()`, `varest()`  
- Implemented for both sampling designs

---

## Key Results

### True Population Values  
Calculated from the full dataset (`scope = 1`) and used as benchmarks.

### OSU Results  
- Unbiased but highly variable  
- Tends to over/underestimate totals  
- Variance large for turnover and investment  
- Domain estimates less stable

### STOSU Results  
- Much lower variance for all parameters  
- Significantly more precise totals  
- Domain estimates for **small companies (≤ 20 employees)** very close to true values  
- Demonstrates the importance of stratification when auxiliary info is correlated with study variables

### Domain Analysis  
Shows large structural differences between small and large firms.  
Important implications for:
- Structural business statistics  
- Economic policy  
- SME-focused research  

---

## Conclusions

- **Stratified sampling with Neyman allocation is far superior** to OSU for this population.  
- When auxiliary variables (like employees) correlate with study variables (turnover, investment), stratification greatly improves efficiency.  
- Domain estimation is essential for understanding specific subpopulations such as small enterprises.  
- Future improvements:
  - Ratio estimators  
  - Regression estimators  
  - Inclusion of administrative register data  

The choice of sampling design profoundly affects precision, variance, and reliability of survey estimates.

---

## How to Run

1. Place `data.xlsx` in the project directory  
2. Open `analysis.R` in RStudio  
3. Install required packages:

```r
install.packages(c("sampling", "rio"))
