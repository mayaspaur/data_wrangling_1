Data Import
================
Maya Spaur
9/17/2019

# Load in a dataset

``` r
##reads in a dataset using absolute path or relative path (always use a relative path!)

litters_data = read_csv(file = "./data_import_examples/FAS_litters.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )

``` r
pups_data = read_csv(file = "./data_import_examples/FAS_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_double(),
    ##   `PD ears` = col_double(),
    ##   `PD eyes` = col_double(),
    ##   `PD pivot` = col_double(),
    ##   `PD walk` = col_double()
    ## )

``` r
litters_data
```

    ## # A tibble: 49 x 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <chr> <chr>                  <dbl>         <dbl>         <dbl>
    ##  1 Con7  #85                     19.7          34.7            20
    ##  2 Con7  #1/2/95/2               27            42              19
    ##  3 Con7  #5/5/3/83/3-3           26            41.4            19
    ##  4 Con7  #5/4/2/95/2             28.5          44.1            19
    ##  5 Con7  #4/2/95/3-3             NA            NA              20
    ##  6 Con7  #2/2/95/3-2             NA            NA              20
    ##  7 Con7  #1/5/3/83/3-3/2         NA            NA              20
    ##  8 Con8  #3/83/3-3               NA            NA              20
    ##  9 Con8  #2/95/3                 NA            NA              20
    ## 10 Con8  #3/5/2/2/95             28.5          NA              20
    ## # ... with 39 more rows, and 3 more variables: `Pups born alive` <dbl>,
    ## #   `Pups dead @ birth` <dbl>, `Pups survive` <dbl>

``` r
pups_data
```

    ## # A tibble: 313 x 6
    ##    `Litter Number`   Sex `PD ears` `PD eyes` `PD pivot` `PD walk`
    ##    <chr>           <dbl>     <dbl>     <dbl>      <dbl>     <dbl>
    ##  1 #85                 1         4        13          7        11
    ##  2 #85                 1         4        13          7        12
    ##  3 #1/2/95/2           1         5        13          7         9
    ##  4 #1/2/95/2           1         5        13          8        10
    ##  5 #5/5/3/83/3-3       1         5        13          8        10
    ##  6 #5/5/3/83/3-3       1         5        14          6         9
    ##  7 #5/4/2/95/2         1        NA        14          5         9
    ##  8 #4/2/95/3-3         1         4        13          6         8
    ##  9 #4/2/95/3-3         1         4        13          7         9
    ## 10 #2/2/95/3-2         1         4        NA          8        10
    ## # ... with 303 more rows

``` r
litters_data = janitor::clean_names(litters_data)

pups_data = janitor::clean_names(pups_data)
```

# Selecting

Select data frame, and then the columns you want.

``` r
select(litters_data, group, litter_number)
```

    ## # A tibble: 49 x 2
    ##    group litter_number  
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
    ## # ... with 39 more rows

``` r
select(litters_data, group, litter_number, gd0_weight)
```

    ## # A tibble: 49 x 3
    ##    group litter_number   gd0_weight
    ##    <chr> <chr>                <dbl>
    ##  1 Con7  #85                   19.7
    ##  2 Con7  #1/2/95/2             27  
    ##  3 Con7  #5/5/3/83/3-3         26  
    ##  4 Con7  #5/4/2/95/2           28.5
    ##  5 Con7  #4/2/95/3-3           NA  
    ##  6 Con7  #2/2/95/3-2           NA  
    ##  7 Con7  #1/5/3/83/3-3/2       NA  
    ##  8 Con8  #3/83/3-3             NA  
    ##  9 Con8  #2/95/3               NA  
    ## 10 Con8  #3/5/2/2/95           28.5
    ## # ... with 39 more rows

``` r
select(litters_data, group, litter_number, starts_with("pups"))
```

    ## # A tibble: 49 x 5
    ##    group litter_number   pups_born_alive pups_dead_birth pups_survive
    ##    <chr> <chr>                     <dbl>           <dbl>        <dbl>
    ##  1 Con7  #85                           3               4            3
    ##  2 Con7  #1/2/95/2                     8               0            7
    ##  3 Con7  #5/5/3/83/3-3                 6               0            5
    ##  4 Con7  #5/4/2/95/2                   5               1            4
    ##  5 Con7  #4/2/95/3-3                   6               0            6
    ##  6 Con7  #2/2/95/3-2                   6               0            4
    ##  7 Con7  #1/5/3/83/3-3/2               9               0            9
    ##  8 Con8  #3/83/3-3                     9               1            8
    ##  9 Con8  #2/95/3                       8               0            8
    ## 10 Con8  #3/5/2/2/95                   8               0            8
    ## # ... with 39 more rows

``` r
select(litters_data, litter_number, group, everything())
```

    ## # A tibble: 49 x 8
    ##    litter_number group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>         <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85           Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2     Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3 Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2   Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3   Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2   Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-~ Con7        NA          NA            20               9
    ##  8 #3/83/3-3     Con8        NA          NA            20               9
    ##  9 #2/95/3       Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95   Con8        28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
select(litters_data, -group)
```

    ## # A tibble: 49 x 7
    ##    litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85                 19.7        34.7          20               3
    ##  2 #1/2/95/2           27          42            19               8
    ##  3 #5/5/3/83/3-3       26          41.4          19               6
    ##  4 #5/4/2/95/2         28.5        44.1          19               5
    ##  5 #4/2/95/3-3         NA          NA            20               6
    ##  6 #2/2/95/3-2         NA          NA            20               6
    ##  7 #1/5/3/83/3-~       NA          NA            20               9
    ##  8 #3/83/3-3           NA          NA            20               9
    ##  9 #2/95/3             NA          NA            20               8
    ## 10 #3/5/2/2/95         28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
select(litters_data, litter_number, gd0_weight:pups_born_alive)
```

    ## # A tibble: 49 x 5
    ##    litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85                   19.7        34.7          20               3
    ##  2 #1/2/95/2             27          42            19               8
    ##  3 #5/5/3/83/3-3         26          41.4          19               6
    ##  4 #5/4/2/95/2           28.5        44.1          19               5
    ##  5 #4/2/95/3-3           NA          NA            20               6
    ##  6 #2/2/95/3-2           NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 #3/83/3-3             NA          NA            20               9
    ##  9 #2/95/3               NA          NA            20               8
    ## 10 #3/5/2/2/95           28.5        NA            20               8
    ## # ... with 39 more rows