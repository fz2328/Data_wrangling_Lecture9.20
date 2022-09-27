data_manipulation
================
2022-09-22

## Import Dataset

``` r
litters_df = read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)

pups_data = read_csv("data/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_data = janitor::clean_names(pups_data)
```

## Select

    ## # A tibble: 49 × 4
    ##    group litter_number   gd0_weight pups_born_alive
    ##    <chr> <chr>                <dbl>           <dbl>
    ##  1 Con7  #85                   19.7               3
    ##  2 Con7  #1/2/95/2             27                 8
    ##  3 Con7  #5/5/3/83/3-3         26                 6
    ##  4 Con7  #5/4/2/95/2           28.5               5
    ##  5 Con7  #4/2/95/3-3           NA                 6
    ##  6 Con7  #2/2/95/3-2           NA                 6
    ##  7 Con7  #1/5/3/83/3-3/2       NA                 9
    ##  8 Con8  #3/83/3-3             NA                 9
    ##  9 Con8  #2/95/3               NA                 8
    ## 10 Con8  #3/5/2/2/95           28.5               8
    ## # … with 39 more rows

    ## # A tibble: 49 × 5
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>
    ##  1 Con7  #85                   19.7        34.7          20
    ##  2 Con7  #1/2/95/2             27          42            19
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19
    ##  5 Con7  #4/2/95/3-3           NA          NA            20
    ##  6 Con7  #2/2/95/3-2           NA          NA            20
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20
    ##  8 Con8  #3/83/3-3             NA          NA            20
    ##  9 Con8  #2/95/3               NA          NA            20
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20
    ## # … with 39 more rows

    ## # A tibble: 49 × 6
    ##    litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive pups_dea…¹
    ##    <chr>                <dbl>       <dbl>       <dbl>           <dbl>      <dbl>
    ##  1 #85                   19.7        34.7          20               3          4
    ##  2 #1/2/95/2             27          42            19               8          0
    ##  3 #5/5/3/83/3-3         26          41.4          19               6          0
    ##  4 #5/4/2/95/2           28.5        44.1          19               5          1
    ##  5 #4/2/95/3-3           NA          NA            20               6          0
    ##  6 #2/2/95/3-2           NA          NA            20               6          0
    ##  7 #1/5/3/83/3-3/2       NA          NA            20               9          0
    ##  8 #3/83/3-3             NA          NA            20               9          1
    ##  9 #2/95/3               NA          NA            20               8          0
    ## 10 #3/5/2/2/95           28.5        NA            20               8          0
    ## # … with 39 more rows, and abbreviated variable name ¹​pups_dead_birth

# Rename Variables when select

``` r
select(litters_df, GROUP = group, LiTtEr_NuMbEr = litter_number)
```

    ## # A tibble: 49 × 2
    ##    GROUP LiTtEr_NuMbEr  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # … with 39 more rows

``` r
#rename as part of the selection process

rename(litters_df, GROUP = group, LiTtEr_NuMbEr = litter_number)
```

    ## # A tibble: 49 × 8
    ##    GROUP LiTtEr_NuMbEr   gd0_weight gd18_weight gd_of_…¹ pups_…² pups_…³ pups_…⁴
    ##    <chr> <chr>                <dbl>       <dbl>    <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 Con7  #85                   19.7        34.7       20       3       4       3
    ##  2 Con7  #1/2/95/2             27          42         19       8       0       7
    ##  3 Con7  #5/5/3/83/3-3         26          41.4       19       6       0       5
    ##  4 Con7  #5/4/2/95/2           28.5        44.1       19       5       1       4
    ##  5 Con7  #4/2/95/3-3           NA          NA         20       6       0       6
    ##  6 Con7  #2/2/95/3-2           NA          NA         20       6       0       4
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA         20       9       0       9
    ##  8 Con8  #3/83/3-3             NA          NA         20       9       1       8
    ##  9 Con8  #2/95/3               NA          NA         20       8       0       8
    ## 10 Con8  #3/5/2/2/95           28.5        NA         20       8       0       8
    ## # … with 39 more rows, and abbreviated variable names ¹​gd_of_birth,
    ## #   ²​pups_born_alive, ³​pups_dead_birth, ⁴​pups_survive

