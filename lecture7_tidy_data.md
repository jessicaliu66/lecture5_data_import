Tidy data
================

## PULSE data

``` r
pulse_df =
  haven::read_sas("data/public_pulse_data.sas7bdat") |>
  janitor::clean_names() |>
  pivot_longer( #making a long format
    bdi_score_bl:bdi_score_12m, # the range of columns you want to pivot
    names_to = "visit", # change the columns' names to the values for a variable "visit"
    values_to = "bdi_score", # change the columns' values to the values of variable "bdi_score"
    names_prefix = "bdi_score_" # remove prename "bdi_score_" from all values
  ) |>
  mutate(
    visit = replace(visit, visit == "bl", "00m")
    # find the "visit" values that are "bl" and replace them with "00m"
  )
```

# Learning Assessment

In the litters data, the variables `gd0_weight` and `gd18_weight` give
the weight of the mother mouse on gestational days 0 and 18. Write a
data cleaning chain that retains only `litter_number` and these columns;
produces new variables `gd` and `weight`; and makes `gd` a numeric
variable taking values `0` and `18` (for the last part, you might want
to use `recode` …). Is this version “tidy”?

``` r
litters_df =
  read_csv("data/FAS_litters.csv") |> 
  janitor::clean_names() |>
  select(litter_number, gd0_weight, gd18_weight) |>
  pivot_longer(
    gd0_weight:gd18_weight,
    names_to = "gd",
    values_to = "weight",
    names_prefix = "gd"
  ) |>
  mutate(
    gd = case_match(
      gd,
      "0_weight" ~ 0, # anytime see a value "0_weight", replace it w/ 0
      "18_weight" ~ 18,
    )
    # gd = replace(gd, gd == "0_weight", 0)
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## LoTR

Import LoTR words data

``` r
fellowship_df = 
  readxl::read_excel("data/LotR_Words.xlsx", range = "B3:D6") |>
# "range" indicates the range of chart you want to work on by EXCEL style
  mutate(movie = "fellowship")

two_towers_df = 
  readxl::read_excel("data/LotR_Words.xlsx", range = "F3:H6") |>
  mutate(movie = "two towers")

return_of_the_king_df = 
  readxl::read_excel("data/LotR_Words.xlsx", range = "B3:D6") |>
  mutate(movie = "return of the king")

lotr_df =
  bind_rows(fellowship_df, two_towers_df, return_of_the_king_df) |>
  janitor::clean_names() |>
  pivot_longer(
    male:female,
    names_to = "gender",
    values_to = "word"
  ) |>
  relocate(movie) # move the "movie" column to the first column
```
