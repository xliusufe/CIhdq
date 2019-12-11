# CIhdq
 Regularized projection score estimation of treatment effects in high-dimensional quantile regression.
 
  A regularized projection score method is proposed for estimating treatment effects in quantile regression 
  in the presence of high-dimensional confounding covariates. This method is based on an estimated projection 
  score function of the low-dimensional treatment parameters in the presence of high-dimensional confounding 
  covariates. We propose one-step algorithm and a reffitted wild bootstrapping approach for variance estimation. 
  This enables us to construct confidence intervals for the treatment effects in the high-dimensional circumstances.
  
# Installation

    #install Rtools 3.5 (http://cran.r-project.org/bin/windows/Rtools)
    #install.packages("devtools")
    #install.packages("Rcpp")
    library(devtools)
    install_github("xliusufe/CIhdq")

# Usage

   - [x] [CIhdq-manual](https://github.com/xliusufe/CIhdq/blob/master/inst/CIhdq-manual.pdf) ------------ Details of the usage of the package.

# Example

    library(CIhdq)

    n <- 50
	d <- 3
	p <- 20
	x <- matrix(rnorm(n*d),n,d)
	z <- matrix(rnorm(n*(p-1)),n,p-1)
	y=x%*%beta+cbind(1,z)%*%eta+error*rnorm(n)
	fit <- inferen(y,x,z,tau=tau,B=500)
	ests <- fit$result
    est.coef <- cbind(est.coef,ests$coef)
	boot.var <- diag(fit$cov)
    lbounds <- ests$coef-qnorm((1+alpha)/2)*sqrt(boot.var)
    ubounds <- ests$coef+qnorm((1+alpha)/2)*sqrt(boot.var)
    counts <- ifelse(lbounds<beta&beta<ubounds,1,0)
    coverage <- cbind(coverage,counts)
 
 # References
 
Feng, X., Huang, J. and Liu, X. (2019). Regularized projection score estimation of treatment effects 
in high-dimensional quantile regression. Manuscript.

# Development

The R-package is developed by Xu Liu (liu.xu@sufe.edu.cn) and Xingdong Feng.
