
<!-- README.md is generated from README.Rmd. Please edit that file -->

# IPD: Inference on Predicted Data

<!-- badges: start -->

[![R-CMD-check](https://github.com/awanafiaz/IPD/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/awanafiaz/IPD/actions/workflows/R-CMD-check.yaml)
<!-- badges: end -->

## <img src="man/figures/IPD_LOGO.png" align="right" height="200" style="float:right; height:200px;">

With the rapid advancement of artificial intelligence (AI), machine
learning (ML) algorithms and owing to financial and domain-specific
constraints, researchers from a wide variety of disciplines are now
increasingly utilizing predictions from pre-trained AI/ML algorithms as
outcome variables in statistical analyses. However, treating these
predicted values as naturally occurring observations, although appealing
for financial and logistical reasons, have been shown to produce biased
estimates and misleading inference ([Wang et al.,
2020](https://www.pnas.org/doi/suppl/10.1073/pnas.2001238117)). The
statistical challenges encountered when conducting Inference on
Predicted Data (IPD) include: (1) correct specification of the
relationship between predicted outcomes and their true unobserved
counterparts, (2) accounting for the robustness of AI/ML models to
resampling or uncertainty about the training data, and (3) appropriately
propagating both bias and uncertainty from predictions into downstream
inferential procedures.

There now exists multiple approaches that address this general problem
as increasing number of researchers are attempting to come up with
statistically valid and efficient methods to solve the aforementioned
challenges. These approaches include Post-prediction inference (PostPI)
by [Wang et al.,
2020](https://www.pnas.org/doi/suppl/10.1073/pnas.2001238117),
Prediction-powered inference (PPI) by [Angelopoulos et al.,
2023](https://www.science.org/doi/10.1126/science.adi6000) and its
modified version [PPI++ (Angelopoulos et al.,
2023)](https://arxiv.org/abs/2311.01453), and Assumption-lean and
Data-adaptive Post-Prediction Inference (POP-Inf) by [Miao et al.,
2023](https://arxiv.org/abs/2311.14220). These methods have been
developed in quick succession in response to the growing practice of
using predicted data directly into statistical analyses. For the purpose
of allowing researchers and practitioners to fully utilize these
powerful and state-of-the-art methods to conduct their statistical
analyses, we have developed the `IPD` r-package to provide software
support to researchers so that all extant methods can be utilized under
the umbrella of a single r-package.

To make the utilization of the package convenient for users, we provide
guidance on installation and use of the package and its functions in the
following section.

## Installation

You can install the development version of `IPD` from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")   ## If devtools is not already installed
devtools::install_github("awanafiaz/IPD")
```

## Usage

We provide a simple example to demonstrate the basic use of the
functions included in `IPD`. We build the premise in the following
manner to build an unifying example to be used across all available
methods.

(i). Assume that we have access to a well-performing and fairly accurate
AI/ML/DL algorithm $f_{\text{x}}(\cdot)$ that can predict our outcome of
interest $Y$.

(ii). Next, consider that we have 2 data sets, a labeled data set (which
we will call the **test set** $(X_{te}, Y_{te})$), and an unlabeled data
set (which we call the **validation set** $(X_{val)}$). Typically the
the labeled/test set is considerably smaller in size compared to the
unlabeled/validation set. Here we will consider them to be equal for
brevity.

- We consider the regressors, $X = (X_1, X_2, X_3, X_4)$ and let $Y$ be
  a scalar.
- The true data generating mechanism is
  $Y = \beta_1X_1 + \beta_2 X_2 + \beta_3 \ g(X_3) + \beta_4 \ g(X_4) + \epsilon,$
  where, $\epsilon = N(0, 1)$ and $g(\cdot)$ refers to some smoother
  function.
- We specify, $(\beta_1, \beta_2, \beta_3, \beta_4) = (1, 0.5, 3, 4)$.

(iii). Our interest is in performing inference on $H_0: \beta_1^* = 0$
vs $H_1: \beta_1^* \ne 0$. That is, our inference model is,

$$
Y_{val} = \beta_0^* + \beta_1^* X_{val} + \epsilon^*,
$$

where $\epsilon^* = N(0, 1)$.

(iv). However, we do not observe $Y_{val}$. We instead only have access
to the predicted $\hat Y_{val} = f_{\text{x}}(X_{val})$.

## Vignette

For more advanced users and researchers, we provide more use cases and
examples in the package `vignettes`.

``` r
vignette("IPD")
```

This provides an extensive tutorial on `IPD` and discusses
method-specific usage in details.

## Feedback

For questions and comments or any other feedback, please contact the
developers.
