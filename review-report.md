# Summary of the Paper

The goal of [Goes et al.](#goes2025) ([2025](#goes2025))'s paper is to extend the original model proposed by [Lee and Carter](#lc1992) ([1992](#lc1992)) to incorporate the effects of mortality jumps. Their methodology builds on the formulation proposed by [Liu and Li](#liuli2015) ([2015](#liuli2015)), which assumes independent and transient jumps. The authors used an autoregressive structure and a moving average structure for jump effects to introduce serial dependence. Their estimation procedure is based on the so-called *Route II* approach, as outlined by [Haberman and Renshaw](#haberman2012) ([2012](#haberman2012)), in which mortality improvements between consecutive years are modelled. The parameters were estimated using a Bayesian approach to account for uncertainty in the parameter values. The Bayesian computation was performed using the `NIMBLE` package in R ([de Valpine et al.](#dV2017), [2017](#dV2017)). The paper also includes a discussion of nonidentifiability issues of the Lee-Carter-type models, which is based on [Hunt and Blake](#hunt2020) ([2020](#hunt2020)). The authors investigated both the in-sample and out-of-sample performance of their model and found that their model outperforms the models of [Lee and Carter](#lc1992) ([1992](#lc1992)) and [Liu and Li](#liuli2015) ([2015](#liuli2015)). Empirical results on the posterior distributions of the parameters are also presented.

[Goes et al.](#goes2025) ([2025](#goes2025)) provided a new framework for modelling mortality rates, enabling a more accurate and flexible approach to model mortality rates in the presence of vanishing jumps, such as those caused by COVID-19.

# Critical Assessment 

[Goes et al.](#goes2025) ([2025](#goes2025))'s paper builds on reputable work by other researchers and specifically targets the limitations of existing methods, aiming to address their weaknesses and provide a better solution that can accommodate practical needs. The relevant background and key concepts of mortality rate modelling are clearly explained in the paper, including the motivation to incorporate vanishing jumps, the original formulation of [Lee and Carter](#lc1992) ([1992](#lc1992)), and the baseline formulation of [Liu and Li](#liuli2015) ([2015](#liuli2015)).

The use of common and technical languages is well balanced to ensure both readability and rigorousness. Mathematical notations are mostly standard and precise, and have been articulated carefully where needed so that readers can easily follow them. In addition, the arrangement of text, mathematical formulae, figures, and tables is generally well balanced throughout the paper to ensure a logic flow. The mortality data used in this paper also come from reliable sources.

Overall, this paper presents original research by the authors that is of high-quality and provides useful insights for researchers interested in further development on mortality rate modelling.

# Major Concerns and Comments 

## Limited Justification for Prior Selection 
The selection of priors in Section 3.2 appears to be highly subjective, relying heavily on weakly informative priors. The justification provided by the authors is minimal, focusing primarily on ruling out unreasonable values to narrow the range of plausible values.

The authors are advised to provide further explanation or analysis to justify their choice of priors. The authors may also want to conduct a sensitivity analysis on the priors to test the robustness of their results; it may be helpful to consult [Müller](#muller2012) ([2012](#muller2012)) for this refinement.

## Clarification Needed in Forecasting Procedure 
The forecasting procedure described in Section 4.2 appears to be ambiguous and difficult to follow. For example, the authors may want to separate Step 2 of Section 4.2 into two or more steps, as it involves generating multiple hyperparameter values before actually generating a value of $J_{T+1}^{(s)}$. In addition, the estimation relies heavily on the `NIMBLE` package in R, but it is unclear how the draws will be performed for $p^{(s)},\mu_Y^{(s)},\sigma_Y^{(s)},\varepsilon_{x,T+1}^{(s)},$ etc., from the posterior distribution. For example, do we need to marginalize the posterior distribution for each parameter before drawing? Do we draw from the joint posterior distribution directly?

If feasible, the authors may want to include a more detailed discussion on sampling from the posterior, similar to the discussions presented in [Kass et al.](#kass1998) ([1998](#kass1998)).

The authors are also advised to further elaborate on this section by incorporating specific mathematical expressions and reorganizing the argument. They may also want to move Section 4.2 to a standalone section, as it is not directly related to model comparison.

## Limited Discussion of the Multi-Population Extension 

The authors are advised to provide further justification for their multi-population formulation presented in Section 7. Upon introducing the index set $c=\{1,2,\dots,C\}$ to denote different countries, the following questions may be worth considering.

-   Do we need to consider the difference in each country's lifespan distribution due to the difference in population sizes, genetic compositions, healthcare systems, etc.?

-   Are the jump severity parameters $Y_{t,c}$ independent? For example, could there be any correlations between the jump effects of two countries that are geographically close? How do we account for such a correlation if it existed?

-   Do we use the same AR or MA structure for all countries, or do we use different structures for different countries? What are some considerations for choosing the serial dependence structures in the multi-population scenario?

## Clarification Needed on Model Comparison with Liu and Li (2015) 

The authors noted that one of the weaknesses in [Liu and Li](#liuli2015) ([2015](#liuli2015))'s formulation is the fixed age pattern of mortality jumps. However, this weakness does not apply to the J2 variant of [Liu and Li](#liuli2015) ([2015](#liuli2015)). It is understood that [Liu and Li](#liuli2015) ([2015](#liuli2015)) proposed three variants (J0, J1, and J2) of [Lee and Carter](#lc1992) ([1992](#lc1992))'s model, with the J2 variant also allowing the age patterns to vary. The authors are advised to clarify this point in their paper.

Furthermore, the authors are advised to elaborate on their model comparison with [Liu and Li](#liuli2015) ([2015](#liuli2015))'s model. More specifically, while the authors claimed that their model outperformed [Liu and Li](#liuli2015) ([2015](#liuli2015))'s model, they did not explicitly indicate which of the J0, J1, and J2 variants was used for comparison. The authors are advised to clarify this as well.

## Clarification Needed on Enforcement of Identifiability Constraints 

The authors discussed the nonidentifiability issues in the Lee-Carter-type models, but did not explain how the identifiability constraints were enforced during model estimation. It is understood that multivariate Dirichlet priors were used to implicitly impose the constraints on $(\beta_1,\dots,\beta_A)$ and $(\beta_1^{(J)},\dots,\beta_A^{(A)})$, but it is unclear how the other constraints were implemented.

The authors are advised to clarify this point by providing more details on how the identifiability constraints were implemented during the estimation. Specifically, were the constraints enforced through prior specifications, manual parameter fixing in `NIMBLE`, or other suitable techniques?

## Limited Discussion of the Robustness of Main Results 

The authors may want to discuss the robustness of their results, as there are several factors that could potentially affect model performance; for example, the choice of priors, the types of samplers used in the estimation.

The authors may want to consider addressing the following questions.

-   How would the results differ if we used data from countries other than the U.S., Spain, and Poland?

-   Would the results differ if different samplers were used in the parameter estimation?

-   Were there any convergence issues for the model parameters that might have an impact on the results?

Also, as mentioned in the *Major Concerns and Comments* of this report, would the results differ if we change the priors?

# Minor Concerns and Comments 

-   **The Notation $\beta_x^{(J)}$ for Age Patterns**\
    The authors may want to reconsider the use of $\beta_x^{(J)}$ for age patterns in their formulation. The authors also used $\beta_x^{(J)}$ in their description of [Liu and Li](#liuli2015) ([2015](#liuli2015))'s J1 model, but [Liu and Li](#liuli2015) ([2015](#liuli2015)) considered $\beta_x^{(J)}$ to be fixed quantities. Confusion may arise for this reason.

-   **Choice of Bayesian Framework**\
    The authors may want to provide a brief justification for their choice of the Bayesian framework over the frequentist framework. This can improve readability for readers unfamiliar with the use of Bayesian inference in mortality rate modelling.

-   **Advantages of A Joint Jump Occurrence**\
    The authors may want to elaborate on the last paragraph of Section 7.2, where they highlight the advantage of a single jump occurrence in the multi-population scenario. In particular, why is a single jump occurrence better than multiple jump occurrences in terms of forecasting in the multi-population case? What are the considerations and implications here?

# Recommendation for Decision

Upon review, we recommend the following decision.

-   *Accept* with revisions needed.

The paper presents high-quality research on mortality rate modelling, offering both theoretical and practical insights for further work in this area. To enhance soundness, readability, and presentation, it is recommended that the authors carefully review the comments outlined above and incorporate the suggestions where feasible.

# References 

de Valpine, P., Turek, D., Paciorek, C. J., Anderson-Bergman, C., Temple Lang, D., and Bodik, R. (2017). Programming With Models: Writing Statistical Algorithms for General Model Structures With NIMBLE. Journal of Computational and Graphical Statistics, 26(2), 403--413.


Goes, J., Barigou, K., and Leucht, A. (2025). Bayesian Mortality Modelling With Pandemics: A Vanishing Jump Approach. Journal of the Royal Statistical Society: Series C (Applied Statistics), 00, 1--33.



Haberman, S., and Renshaw, A. E. (2012). Parametric Mortality Improvement Rate Modelling and Projecting. Insurance: Mathematics and Economics, 50(3), 309--333.



Hunt, A., and Blake, D. (2020). Identifiability in Age/Period Mortality Models. Annals of Actuarial Science, 14(2), 461--499.



Kass, R. E., Carlin, B. P., Gelman, A., and Neal, R. M. (1998). Markov Chain Monte Carlo in Practice: A Roundtable Discussion. The American Statistician, 52(2), 93--100.



Lee, R. D., and Carter, L. R. (1992). Modeling and Forecasting U.S. Mortality. Journal of the American Statistical Association, 87(419), 659--671.



Liu, Y., and Li, J. S.-H. (2015). The Age Pattern of Transitory Mortality Jumps and Its Impact on the Pricing of Catastrophic Mortality Bonds. Insurance: Mathematics and Economics, 64, 135--150.



Müller, U. K. (2012). Measuring Prior Sensitivity and Prior Informativeness in Large Bayesian Models. Journal of Monetary Economics, 59(6), 581--597.