``` r
#rename without selecting
```

# select with functions

``` r
select(litters_df, starts_with("gd"))
```

    ## # A tibble: 49 × 3
    ##    gd0_weight gd18_weight gd_of_birth
    ##         <dbl>       <dbl>       <dbl>
    ##  1       19.7        34.7          20
    ##  2       27          42            19
    ##  3       26          41.4          19
    ##  4       28.5        44.1          19
    ##  5       NA          NA            20
    ##  6       NA          NA            20
    ##  7       NA          NA            20
    ##  8       NA          NA            20
    ##  9       NA          NA            20
    ## 10       28.5        NA            20
    ## # … with 39 more rows

``` r
select(litters_df, ends_with("ve"))
```

    ## # A tibble: 49 × 2
    ##    pups_born_alive pups_survive
    ##              <dbl>        <dbl>
    ##  1               3            3
    ##  2               8            7
    ##  3               6            5
    ##  4               5            4
    ##  5               6            6
    ##  6               6            4
    ##  7               9            9
    ##  8               9            8
    ##  9               8            8
    ## 10               8            8
    ## # … with 39 more rows

``` r
select(litters_df, litter_number, pups_survive, everything())
```

    ## # A tibble: 49 × 8
    ##    litter_number   pups_survive group gd0_weight gd18_…¹ gd_of…² pups_…³ pups_…⁴
    ##    <chr>                  <dbl> <chr>      <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 #85                        3 Con7        19.7    34.7      20       3       4
    ##  2 #1/2/95/2                  7 Con7        27      42        19       8       0
    ##  3 #5/5/3/83/3-3              5 Con7        26      41.4      19       6       0
    ##  4 #5/4/2/95/2                4 Con7        28.5    44.1      19       5       1
    ##  5 #4/2/95/3-3                6 Con7        NA      NA        20       6       0
    ##  6 #2/2/95/3-2                4 Con7        NA      NA        20       6       0
    ##  7 #1/5/3/83/3-3/2            9 Con7        NA      NA        20       9       0
    ##  8 #3/83/3-3                  8 Con8        NA      NA        20       9       1
    ##  9 #2/95/3                    8 Con8        NA      NA        20       8       0
    ## 10 #3/5/2/2/95                8 Con8        28.5    NA        20       8       0
    ## # … with 39 more rows, and abbreviated variable names ¹​gd18_weight,
    ## #   ²​gd_of_birth, ³​pups_born_alive, ⁴​pups_dead_birth

``` r
#this function put litter number and survive up at the front, and put everything else after. This function changes the order of the variables. 

relocate(litters_df, litter_number, pups_survive)
```

    ## # A tibble: 49 × 8
    ##    litter_number   pups_survive group gd0_weight gd18_…¹ gd_of…² pups_…³ pups_…⁴
    ##    <chr>                  <dbl> <chr>      <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 #85                        3 Con7        19.7    34.7      20       3       4
    ##  2 #1/2/95/2                  7 Con7        27      42        19       8       0
    ##  3 #5/5/3/83/3-3              5 Con7        26      41.4      19       6       0
    ##  4 #5/4/2/95/2                4 Con7        28.5    44.1      19       5       1
    ##  5 #4/2/95/3-3                6 Con7        NA      NA        20       6       0
    ##  6 #2/2/95/3-2                4 Con7        NA      NA        20       6       0
    ##  7 #1/5/3/83/3-3/2            9 Con7        NA      NA        20       9       0
    ##  8 #3/83/3-3                  8 Con8        NA      NA        20       9       1
    ##  9 #2/95/3                    8 Con8        NA      NA        20       8       0
    ## 10 #3/5/2/2/95                8 Con8        28.5    NA        20       8       0
    ## # … with 39 more rows, and abbreviated variable names ¹​gd18_weight,
    ## #   ²​gd_of_birth, ³​pups_born_alive, ⁴​pups_dead_birth

