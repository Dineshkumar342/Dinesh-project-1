
Causal Inference Using Double Machine Learning (DML)
1. Introduction

Understanding causal effects is essential in situations where we want to estimate the true impact of a treatment or intervention. Traditional statistical models such as Ordinary Least Squares (OLS) often fail when there are many confounding variables or when relationships are nonlinear.

This project applies Double Machine Learning (DML) to estimate the Average Treatment Effect (ATE) and investigate Heterogeneous Treatment Effects (CATE) using machine-learning models. DML provides a principled way to remove confounding bias even in high-dimensional settings.

A synthetic dataset was generated to ensure full control over the data-generating process and to properly evaluate the performance of the method.

2. Synthetic Data Generation

A dataset containing 3000 observations and 50 covariates was programmatically generated. These covariates act as confounders that influence both the treatment assignment and the final outcome.

Treatment (T): Binary variable (0 or 1)

Outcome (Y): Continuous variable

Covariates (X1 to X50): High-dimensional confounding variables

The treatment probability was designed using a logistic model based on selected covariates, ensuring genuine confounding. The outcome was generated from a nonlinear function of covariates, combined with a heterogeneous treatment effect that varies according to X1 and X2. Random noise was added to replicate realistic data.

This controlled environment makes it possible to evaluate the accuracy of causal estimators.

3. Methodology
3.1 Double Machine Learning Framework

The Double Machine Learning approach consists of three major steps:

Model the outcome:
Machine-learning model estimates 
𝑚
^
(
𝑋
)
=
𝐸
[
𝑌
∣
𝑋
]
m
^
(X)=E[Y∣X].

Model the treatment assignment:
Machine-learning classifier estimates

𝑒
^
(
𝑋
)
=
𝐸
[
𝑇
∣
𝑋
]
e
^
(X)=E[T∣X], the propensity score.

Residualize both variables:

𝑌
res
=
𝑌
−
𝑚
^
(
𝑋
)
Y
res
	​

=Y−
m
^
(X)

𝑇
res
=
𝑇
−
𝑒
^
(
𝑋
)
T
res
	​

=T−
e
^
(X)

Regress residualized outcome on residualized treatment:
The slope from this regression is the debiased ATE estimate.

This process removes the influence of confounders and produces a consistent estimate of the treatment effect.

3.2 Machine Learning Models Used

Random Forest Regressor for estimating the outcome model.

Random Forest Classifier for estimating the treatment model.

5-fold cross-fitting to prevent overfitting and ensure unbiased predictions on held-out data.

Linear Regression on the residuals for the final ATE estimate.

This combination follows standard recommendations in modern causal inference literature.

4. Estimation Results
4.1 Average Treatment Effect (ATE)

The Double Machine Learning estimator produced:

ATE ≈ 0.99

Interpretation:
On average, receiving the treatment increases the outcome by approximately 1 unit, after properly adjusting for all confounding variables.

4.2 Comparison with Naive OLS

OLS regression using only Y ~ T gave a different estimate (usually much higher or lower).
This happens because OLS does not adjust for confounding, and therefore produces a biased estimate.

DML corrects this by removing the influence of all covariates using machine learning, leading to a more reliable causal effect.

5. Heterogeneous Treatment Effects (CATE)

To explore how treatment effects vary across individuals, a T-Learner was used:

One model predicts the potential outcome if treated: 
𝜇
^
1
(
𝑋
)
μ
^
	​

1
	​

(X)

Another predicts the potential outcome without treatment: 
𝜇
^
0
(
𝑋
)
μ
^
	​

0
	​

(X)

Their difference gives the individual CATE:

𝜏
(
𝑋
)
=
𝜇
^
1
(
𝑋
)
−
𝜇
^
0
(
𝑋
)
τ(X)=
μ
^
	​

1
	​

(X)−
μ
^
	​

0
	​

(X)

Key Findings

The distribution of CATE showed that treatment effects differ widely across individuals.

Covariates X1 and X2 were identified as the most influential in determining treatment effect size.

Individuals with higher values of these covariates tended to exhibit larger treatment effects.

Visualizations included in the analysis:

Histogram of CATE values

Feature importance plot showing top influential covariates

Scatter plots of CATE vs X1 and CATE vs X2

Propensity score distribution plot

These visualizations clearly demonstrate the presence of heterogeneity and the factors driving it.

6. Sensitivity Analysis
6.1 Overlap (Propensity Score Check)

The estimated propensity scores were within acceptable bounds, indicating adequate overlap between treated and untreated groups. This confirms that the treatment effect is identifiable.

6.2 Residual Diagnostics

The residuals from both nuisance models were centered around zero, indicating that the machine-learning models were trained properly and not systematically biased.

This supports the validity of the DML procedure.

7. Conclusion

This project successfully implemented Double Machine Learning to estimate causal effects in a high-dimensional environment with many confounders. The method produced a reliable estimate of the Average Treatment Effect and revealed substantial variation in individual-level treatment effects.

Key achievements:

Generated a realistic synthetic dataset with confounding and heterogeneity

Implemented a full DML pipeline with cross-fitting

Estimated an unbiased ATE

Compared DML with naive OLS

Examined heterogeneous treatment effects using a T-Learner

Performed sensitivity checks to validate the model assumptions

The project demonstrates how modern machine-learning-based causal inference can outperform traditional methods and provide a clearer understanding of treatment effects at both average and individual levels.
