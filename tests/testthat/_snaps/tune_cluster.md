# tune model only - failure in formula is caught elegantly

    Code
      cars_res <- tune_cluster(helper_objects$kmeans_mod, ~z, resamples = data_folds,
      grid = cars_grid, control = tune::control_grid(extract = function(x) {
        1
      }, save_pred = TRUE))
    Message <simpleMessage>
      x Fold1: preprocessor 1/1: Error in `get_all_predictors()`:
      ! The following predi...
      x Fold2: preprocessor 1/1: Error in `get_all_predictors()`:
      ! The following predi...
    Warning <rlang_warning>
      All models failed. See the `.notes` column.

# argument order gives errors for recipes

    Code
      tune_cluster(helper_objects$rec_tune_1, helper_objects$kmeans_mod_no_tune,
      rsample::vfold_cv(mtcars, v = 2))
    Error <rlang_error>
      The first argument to [tune_cluster()] should be either a model or workflow.

# argument order gives errors for formula

    Code
      tune_cluster(mpg ~ ., helper_objects$kmeans_mod_no_tune, rsample::vfold_cv(
        mtcars, v = 2))
    Error <rlang_error>
      The first argument to [tune_cluster()] should be either a model or workflow.

# ellipses with tune_cluster

    Code
      tune_cluster(wflow, resamples = folds, grid = 3, something = "wrong")
    Warning <rlang_warning>
      The `...` are not used in this function but one or more objects were passed: 'something'
    Output
      # Tuning results
      # 10-fold cross-validation 
      # A tibble: 10 x 4
         splits         id     .metrics         .notes          
         <list>         <chr>  <list>           <list>          
       1 <split [28/4]> Fold01 <tibble [4 x 5]> <tibble [0 x 3]>
       2 <split [28/4]> Fold02 <tibble [4 x 5]> <tibble [0 x 3]>
       3 <split [29/3]> Fold03 <tibble [4 x 5]> <tibble [0 x 3]>
       4 <split [29/3]> Fold04 <tibble [4 x 5]> <tibble [0 x 3]>
       5 <split [29/3]> Fold05 <tibble [4 x 5]> <tibble [0 x 3]>
       6 <split [29/3]> Fold06 <tibble [4 x 5]> <tibble [0 x 3]>
       7 <split [29/3]> Fold07 <tibble [4 x 5]> <tibble [0 x 3]>
       8 <split [29/3]> Fold08 <tibble [4 x 5]> <tibble [0 x 3]>
       9 <split [29/3]> Fold09 <tibble [4 x 5]> <tibble [0 x 3]>
      10 <split [29/3]> Fold10 <tibble [4 x 5]> <tibble [0 x 3]>

# select_best() and show_best() works

    Code
      tmp <- tune::show_best(res)
    Warning <rlang_warning>
      No value of `metric` was given; metric 'tot_wss' will be used.

---

    Code
      tmp <- tune::select_best(res)
    Warning <rlang_warning>
      No value of `metric` was given; metric 'tot_wss' will be used.

