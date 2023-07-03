# dcmle: Hierarchical Models Made Easy with Data Cloning

[![CRAN version](https://www.r-pkg.org/badges/version/dcmle)](https://CRAN.R-project.org/package=dcmle)
[![CRAN RStudio mirror downloads](https://cranlogs.r-pkg.org/badges/grand-total/dcmle)](https://www.rdocumentation.org/packages/dcmle/)

S4 classes around infrastructure
provided by the 
[**dclone**](https://github.com/datacloning/dclone) 
package to make package
development with data cloning for hierarchical
models easy as a breeze.

Sequential and parallel MCMC support
for JAGS, WinBUGS, OpenBUGS, and Stan.
See Solymos 2010 ([R Journal 2(2):29--37](https://journal.r-project.org/archive/2010-2/RJournal_2010-2_Solymos.pdf)).

## Versions

Install the CRAN version of the package from R:

```R
install.packages("dcmle")
```

Install the development version of the package from R using the
`devtools` package:

```R
devtools::install_github("datacloning/dcmle")
```

User visible changes in the package are listed in the [NEWS](https://github.com/datacloning/dcmle/blob/master/NEWS.md) file.

## Examples

State space model:

```R
## Data and model taken from Ponciano et al. 2009
## Ecology 90, 356-362.
paurelia <- c(17,29,39,63,185,258,267,392,510,
    570,650,560,575,650,550,480,520,500)
paramecium <- new("dcFit")
paramecium@data <- list(
    ncl=1,
    n=length(paurelia),
    Y=dcdim(data.matrix(paurelia)))
paramecium@model <- function() {
    for (k in 1:ncl) {
        for(i in 2:(n+1)){
            Y[(i-1), k] ~ dpois(exp(X[i, k])) # observations
            X[i, k] ~ dnorm(mu[i, k], 1 / sigma^2) # state
            mu[i, k] <- X[(i-1), k] + log(lambda) - log(1 + beta * exp(X[(i-1), k]))
        }
        X[1, k] ~ dnorm(mu0, 1 / sigma^2) # state at t0
    }
    beta ~ dlnorm(-1, 1) # Priors on model parameters
    sigma ~ dlnorm(0, 1)
    tmp ~ dlnorm(0, 1)
    lambda <- tmp + 1
    mu0 <- log(2)  + log(lambda) - log(1 + beta * 2)
}
paramecium@multiply <- "ncl"
paramecium@unchanged <- "n"
paramecium@params <- c("lambda","beta","sigma")

(m1 <- dcmle(paramecium, n.clones=1, n.iter=1000))
(m2 <- dcmle(paramecium, n.clones=2, n.iter=1000))
(m3 <- dcmle(paramecium, n.clones=1:3, n.iter=1000))

cl <- makePSOCKcluster(3)
(m4 <- dcmle(paramecium, n.clones=2, n.iter=1000, cl=cl))
(m5 <- dcmle(paramecium, n.clones=1:3, n.iter=1000, cl=cl))
(m6 <- dcmle(paramecium, n.clones=1:3, n.iter=1000, cl=cl,
    partype="parchains"))
(m7 <- dcmle(paramecium, n.clones=1:3, n.iter=1000, cl=cl,
    partype="both"))
stopCluster(cl)
```

Visit the [dcexamples](https://github.com/datacloning/dcexamples) 
repository for classic BUGS examples using **dcmle**.

## Help

Find help on the [Dclone users mailing list](https://groups.google.com/forum/#!forum/dclone-users).
More resources at [datacloning.org](http://datacloning.org).

Use the [issue tracker](https://github.com/datacloning/dcmle/issues)
to report a problem.

## References

Solymos, P., 2010. dclone: Data Cloning in R. R Journal 2(2):29--37. [[PDF](https://journal.r-project.org/archive/2010-2/RJournal_2010-2_Solymos.pdf)]
