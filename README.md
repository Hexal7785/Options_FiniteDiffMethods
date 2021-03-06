# Options_FiniteDiffMethods
OptionValuation - FiniteDifferenceMethods Implicit &amp;Explicit- Binomial, BlackScholes,

Option Pricing with Finite Difference Methods in R

This repository demonstrates several Finite difference methods for option pricing. There is:

	* implicit finite difference method


	* explicit finite difference method

	* Crank-Nicolson scheme

Log - Outputted from Put_Pricing_Comparison.R
---------------

$ R

R version 3.4.2 (2017-09-28) -- "Short Summer"
Copyright (C) 2017 The R Foundation for Statistical Computing
Platform: x86_64-w64-mingw32/x64 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.


> source('Option_Pricing_FDiffs_Binomial_BS.R')
> 
> ######################################################################
> ## European put                                                     ##
> ######################################################################
> 
> s <- 10
> k <- 10
> r <- .04
> t <- .5
> sd <- .2
> dt <- .002
> dx <- c(sd*sqrt(dt), sd*sqrt(3*dt), sd*sqrt(4*dt))
> type <- 'put'; style <- 'european'
> 
> ## Binomial or Black-Scholes-Merton for comparison
> if (type == 'put' && style == 'american') {
+   binom.american.put(s, k, r, t, sd, n=1e3)
+ } else
+   bsm.option(s, k, r, t, sd, type)
[1] 0.4646945
> 
> ## Regular implementation.
> fde.log(s, k, r, t, sd, type=type, style=style)
[1] 0.4623372
> fdi.log(s, k, r, t, sd, type=type, style=style)
[1] 0.4642185
> fdcn.log(s, k, r, t, sd, type=type, style=style)
[1] 0.4621469
> 
> ## Convergence demonstration.
> n <- round(t/dt)
> m <- round(6*sd*sqrt(t)/dx[1])          # dx = sd*sqrt(dt)
> fde.log(s, k, r, t, sd, n, m, type, style)
[1] -67.22841
> fdi.log(s, k, r, t, sd, n, m, type, style)
[1] 0.4642181
> fdcn.log(s, k, r, t, sd, n, m, type, style)
[1] 0.4623665
> 
> m <- round(6*sd*sqrt(t)/dx[2])          # dx = sd*sqrt(3*dt)
> fde.log(s, k, r, t, sd, n, m, type, style)
[1] 0.4619982
> fdi.log(s, k, r, t, sd, n, m, type, style)
[1] 0.4637008
> fdcn.log(s, k, r, t, sd, n, m, type, style)
[1] 0.4616131
> 
> m <- round(6*sd*sqrt(t)/dx[3])          # dx = sd*sqrt(4*dt)
> fde.log(s, k, r, t, sd, n, m, type, style)
[1] 0.4616075
> fdi.log(s, k, r, t, sd, n, m, type, style)
[1] 0.463417
> fdcn.log(s, k, r, t, sd, n, m, type, style)
[1] 0.4612192
> 
> 
> ######################################################################
> ## American put                                                     ##
> ######################################################################
> 
> s <- 10
> k <- 10
> r <- .04
> t <- .5
> sd <- .2
> dt <- .002
> ds <- c(0.5, 1, 1.5)
> type <- 'put'; style <- 'american'
> 
> ## Binomial or Black-Scholes-Merton for comparison
> if (type == 'put' && style == 'american') {
+   binom.american.put(s, k, r, t, sd, n=1e3)
+ } else
+   bsm.option(s, k, r, t, sd, type)
[1] 0.4827014
> 
> ## Regular implementation.
> fde(s, k, r, t, sd, type=type, style=style)
[1] 0.4803301
> fdi(s, k, r, t, sd, type=type, style=style)
[1] 0.4798712
> fdcn(s, k, r, t, sd, type=type, style=style)
[1] 0.4822621
> 
> ## Convergence demonstration.
> n <- round(t/dt)
> m <- round(2*s/ds[1])                   # ds = 0.5
> fde(s, k, r, t, sd, n, m, type, style)
[1] 0.4733109
> fdi(s, k, r, t, sd, n, m, type, style)
[1] 0.4724533
> fdcn(s, k, r, t, sd, n, m, type, style)
[1] 0.480942
> 
> m <- round(2*s/ds[2])                   # ds = 1
> fde(s, k, r, t, sd, n, m, type, style)
[1] 0.4399607
> fdi(s, k, r, t, sd, n, m, type, style)
[1] 0.4390812
> fdcn(s, k, r, t, sd, n, m, type, style)
[1] 0.475788
> 
> m <- round(2*s/ds[3])                   # ds = 1.5
> fde(s, k, r, t, sd, n, m, type, style)
[1] 0.394225
> fdi(s, k, r, t, sd, n, m, type, style)
[1] 0.3933963
> fdcn(s, k, r, t, sd, n, m, type, style)
[1] 0.4684005
