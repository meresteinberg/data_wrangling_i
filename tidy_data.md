Tidy Data
================

This document will show how to tidy data.

## Pivot longer

``` r
pulse_df=
  read_sas("data/public_pulse_data.sas7bdat") |> 
  janitor::clean_names()
pulse_df
```

    ## # A tibble: 1,087 × 7
    ##       id   age sex    bdi_score_bl bdi_score_01m bdi_score_06m bdi_score_12m
    ##    <dbl> <dbl> <chr>         <dbl>         <dbl>         <dbl>         <dbl>
    ##  1 10003  48.0 male              7             1             2             0
    ##  2 10015  72.5 male              6            NA            NA            NA
    ##  3 10022  58.5 male             14             3             8            NA
    ##  4 10026  72.7 male             20             6            18            16
    ##  5 10035  60.4 male              4             0             1             2
    ##  6 10050  84.7 male              2            10            12             8
    ##  7 10078  31.3 male              4             0            NA            NA
    ##  8 10088  56.9 male              5            NA             0             2
    ##  9 10091  76.0 male              0             3             4             0
    ## 10 10092  74.2 female           10             2            11             6
    ## # ℹ 1,077 more rows

This needs to go from wide to long format (with pivot longer)

``` r
pulse_tidy_df=
  pulse_df |> 
  pivot_longer(
    cols = bdi_score_bl: bdi_score_12m,
    names_to = "visit",
    values_to = "bdi_score",
    names_prefix = "bdi_score_"
  ) |> 
  mutate(
    visit= replace(visit, visit == "bl", "00m")
  ) |> 
  relocate(id, visit)
pulse_tidy_df
```

    ## # A tibble: 4,348 × 5
    ##       id visit   age sex   bdi_score
    ##    <dbl> <chr> <dbl> <chr>     <dbl>
    ##  1 10003 00m    48.0 male          7
    ##  2 10003 01m    48.0 male          1
    ##  3 10003 06m    48.0 male          2
    ##  4 10003 12m    48.0 male          0
    ##  5 10015 00m    72.5 male          6
    ##  6 10015 01m    72.5 male         NA
    ##  7 10015 06m    72.5 male         NA
    ##  8 10015 12m    72.5 male         NA
    ##  9 10022 00m    58.5 male         14
    ## 10 10022 01m    58.5 male          3
    ## # ℹ 4,338 more rows

Do one more example

``` r
litters_df=
  read_csv("data/FAS_litters.csv", na = c("NA", ".", "")) |> 
  janitor::clean_names()
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

weight is spread across two diff columns, gd could be 0 and 18

``` r
litters_tidy_df=
  litters_df |> 
  pivot_longer(
    cols = gd0_weight:gd18_weight,
    names_to = "gd_time",
    values_to = "weight"
  ) |> 
  mutate(
    gd_time = case_match(
      gd_time,
      "gd0_weight" ~ 0,
      "gd18_weight" ~ 18
    ))
```

gd_time and weight become two new columns above (also could do this
without creating new tidy df and put all of this in one chunk with
litters_df). Case match requires you to list out all options when
replacing variable with something else

## Pivot Wider

Let’s make up an analysis result table.

``` r
analysis_df=
  tibble(
    group = c("treatment", "treatment", "control", "control"),
    time = c("pre", "post", "pre", "post"),
    mean = c(4, 10, 4.2, 5)
  )
```

Pivot wider for human readability.

``` r
analysis_df |> 
  pivot_wider(
    names_from = time,
    values_from = mean
  ) |> 
  knitr::kable()
```

| group     | pre | post |
|:----------|----:|-----:|
| treatment | 4.0 |   10 |
| control   | 4.2 |    5 |

making column names from “time” variable (pre and post will be new
columns) and values for those columns are mean variable kable makes it a
nice table to read when knitted

## Bind tables

``` r
fellowship_ring=
  read_excel("data/LotR_Words.xlsx", range = "B3:D6") |> 
  mutate(movie = "fellowship_ring")

two_towers=
  read_excel("data/LotR_Words.xlsx", range = "F3:H6") |> 
  mutate(movie = "two_towers")

return_king=
  read_excel("data/LotR_Words.xlsx", range = "J3:L6") |> 
  mutate(movie = "return_king")

lotr_df=
  bind_rows(fellowship_ring, two_towers, return_king) |> 
  janitor::clean_names() |> 
    pivot_longer(
      cols = female:male,
      names_to = "sex",
      values_to = "words"
    ) |> 
  relocate(movie) |> 
  mutate(race = str_to_lower(race))
```