``` r
#This relocate function does the same reordering as the above. 
```

## `filter` select certain rows/ certain observatons.

some examples: `gd_of_birth == 20` `pups_born_alive >= 2`
`pups_survive != 4` `!(pups_survive == 4)`
`group %in% c("Con7", "Con8")` `group == "Con7" & gd_of_birth == 20`
`!((pups_survive == 4) & (gd_of_birth == 20))`

``` r
filter(litters_df, group == "Con7" & gd_of_birth == 20)
```

    ## # A tibble: 4 × 8
    ##   group litter_number   gd0_weight gd18_weight gd_of_b…¹ pups_…² pups_…³ pups_…⁴
    ##   <chr> <chr>                <dbl>       <dbl>     <dbl>   <dbl>   <dbl>   <dbl>
    ## 1 Con7  #85                   19.7        34.7        20       3       4       3
    ## 2 Con7  #4/2/95/3-3           NA          NA          20       6       0       6
    ## 3 Con7  #2/2/95/3-2           NA          NA          20       6       0       4
    ## 4 Con7  #1/5/3/83/3-3/2       NA          NA          20       9       0       9
    ## # … with abbreviated variable names ¹​gd_of_birth, ²​pups_born_alive,
    ## #   ³​pups_dead_birth, ⁴​pups_survive

`drop_na(litters_df)` will remove any row with a missing value
`drop_na(litters_df, wt_increase)` will remove rows for which
wt_increase is missing.

``` r
drop_na(litters_df)
```

    ## # A tibble: 31 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_bi…¹ pups_…² pups_…³ pups_…⁴
    ##    <chr> <chr>              <dbl>       <dbl>      <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 Con7  #85                 19.7        34.7         20       3       4       3
    ##  2 Con7  #1/2/95/2           27          42           19       8       0       7
    ##  3 Con7  #5/5/3/83/3-3       26          41.4         19       6       0       5
    ##  4 Con7  #5/4/2/95/2         28.5        44.1         19       5       1       4
    ##  5 Mod7  #59                 17          33.4         19       8       0       5
    ##  6 Mod7  #103                21.4        42.1         19       9       1       9
    ##  7 Mod7  #3/82/3-2           28          45.9         20       5       0       5
    ##  8 Mod7  #5/3/83/5-2         22.6        37           19       5       0       5
    ##  9 Mod7  #106                21.7        37.8         20       5       0       2
    ## 10 Mod7  #94/2               24.4        42.9         19       7       1       3
    ## # … with 21 more rows, and abbreviated variable names ¹​gd_of_birth,
    ## #   ²​pups_born_alive, ³​pups_dead_birth, ⁴​pups_survive

``` r
drop_na(litters_df, gd18_weight)
```

    ## # A tibble: 32 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_bi…¹ pups_…² pups_…³ pups_…⁴
    ##    <chr> <chr>              <dbl>       <dbl>      <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 Con7  #85                 19.7        34.7         20       3       4       3
    ##  2 Con7  #1/2/95/2           27          42           19       8       0       7
    ##  3 Con7  #5/5/3/83/3-3       26          41.4         19       6       0       5
    ##  4 Con7  #5/4/2/95/2         28.5        44.1         19       5       1       4
    ##  5 Mod7  #59                 17          33.4         19       8       0       5
    ##  6 Mod7  #103                21.4        42.1         19       9       1       9
    ##  7 Mod7  #3/82/3-2           28          45.9         20       5       0       5
    ##  8 Mod7  #5/3/83/5-2         22.6        37           19       5       0       5
    ##  9 Mod7  #106                21.7        37.8         20       5       0       2
    ## 10 Mod7  #94/2               24.4        42.9         19       7       1       3
    ## # … with 22 more rows, and abbreviated variable names ¹​gd_of_birth,
    ## #   ²​pups_born_alive, ³​pups_dead_birth, ⁴​pups_survive

## `mutate`

used when you want to create new variables, change current variabels.

