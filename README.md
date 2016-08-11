# graml
A grammar for machine learning in R

As a Data Scientist we have available to us a grammar for preparing data (Hadley Wickham's tidyr package in R), a grammar for data wrangling (Hadley's dplyr package), and a grammar for graphics (developed by Leland Wilkinson with a premier implementation in R by Hadley Wickham called ggplot2). What about a grammar for machne learning?

This is an experimental test of the concept and not yet a useful package.

To use:

~~~~
> install.packages("devtools")
> devtools::install_github("gjwgit/graml") 
~~~~

Then try it out

~~~~
library(graml)
library(rattle)
library(magrittr)
library(dplyr)
library(randomForest)

model <-
  weather %>%
  set_names(names(.) %>% normVarNames()) %>%
  select(-date, -location, -risk_mm) %>%
  train(formula(rain_tomrrow ~ .)) +
    data_partition(0.7, 0.3) +
    model_binary_classification(randomForest) %>%
    tune_sweep(mtry=seq(5, nvars, 1)) +
    evaluate_confusion() +
    evaluate_auc() +
    evaluate_risk_chart()
~~~~

This returns a model as a graml object. We can plot the AUC or risk chart by extracting the appropriate elements from the object.
