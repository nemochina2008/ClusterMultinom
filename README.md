ClusterMultinom
================

Current Status: UNDER CONSTRUCTION
----------------------------------

Purpose
-------

ClusterMultinom provides a suite of functions to make the process of fitting multinomial logistic regression models with clustered data, as well as extracting and visualizing meaningful results from those models, as painless as possible.

Current Capabilities
--------------------

The package assumes your multinomial logistic regression model will be fit using `VGAM::vglm(..., family = multinomial(...))`, and that you want to calculate variance of beta coefficients using the bootstrap. It also allows for multiple imputation, using the [`mice`](https://CRAN.R-project.org/package=mice) package and following the "boot MI" procedure recommended by [Schomaker & Heumann](https://arxiv.org/abs/1602.07933).

The functions included mirror the following steps:

1.  `create_bootdata()`: Create `B` datasets.
    -   Optional: Multiply impute each dataset `M` times.
    -   **NOTE: FUNCTIONALITY CURRENTLY ENDS HERE**
2.  Fit the same model to each bootstrapped dataset (or set of imputations), saving errors/warnings of failed model fits and saving coefficients of successful model fits.
3.  Create a vector of point estimates, and a corresponding variance-covariance matrix, for all model coefficients.
4.  Hypothesis testing for individual coefficients or for groups of coefficients.
5.  Calculate odds ratios and confidence limits for a coefficient.
6.  Calculate predicted probabilities and confidence limits for each outcome level, given a matrix of **X** values.

The functions are written and exported so that the user can access each step of the process independently if needed; however, wrappers are also provided to perform common tasks which fall completely within the context of the package.

Dependencies
------------

Currently, `purrr` is **Imported** and all other package dependencies are **Suggested**. Those suggested packages include, in order of importance:

1.  [`VGAM`](https://cran.r-project.org/package=VGAM): We chose `VGAM::vglm()` for our multinomial logistic regression fits because it produces the most conservative warning messages of the options we tried, which are important when fitting a potentially unstable model to many bootstrapped datasets.
2.  [`mice`](https://cran.r-project.org/package=mice): `mice` is a popular package for multiple imputation, providing plenty of opportunity for customization and modeling.
3.  [`gapminder`](https://cran.r-project.org/package=gapminder): Required only to run examples.
4.  [`testthat`](https://cran.r-project.org/package=testthat): Required only for testing.

Future Directions/Collaboration Opportunities
---------------------------------------------

1.  Including sandwich estimation in addition to bootstrap methods to calculate coefficient variances.
2.  Adding flexibility such that `purrr` need not be installed to use this package.
3.  Adding methods for `mlogit` or `nnet::multinom()` model fits, in addition to `VGAM::vglm()`.

Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.