``` r
mutate(litters_df,
  wt_gain = gd18_weight - gd0_weight,
  wt_gain_kg = wt_gain * 2.2, 
  group = str_to_lower(group)
)
```

    ## # A tibble: 49 × 10
    ##    group litte…¹ gd0_w…² gd18_…³ gd_of…⁴ pups_…⁵ pups_…⁶ pups_…⁷ wt_gain wt_ga…⁸
    ##    <chr> <chr>     <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 con7  #85        19.7    34.7      20       3       4       3    15      33  
    ##  2 con7  #1/2/9…    27      42        19       8       0       7    15      33  
    ##  3 con7  #5/5/3…    26      41.4      19       6       0       5    15.4    33.9
    ##  4 con7  #5/4/2…    28.5    44.1      19       5       1       4    15.6    34.3
    ##  5 con7  #4/2/9…    NA      NA        20       6       0       6    NA      NA  
    ##  6 con7  #2/2/9…    NA      NA        20       6       0       4    NA      NA  
    ##  7 con7  #1/5/3…    NA      NA        20       9       0       9    NA      NA  
    ##  8 con8  #3/83/…    NA      NA        20       9       1       8    NA      NA  
    ##  9 con8  #2/95/3    NA      NA        20       8       0       8    NA      NA  
    ## 10 con8  #3/5/2…    28.5    NA        20       8       0       8    NA      NA  
    ## # … with 39 more rows, and abbreviated variable names ¹​litter_number,
    ## #   ²​gd0_weight, ³​gd18_weight, ⁴​gd_of_birth, ⁵​pups_born_alive,
    ## #   ⁶​pups_dead_birth, ⁷​pups_survive, ⁸​wt_gain_kg

``` r
#str_to_lower: is changing the variable to lower case. 
```

\##`arrange` rearrange the rows in your data. eg. sort your rows by
weight, then it goes from lower weight to higher weight.

``` r
head(arrange(litters_df, group, pups_born_alive), 10)
```

    ## # A tibble: 10 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_…¹ pups_…² pups_…³ pups_…⁴
    ##    <chr> <chr>                <dbl>       <dbl>    <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 Con7  #85                   19.7        34.7       20       3       4       3
    ##  2 Con7  #5/4/2/95/2           28.5        44.1       19       5       1       4
    ##  3 Con7  #5/5/3/83/3-3         26          41.4       19       6       0       5
    ##  4 Con7  #4/2/95/3-3           NA          NA         20       6       0       6
    ##  5 Con7  #2/2/95/3-2           NA          NA         20       6       0       4
    ##  6 Con7  #1/2/95/2             27          42         19       8       0       7
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA         20       9       0       9
    ##  8 Con8  #2/2/95/2             NA          NA         19       5       0       4
    ##  9 Con8  #1/6/2/2/95-2         NA          NA         20       7       0       6
    ## 10 Con8  #3/6/2/2/95-3         NA          NA         20       7       0       7
    ## # … with abbreviated variable names ¹​gd_of_birth, ²​pups_born_alive,
    ## #   ³​pups_dead_birth, ⁴​pups_survive

## Piping ‘%\>%’

to do piping, we can create several intermediate datasets untill you get
to the final dataset.

``` r
litters_data_raw = read_csv("./data/FAS_litters.csv",
  col_types = "ccddiiii")
litters_data_clean_names = janitor::clean_names(litters_data_raw)
litters_data_selected_cols = select(litters_data_clean_names, -pups_survive)
litters_data_with_vars = 
  mutate(
    litters_data_selected_cols, 
    wt_gain = gd18_weight - gd0_weight,
    group = str_to_lower(group))
litters_data_with_vars_without_missing = 
  drop_na(litters_data_with_vars, wt_gain)
litters_data_with_vars_without_missing
```

    ## # A tibble: 31 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_bi…¹ pups_…² pups_…³ wt_gain
    ##    <chr> <chr>              <dbl>       <dbl>      <int>   <int>   <int>   <dbl>
    ##  1 con7  #85                 19.7        34.7         20       3       4    15  
    ##  2 con7  #1/2/95/2           27          42           19       8       0    15  
    ##  3 con7  #5/5/3/83/3-3       26          41.4         19       6       0    15.4
    ##  4 con7  #5/4/2/95/2         28.5        44.1         19       5       1    15.6
    ##  5 mod7  #59                 17          33.4         19       8       0    16.4
    ##  6 mod7  #103                21.4        42.1         19       9       1    20.7
    ##  7 mod7  #3/82/3-2           28          45.9         20       5       0    17.9
    ##  8 mod7  #5/3/83/5-2         22.6        37           19       5       0    14.4
    ##  9 mod7  #106                21.7        37.8         20       5       0    16.1
    ## 10 mod7  #94/2               24.4        42.9         19       7       1    18.5
    ## # … with 21 more rows, and abbreviated variable names ¹​gd_of_birth,
    ## #   ²​pups_born_alive, ³​pups_dead_birth

