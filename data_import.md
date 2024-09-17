Data Import
================

This document will show how to import data.

## Import the FAS Litters CSV

``` r
litters_df = read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df
```

    ## # A tibble: 49 × 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <chr> <chr>           <chr>        <chr>                 <dbl>
    ##  1 Con7  #85             19.7         34.7                     20
    ##  2 Con7  #1/2/95/2       27           42                       19
    ##  3 Con7  #5/5/3/83/3-3   26           41.4                     19
    ##  4 Con7  #5/4/2/95/2     28.5         44.1                     19
    ##  5 Con7  #4/2/95/3-3     <NA>         <NA>                     20
    ##  6 Con7  #2/2/95/3-2     <NA>         <NA>                     20
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>         <NA>                     20
    ##  8 Con8  #3/83/3-3       <NA>         <NA>                     20
    ##  9 Con8  #2/95/3         <NA>         <NA>                     20
    ## 10 Con8  #3/5/2/2/95     28.5         <NA>                     20
    ## # ℹ 39 more rows
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

## Look at the dataset

``` r
litters_df
```

    ## # A tibble: 49 × 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <chr> <chr>           <chr>        <chr>                 <dbl>
    ##  1 Con7  #85             19.7         34.7                     20
    ##  2 Con7  #1/2/95/2       27           42                       19
    ##  3 Con7  #5/5/3/83/3-3   26           41.4                     19
    ##  4 Con7  #5/4/2/95/2     28.5         44.1                     19
    ##  5 Con7  #4/2/95/3-3     <NA>         <NA>                     20
    ##  6 Con7  #2/2/95/3-2     <NA>         <NA>                     20
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>         <NA>                     20
    ##  8 Con8  #3/83/3-3       <NA>         <NA>                     20
    ##  9 Con8  #2/95/3         <NA>         <NA>                     20
    ## 10 Con8  #3/5/2/2/95     28.5         <NA>                     20
    ## # ℹ 39 more rows
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <chr> <chr>           <chr>        <chr>                 <dbl>
    ## 1 Con7  #85             19.7         34.7                     20
    ## 2 Con7  #1/2/95/2       27           42                       19
    ## 3 Con7  #5/5/3/83/3-3   26           41.4                     19
    ## 4 Con7  #5/4/2/95/2     28.5         44.1                     19
    ## 5 Con7  #4/2/95/3-3     <NA>         <NA>                     20
    ## 6 Con7  #2/2/95/3-2     <NA>         <NA>                     20
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

``` r
tail(litters_df, 10)
```

    ## # A tibble: 10 × 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <chr> <chr>           <chr>        <chr>                 <dbl>
    ##  1 Mod8  #7/110/3-2      27.5         46                       19
    ##  2 Mod8  #2/95/2         28.5         44.5                     20
    ##  3 Mod8  #82/4           33.4         52.7                     20
    ##  4 Low8  #53             21.8         37.2                     20
    ##  5 Low8  #79             25.4         43.8                     19
    ##  6 Low8  #100            20           39.2                     20
    ##  7 Low8  #4/84           21.8         35.2                     20
    ##  8 Low8  #108            25.6         47.5                     20
    ##  9 Low8  #99             23.5         39                       20
    ## 10 Low8  #110            25.5         42.7                     20
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

``` r
view(litters_df)
#want this to be False when using view bc when you knit it it gets confused
```
