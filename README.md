
# simulatebayes

<!-- badges: start -->
<!-- badges: end -->

The goal of simulatebayes is to make simulated data and run bayesian regression on it. The functions should therefore be called in the right order. 

* First, you simulate participants with make_participants. You chose the number of intervention participants and the number of control. 

* Second, you create the intervention data with make_interventions. 

* Third, you run the regressions with run_regressions (Stan installation is needed). 

Finally, you can plot the samples from the posterior with plot_samples. If you make regression output for different priors, you can compare the estimate results for two different priors with compare_priors.

## Installation

You can install the development version of simulatebayes like so:

``` r
devtools::install_github("tessavoesenek/simulatebayes", build_vignettes = TRU
```

## Example

This is a basic example which shows you how to set an experiment:

``` r
library(simulatebayes)

participants <- make_participants()
intervention_output <- make_interventions()

prior1_reg_out <- run_regressions(intervention_output$interventions, prior_type = 1)
prior0_reg_out <- run_regressions(intervention_output$interventions, prior_type = 0)

samples_plot_prior1 <- plot_samples(prior1_reg_out$samples, Effect = intervention_output$Effect)
samples_plot_prior0 <- plot_samples(prior0_reg_out$samples, Effect = intervention_output$Effect)

compare_prior_plot <- compare_priors(prior1_reg_out$coefficients, prior0_reg_out$coefficients, intervention_output$Effect)
```