or, we could nest our functions: In this case, the first step is in the
middle of the code, then it reads from the middle to the outside.

``` r
litters_data_clean = 
  drop_na(
    mutate(
      select(
        janitor::clean_names(
          read_csv("./data/FAS_litters.csv", col_types = "ccddiiii")
          ), 
      -pups_survive
      ),
    wt_gain = gd18_weight - gd0_weight,
    group = str_to_lower(group)
    ),
  wt_gain
  )

litters_data_clean
```

    ## # A tibble: 31 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_bi…¹ pups_…² pups_…³ wt_gain
    ##    <chr> <chr>              <dbl>       <dbl>      <int>   <int>   <int>   <dbl>
    ##  1 con7  #85                 19.7        34.7         20       3       4    15  
    ##  2 con7  #1/2/95/2           27          42           19       8       0    15  
    ##  3 con7  #5/5/3/83/3-3       26          41.4         19       6       0    15.4
    ##  4 con7  #5/4/2/95/2         28.5        44.1         19       5       1    15.6
    ##  5 mod7  #59                 17          33.4         19       8       0    16.4
    ##  6 mod7  #103                21.4        42.1         19       9       1    20.7
    ##  7 mod7  #3/82/3-2           28          45.9         20       5       0    17.9
    ##  8 mod7  #5/3/83/5-2         22.6        37           19       5       0    14.4
    ##  9 mod7  #106                21.7        37.8         20       5       0    16.1
    ## 10 mod7  #94/2               24.4        42.9         19       7       1    18.5
    ## # … with 21 more rows, and abbreviated variable names ¹​gd_of_birth,
    ## #   ²​pups_born_alive, ³​pups_dead_birth

Instead, we are using the pipe operator `%>%` shortcut: “command +
shift + m”

``` r
litters_data = 
  read_csv("./data/FAS_litters.csv", col_types = "ccddiiii") %>%
  janitor::clean_names() %>%
  select(-pups_survive) %>%
  mutate(
    wt_gain = gd18_weight - gd0_weight,
    group = str_to_lower(group)) %>% 
  drop_na(wt_gain)

litters_data 
```

    ## # A tibble: 31 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_bi…¹ pups_…² pups_…³ wt_gain
    ##    <chr> <chr>              <dbl>       <dbl>      <int>   <int>   <int>   <dbl>
    ##  1 con7  #85                 19.7        34.7         20       3       4    15  
    ##  2 con7  #1/2/95/2           27          42           19       8       0    15  
    ##  3 con7  #5/5/3/83/3-3       26          41.4         19       6       0    15.4
    ##  4 con7  #5/4/2/95/2         28.5        44.1         19       5       1    15.6
    ##  5 mod7  #59                 17          33.4         19       8       0    16.4
    ##  6 mod7  #103                21.4        42.1         19       9       1    20.7
    ##  7 mod7  #3/82/3-2           28          45.9         20       5       0    17.9
    ##  8 mod7  #5/3/83/5-2         22.6        37           19       5       0    14.4
    ##  9 mod7  #106                21.7        37.8         20       5       0    16.1
    ## 10 mod7  #94/2               24.4        42.9         19       7       1    18.5
    ## # … with 21 more rows, and abbreviated variable names ¹​gd_of_birth,
    ## #   ²​pups_born_alive, ³​pups_dead_birth
