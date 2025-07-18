# dcmle package version history

## Version 0.4-2, July 12, 2025

* Use Authors@R field in DESCRIPTION.
* Fix documentation.

## Version 0.4-1, July 4, 2023

* Removing undocumented .dcmle internal function from NAMESPACE
  after failed CRAN checks.

## Version 0.4-0, July 3, 2023

* Spell checks.
* More coda methods added: cumuplot, HPDinterval, rejectionRate.
* Added Stan support.

## Version 0.3-1, Jan 14, 2016

* str method for dcCodaMCMC class confusingly parsed the object
  as an mcmc.list (MCMClist) object. The true S4 nature of the
  object is now revealed (show method also relies on str).
* snowWrapper in dclone is now deprecated, NAMESPACE reflects this.

## Version 0.3-0, Jan 12, 2016

* NAMESPACE changes triggered by CRAN checks.
* Fixing S4 methods related Rd changes.
* Fixing import issue with coda::as.mcmc.list generic.
  The coda:::as.mcmc.list.default is replicated
  as the internal .as_mcmc_list_default function.
* Fixing update method for dcmle class: R-devel gave NOTE,
  call was not properly updated in return object.
* dcexample function is defunct.
  The R-Forge example repo is moved to:
  https://github.com/datacloning/dcexamples

## Version 0.2-4, Sep 27, 2013

* Reference for .GlobalEnv replaced by parent.frame() in
  sourceDcExample, also the assign.global argument is no
  longer used. The envir argument can be set instead.
  No assignment is made when envir=NULL.
* gelman.plot generic documentation added.
* dcmle: reflects changes in dclone due to addition of
  bugs.parfit and all partypes in dc.parfit.
* flavour slot can be 'jags', 'bugs', or any of
  'winbugs', 'openbugs', 'brugs' referring to the
  program argument in bugs.*fit.
* Removed ::: to satisfy R 3.0.2 check.
* snow is not suggested in DESCRIPTION.

## Version 0.2-3, Mar 1, 2013

* gsFit: gained flavour argument.
* gelman.plot: now implemented for dcmle classes as generic.

## Version 0.2-2, Jul 6, 2012

* Inverse coercion methods (as.mcmc.list) failed with nvar=1 cases,
  it is now fixed.

## Version 0.2-1, May 13, 2012

* Depends: R (>= 2.15.0). Old versions of R failed under MacOS
  and Windows (reported by Uwe Ligges).

## Version 0.2-0, Apr 27, 2012

* Complete rework of the package internals, no user visible
  changes (except for coda type methods are now available
  without extra as.mcmc.list coercion, including plots).
* dcmle class replaces dcMle, new classes and methods added.

## Version 0.1-6, Mar 22, 2012

* dcmle: cl=1 is now acceptable (defaults to NULL).
  Note that this behaviour is different from that is in dclone.

## Version 0.1-5, Feb 25, 2012

* S4 methods compliance for R 2.15.0:
  importFrom(stats4, coef, confint, summary, vcov)
  added to namespace (reported by B Ripley).

## Version 0.1-4, Jan 31, 2012

* sourceDcExample: topic is coerced to character.
* Documentation updated.
* NAMESPACE updated to export all classes,
  and import new functions from dclone.
* S4 summary method is now imported from stats4 and not
  redefined again.

## Version 0.1-3, Jan 25, 2012

* Preparing for new release.
* Define S4 generic for 'summary'.

## Version 0.1-2, Oct 18, 2011

* params slot can be list (to follow new dclone options).
* show/summary method for dcMle class got headings:
  Settings, Coefficients, Convergence.
* dcmle failed with initsfun when length(n.clones)==1
  and n.clones>1: now fixed.
* dcmle checks for getOption("mc.cores") and uses it
  when cl=NULL and mc.cores > 1. This allows
  forking to happen automatically via the global option.

## Version 0.1-1, Sep 29, 2011

* dcExample, sourceDcExample, listDcExample: new
  functions added to deal with examples from R-Forge.

## Version 0.1-0, Sep 27, 2011

* main functions, classes, methods work
* dependencies and namespace figured out
* documentation is ready
