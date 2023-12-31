Simple document
================

``` r
litters_df =
  read_csv("data/FAS_litters.csv")
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

pups_df =
  read.csv("data/FAS_pups.csv")
pups_df = janitor::clean_names(pups_df)
```

## `select`

`select` is used to select columns! (Note: If you does not use
`litters_df = select(...)`, the changes will not be saved.)

``` r
select(litters_df, group, litter_number, gd0_weight)
```

    ## # A tibble: 49 × 3
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
    ## # ℹ 39 more rows

``` r
select(litters_df, gd0_weight, litter_number)
```

    ## # A tibble: 49 × 2
    ##    gd0_weight litter_number  
    ##         <dbl> <chr>          
    ##  1       19.7 #85            
    ##  2       27   #1/2/95/2      
    ##  3       26   #5/5/3/83/3-3  
    ##  4       28.5 #5/4/2/95/2    
    ##  5       NA   #4/2/95/3-3    
    ##  6       NA   #2/2/95/3-2    
    ##  7       NA   #1/5/3/83/3-3/2
    ##  8       NA   #3/83/3-3      
    ##  9       NA   #2/95/3        
    ## 10       28.5 #3/5/2/2/95    
    ## # ℹ 39 more rows

``` r
select(litters_df, group, gd0_weight:gd_of_birth)
```

    ## # A tibble: 49 × 4
    ##    group gd0_weight gd18_weight gd_of_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>
    ##  1 Con7        19.7        34.7          20
    ##  2 Con7        27          42            19
    ##  3 Con7        26          41.4          19
    ##  4 Con7        28.5        44.1          19
    ##  5 Con7        NA          NA            20
    ##  6 Con7        NA          NA            20
    ##  7 Con7        NA          NA            20
    ##  8 Con8        NA          NA            20
    ##  9 Con8        NA          NA            20
    ## 10 Con8        28.5        NA            20
    ## # ℹ 39 more rows

``` r
select(litters_df, group, starts_with("pups")) 
```

    ## # A tibble: 49 × 4
    ##    group pups_born_alive pups_dead_birth pups_survive
    ##    <chr>           <dbl>           <dbl>        <dbl>
    ##  1 Con7                3               4            3
    ##  2 Con7                8               0            7
    ##  3 Con7                6               0            5
    ##  4 Con7                5               1            4
    ##  5 Con7                6               0            6
    ##  6 Con7                6               0            4
    ##  7 Con7                9               0            9
    ##  8 Con8                9               1            8
    ##  9 Con8                8               0            8
    ## 10 Con8                8               0            8
    ## # ℹ 39 more rows

``` r
#select every column with name that starts with "pups"

select(litters_df, -litter_number) 
```

    ## # A tibble: 49 × 7
    ##    group gd0_weight gd18_weight gd_of_birth pups_born_alive pups_dead_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>           <dbl>           <dbl>
    ##  1 Con7        19.7        34.7          20               3               4
    ##  2 Con7        27          42            19               8               0
    ##  3 Con7        26          41.4          19               6               0
    ##  4 Con7        28.5        44.1          19               5               1
    ##  5 Con7        NA          NA            20               6               0
    ##  6 Con7        NA          NA            20               6               0
    ##  7 Con7        NA          NA            20               9               0
    ##  8 Con8        NA          NA            20               9               1
    ##  9 Con8        NA          NA            20               8               0
    ## 10 Con8        28.5        NA            20               8               0
    ## # ℹ 39 more rows
    ## # ℹ 1 more variable: pups_survive <dbl>

``` r
# remove "litter_number", keep everything eles

select(litters_df, -starts_with("gd")) 
```

    ## # A tibble: 49 × 5
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
    ## # ℹ 39 more rows

``` r
select(litters_df, group, litter_id = litter_number) 
```

    ## # A tibble: 49 × 2
    ##    group litter_id      
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
    ## # ℹ 39 more rows

``` r
# rename "litter_number" to "litter_id"

select(litters_df, group, litter_id = litter_number, everything())
```

    ## # A tibble: 49 × 8
    ##    group litter_id       gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# keep everything else I didn't mention as they were

select(litters_df, gd0_weight, everything()) 
```

    ## # A tibble: 49 × 8
    ##    gd0_weight group litter_number   gd18_weight gd_of_birth pups_born_alive
    ##         <dbl> <chr> <chr>                 <dbl>       <dbl>           <dbl>
    ##  1       19.7 Con7  #85                    34.7          20               3
    ##  2       27   Con7  #1/2/95/2              42            19               8
    ##  3       26   Con7  #5/5/3/83/3-3          41.4          19               6
    ##  4       28.5 Con7  #5/4/2/95/2            44.1          19               5
    ##  5       NA   Con7  #4/2/95/3-3            NA            20               6
    ##  6       NA   Con7  #2/2/95/3-2            NA            20               6
    ##  7       NA   Con7  #1/5/3/83/3-3/2        NA            20               9
    ##  8       NA   Con8  #3/83/3-3              NA            20               9
    ##  9       NA   Con8  #2/95/3                NA            20               8
    ## 10       28.5 Con8  #3/5/2/2/95            NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
rename(litters_df, litter_id = litter_number)
```

    ## # A tibble: 49 × 8
    ##    group litter_id       gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
relocate(litters_df, litter_number)
```

    ## # A tibble: 49 × 8
    ##    litter_number   group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>           <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85             Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2       Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3   Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2     Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3     Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2     Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2 Con7        NA          NA            20               9
    ##  8 #3/83/3-3       Con8        NA          NA            20               9
    ##  9 #2/95/3         Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95     Con8        28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# start with "litter_number" first
```

# Learning Assessment: In the pups data, select the columns containing litter number, sex, and PD ears

``` r
select(pups_df, litter_number, sex, pd_ears)
```

    ##       litter_number sex pd_ears
    ## 1               #85   1       4
    ## 2               #85   1       4
    ## 3         #1/2/95/2   1       5
    ## 4         #1/2/95/2   1       5
    ## 5     #5/5/3/83/3-3   1       5
    ## 6     #5/5/3/83/3-3   1       5
    ## 7       #5/4/2/95/2   1      NA
    ## 8       #4/2/95/3-3   1       4
    ## 9       #4/2/95/3-3   1       4
    ## 10      #2/2/95/3-2   1       4
    ## 11  #1/5/3/83/3-3/2   1       4
    ## 12  #1/5/3/83/3-3/2   1       4
    ## 13  #1/5/3/83/3-3/2   1       4
    ## 14  #1/5/3/83/3-3/2   1       4
    ## 15  #1/5/3/83/3-3/2   1       4
    ## 16              #85   2       4
    ## 17        #1/2/95/2   2       4
    ## 18        #1/2/95/2   2       4
    ## 19        #1/2/95/2   2       5
    ## 20        #1/2/95/2   2       5
    ## 21        #1/2/95/2   2       5
    ## 22    #5/5/3/83/3-3   2       5
    ## 23    #5/5/3/83/3-3   2       5
    ## 24    #5/5/3/83/3-3   2       5
    ## 25      #5/4/2/95/2   2      NA
    ## 26      #5/4/2/95/2   2      NA
    ## 27      #5/4/2/95/2   2      NA
    ## 28      #4/2/95/3-3   2       4
    ## 29      #4/2/95/3-3   2       4
    ## 30      #4/2/95/3-3   2       4
    ## 31      #4/2/95/3-3   2       4
    ## 32      #2/2/95/3-2   2       4
    ## 33      #2/2/95/3-2   2       4
    ## 34      #2/2/95/3-2   2       4
    ## 35  #1/5/3/83/3-3/2   2       4
    ## 36  #1/5/3/83/3-3/2   2       4
    ## 37  #1/5/3/83/3-3/2   2       4
    ## 38  #1/5/3/83/3-3/2   2       4
    ## 39        #3/83/3-3   1       3
    ## 40        #3/83/3-3   1       3
    ## 41        #3/83/3-3   1       3
    ## 42        #3/83/3-3   1       3
    ## 43        #3/83/3-3   1       4
    ## 44          #2/95/3   1       4
    ## 45          #2/95/3   1       3
    ## 46          #2/95/3   1       3
    ## 47          #2/95/3   1       3
    ## 48      #3/5/2/2/95   1       4
    ## 49      #3/5/2/2/95   1       4
    ## 50      #3/5/2/2/95   1       4
    ## 51      #3/5/2/2/95   1       4
    ## 52      #5/4/3/83/3   1       4
    ## 53      #5/4/3/83/3   1       4
    ## 54      #5/4/3/83/3   1       4
    ## 55      #5/4/3/83/3   1       4
    ## 56      #5/4/3/83/3   1       4
    ## 57    #1/6/2/2/95-2   1       3
    ## 58    #1/6/2/2/95-2   1       4
    ## 59  #3/5/3/83/3-3-2   1       4
    ## 60  #3/5/3/83/3-3-2   1       4
    ## 61  #3/5/3/83/3-3-2   1       4
    ## 62  #3/5/3/83/3-3-2   1       4
    ## 63        #2/2/95/2   1       5
    ## 64        #2/2/95/2   1       4
    ## 65    #3/6/2/2/95-3   1       3
    ## 66    #3/6/2/2/95-3   1       3
    ## 67    #3/6/2/2/95-3   1       3
    ## 68    #3/6/2/2/95-3   1       3
    ## 69    #3/6/2/2/95-3   1       3
    ## 70        #3/83/3-3   2       3
    ## 71        #3/83/3-3   2       3
    ## 72        #3/83/3-3   2       3
    ## 73          #2/95/3   2       3
    ## 74          #2/95/3   2       3
    ## 75          #2/95/3   2       4
    ## 76          #2/95/3   2       3
    ## 77      #3/5/2/2/95   2       4
    ## 78      #3/5/2/2/95   2       4
    ## 79      #3/5/2/2/95   2       3
    ## 80      #3/5/2/2/95   2       4
    ## 81      #5/4/3/83/3   2       4
    ## 82      #5/4/3/83/3   2       4
    ## 83      #5/4/3/83/3   2       4
    ## 84    #1/6/2/2/95-2   2       3
    ## 85    #1/6/2/2/95-2   2       3
    ## 86    #1/6/2/2/95-2   2       4
    ## 87    #1/6/2/2/95-2   2       4
    ## 88  #3/5/3/83/3-3-2   2       4
    ## 89  #3/5/3/83/3-3-2   2       4
    ## 90  #3/5/3/83/3-3-2   2       4
    ## 91  #3/5/3/83/3-3-2   2       4
    ## 92        #2/2/95/2   2       4
    ## 93        #2/2/95/2   2       4
    ## 94    #3/6/2/2/95-3   2       3
    ## 95    #3/6/2/2/95-3   2       3
    ## 96            #84/2   1       3
    ## 97            #84/2   1       3
    ## 98            #84/2   1       3
    ## 99             #107   1       4
    ## 100            #107   1       4
    ## 101            #107   1       4
    ## 102            #107   1       4
    ## 103            #107   1       4
    ## 104            #107   1       4
    ## 105            #107   1       4
    ## 106           #85/2   1       4
    ## 107           #85/2   1       4
    ## 108             #98   1       3
    ## 109             #98   1       4
    ## 110             #98   1       4
    ## 111             #98   1       4
    ## 112             #98   1       3
    ## 113            #102   1       4
    ## 114            #102   1       4
    ## 115            #101   1       3
    ## 116            #101   1       3
    ## 117            #101   1       4
    ## 118            #101   1       4
    ## 119            #111   1       4
    ## 120           #84/2   2       3
    ## 121           #84/2   2       3
    ## 122           #84/2   2       3
    ## 123           #84/2   2       3
    ## 124           #84/2   2       3
    ## 125            #107   2       4
    ## 126           #85/2   2       4
    ## 127           #85/2   2       4
    ## 128           #85/2   2       4
    ## 129           #85/2   2       4
    ## 130             #98   2       2
    ## 131             #98   2       4
    ## 132             #98   2       4
    ## 133             #98   2       3
    ## 134            #102   2       4
    ## 135            #102   2       3
    ## 136            #102   2       3
    ## 137            #102   2       4
    ## 138            #102   2       3
    ## 139            #101   2       3
    ## 140            #101   2       3
    ## 141            #101   2       3
    ## 142            #101   2       4
    ## 143            #101   2       4
    ## 144            #111   2       4
    ## 145            #111   2       4
    ## 146             #59   1       4
    ## 147             #59   1       4
    ## 148             #59   1       4
    ## 149            #103   1       4
    ## 150            #103   1       4
    ## 151            #103   1       3
    ## 152       #1/82/3-2   1       4
    ## 153       #1/82/3-2   1       4
    ## 154       #3/83/3-2   1       4
    ## 155       #3/83/3-2   1       4
    ## 156       #3/83/3-2   1       4
    ## 157       #3/83/3-2   1       4
    ## 158       #3/83/3-2   1       4
    ## 159       #3/83/3-2   1       4
    ## 160       #2/95/2-2   1       4
    ## 161       #2/95/2-2   1       4
    ## 162       #2/95/2-2   1       4
    ## 163       #2/95/2-2   1       4
    ## 164       #3/82/3-2   1       3
    ## 165       #3/82/3-2   1       4
    ## 166       #4/2/95/2   1       4
    ## 167       #4/2/95/2   1       4
    ## 168       #4/2/95/2   1       4
    ## 169       #4/2/95/2   1       4
    ## 170     #5/3/83/5-2   1       4
    ## 171     #5/3/83/5-2   1       4
    ## 172     #5/3/83/5-2   1       4
    ## 173      #8/110/3-2   1       3
    ## 174      #8/110/3-2   1       3
    ## 175      #8/110/3-2   1       3
    ## 176      #8/110/3-2   1       4
    ## 177            #106   1       3
    ## 178           #94/2   1      NA
    ## 179             #62   1       5
    ## 180             #62   1       5
    ## 181             #62   1       5
    ## 182             #59   2       4
    ## 183             #59   2       4
    ## 184            #103   2       3
    ## 185            #103   2       3
    ## 186            #103   2       3
    ## 187            #103   2       3
    ## 188            #103   2       3
    ## 189            #103   2       4
    ## 190       #1/82/3-2   2       4
    ## 191       #1/82/3-2   2       4
    ## 192       #1/82/3-2   2       5
    ## 193       #1/82/3-2   2       4
    ## 194       #3/83/3-2   2       4
    ## 195       #3/83/3-2   2       4
    ## 196       #2/95/2-2   2       4
    ## 197       #2/95/2-2   2       4
    ## 198       #2/95/2-2   2       4
    ## 199       #3/82/3-2   2       4
    ## 200       #3/82/3-2   2       3
    ## 201       #3/82/3-2   2       3
    ## 202       #4/2/95/2   2       4
    ## 203       #4/2/95/2   2       4
    ## 204       #4/2/95/2   2       4
    ## 205     #5/3/83/3-2   2       3
    ## 206     #5/3/83/3-2   2       3
    ## 207      #8/110/3-2   2       3
    ## 208      #8/110/3-2   2       3
    ## 209      #8/110/3-2   2       4
    ## 210      #8/110/3-2   2       4
    ## 211      #8/110/3-2   2       4
    ## 212            #106   2       3
    ## 213           #94/2   2      NA
    ## 214           #94/2   2      NA
    ## 215             #62   2       5
    ## 216             #53   1       4
    ## 217             #53   1       3
    ## 218             #53   1       4
    ## 219             #53   1       3
    ## 220             #53   1       4
    ## 221             #79   1       4
    ## 222             #79   1       4
    ## 223             #79   1       4
    ## 224             #79   1       4
    ## 225             #79   1       4
    ## 226            #100   1       3
    ## 227            #100   1       3
    ## 228           #4/84   1       3
    ## 229           #4/84   1       3
    ## 230           #4/84   1       4
    ## 231            #108   1       3
    ## 232            #108   1       3
    ## 233            #108   1       3
    ## 234            #108   1       3
    ## 235             #99   1      NA
    ## 236             #99   1      NA
    ## 237             #99   1      NA
    ## 238             #99   1      NA
    ## 239            #110   1      NA
    ## 240             #53   2       3
    ## 241             #53   2       4
    ## 242             #79   2       4
    ## 243             #79   2       4
    ## 244            #100   2       4
    ## 245            #100   2       3
    ## 246            #100   2       3
    ## 247            #100   2       3
    ## 248            #100   2       4
    ## 249           #4/84   2       3
    ## 250            #108   2       3
    ## 251            #108   2       3
    ## 252            #108   2       3
    ## 253             #99   2      NA
    ## 254            #110   2      NA
    ## 255            #110   2      NA
    ## 256            #110   2      NA
    ## 257            #110   2      NA
    ## 258            #110   2      NA
    ## 259             #97   1       3
    ## 260             #97   1       3
    ## 261             #97   1       3
    ## 262             #97   1       3
    ## 263             #97   1       3
    ## 264             #97   1       3
    ## 265           #5/93   1       3
    ## 266           #5/93   1       3
    ## 267           #5/93   1       3
    ## 268         #5/93/2   1       4
    ## 269       #7/82/3-2   1       3
    ## 270       #7/82/3-2   1       4
    ## 271       #7/82/3-2   1       3
    ## 272      #7/110/3-2   1       3
    ## 273      #7/110/3-2   1       3
    ## 274      #7/110/3-2   1       4
    ## 275      #7/110/3-2   1       3
    ## 276      #7/110/3-2   1       3
    ## 277      #7/110/3-2   1       3
    ## 278         #2/95/2   1       4
    ## 279         #2/95/2   1       4
    ## 280         #2/95/2   1       4
    ## 281           #82/4   1       4
    ## 282           #82/4   1       3
    ## 283           #82/4   1       4
    ## 284             #97   2       3
    ## 285             #97   2       3
    ## 286           #5/93   2       4
    ## 287           #5/93   2       3
    ## 288           #5/93   2       4
    ## 289           #5/93   2       3
    ## 290           #5/93   2       3
    ## 291           #5/93   2       3
    ## 292         #5/93/2   2       4
    ## 293         #5/93/2   2       5
    ## 294         #5/93/2   2       4
    ## 295         #5/93/2   2       5
    ## 296         #5/93/2   2       4
    ## 297         #5/93/2   2       4
    ## 298         #5/93/2   2       5
    ## 299       #7/82/3-2   2       3
    ## 300       #7/82/3-2   2       3
    ## 301       #7/82/3-2   2       3
    ## 302       #7/82/3-2   2       3
    ## 303      #7/110/3-2   2       4
    ## 304      #7/110/3-2   2       4
    ## 305         #2/95/2   2       4
    ## 306         #2/95/2   2       4
    ## 307         #2/95/2   2       4
    ## 308         #2/95/2   2       4
    ## 309         #2/95/2   2       3
    ## 310         #2/95/2   2       3
    ## 311           #82/4   2       4
    ## 312           #82/4   2       3
    ## 313           #82/4   2       3

`select` vs `pull`

``` r
select(litters_df, group)
```

    ## # A tibble: 49 × 1
    ##    group
    ##    <chr>
    ##  1 Con7 
    ##  2 Con7 
    ##  3 Con7 
    ##  4 Con7 
    ##  5 Con7 
    ##  6 Con7 
    ##  7 Con7 
    ##  8 Con8 
    ##  9 Con8 
    ## 10 Con8 
    ## # ℹ 39 more rows

``` r
# result comes as column

pull(litters_df, group)
```

    ##  [1] "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con8" "Con8" "Con8"
    ## [11] "Con8" "Con8" "Con8" "Con8" "Con8" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7"
    ## [21] "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Low7" "Low7" "Low7"
    ## [31] "Low7" "Low7" "Low7" "Low7" "Low7" "Mod8" "Mod8" "Mod8" "Mod8" "Mod8"
    ## [41] "Mod8" "Mod8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8"

## `filter`

get rid of rows using `filter()`

``` r
filter(litters_df, group == "Con7")
```

    ## # A tibble: 7 × 8
    ##   group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                   19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2             27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3           NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2           NA          NA            20               6
    ## 7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# keeps the rows with group == "Con7"

filter(litters_df, group == "Mod8")
```

    ## # A tibble: 7 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Mod8  #97                 24.5        42.8          20               8
    ## 2 Mod8  #5/93               NA          41.1          20              11
    ## 3 Mod8  #5/93/2             NA          NA            19               8
    ## 4 Mod8  #7/82-3-2           26.9        43.2          20               7
    ## 5 Mod8  #7/110/3-2          27.5        46            19               8
    ## 6 Mod8  #2/95/2             28.5        44.5          20               9
    ## 7 Mod8  #82/4               33.4        52.7          20               8
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# keeps the rows with group == "Mod8"

filter(litters_df, group != "Con7")
```

    ## # A tibble: 42 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con8  #3/83/3-3             NA          NA            20               9
    ##  2 Con8  #2/95/3               NA          NA            20               8
    ##  3 Con8  #3/5/2/2/95           28.5        NA            20               8
    ##  4 Con8  #5/4/3/83/3           28          NA            19               9
    ##  5 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ##  6 Con8  #3/5/3/83/3-3-2       NA          NA            20               8
    ##  7 Con8  #2/2/95/2             NA          NA            19               5
    ##  8 Con8  #3/6/2/2/95-3         NA          NA            20               7
    ##  9 Mod7  #59                   17          33.4          19               8
    ## 10 Mod7  #103                  21.4        42.1          19               9
    ## # ℹ 32 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# keeps the rows with group that's not "Con7"

filter(litters_df, gd0_weight > 20)
```

    ## # A tibble: 30 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #1/2/95/2           27          42            19               8
    ##  2 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  3 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  4 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  5 Con8  #5/4/3/83/3         28          NA            19               9
    ##  6 Mod7  #103                21.4        42.1          19               9
    ##  7 Mod7  #3/82/3-2           28          45.9          20               5
    ##  8 Mod7  #4/2/95/2           23.5        NA            19               9
    ##  9 Mod7  #5/3/83/5-2         22.6        37            19               5
    ## 10 Mod7  #106                21.7        37.8          20               5
    ## # ℹ 20 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# keeps the rows with gd0_weight > 20

filter(litters_df, gd0_weight <= 20)
```

    ## # A tibble: 4 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Mod7  #59                 17          33.4          19               8
    ## 3 Mod7  #62                 19.5        35.9          19               7
    ## 4 Low8  #100                20          39.2          20               8
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, group == "Con7" | group == "Con8")
```

    ## # A tibble: 15 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## 11 Con8  #5/4/3/83/3           28          NA            19               9
    ## 12 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ## 13 Con8  #3/5/3/83/3-3-2       NA          NA            20               8
    ## 14 Con8  #2/2/95/2             NA          NA            19               5
    ## 15 Con8  #3/6/2/2/95-3         NA          NA            20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, group %in% c("Con7","Con8"))
```

    ## # A tibble: 15 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## 11 Con8  #5/4/3/83/3           28          NA            19               9
    ## 12 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ## 13 Con8  #3/5/3/83/3-3-2       NA          NA            20               8
    ## 14 Con8  #2/2/95/2             NA          NA            19               5
    ## 15 Con8  #3/6/2/2/95-3         NA          NA            20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# Both will keeps the rows with group == "Con7" or "Con8"

filter(litters_df, !(group == "Con7"))
```

    ## # A tibble: 42 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con8  #3/83/3-3             NA          NA            20               9
    ##  2 Con8  #2/95/3               NA          NA            20               8
    ##  3 Con8  #3/5/2/2/95           28.5        NA            20               8
    ##  4 Con8  #5/4/3/83/3           28          NA            19               9
    ##  5 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ##  6 Con8  #3/5/3/83/3-3-2       NA          NA            20               8
    ##  7 Con8  #2/2/95/2             NA          NA            19               5
    ##  8 Con8  #3/6/2/2/95-3         NA          NA            20               7
    ##  9 Mod7  #59                   17          33.4          19               8
    ## 10 Mod7  #103                  21.4        42.1          19               9
    ## # ℹ 32 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, group %in% c("Con7","Con8"), gd0_weight > 20)
```

    ## # A tibble: 5 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #1/2/95/2           27          42            19               8
    ## 2 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 3 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 4 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## 5 Con8  #5/4/3/83/3         28          NA            19               9
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

what about missing rows?

``` r
drop_na(litters_df)
```

    ## # A tibble: 31 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Mod7  #59                 17          33.4          19               8
    ##  6 Mod7  #103                21.4        42.1          19               9
    ##  7 Mod7  #3/82/3-2           28          45.9          20               5
    ##  8 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  9 Mod7  #106                21.7        37.8          20               5
    ## 10 Mod7  #94/2               24.4        42.9          19               7
    ## # ℹ 21 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# drop all the rows with any missing value

drop_na(litters_df, gd0_weight)
```

    ## # A tibble: 34 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  6 Con8  #5/4/3/83/3         28          NA            19               9
    ##  7 Mod7  #59                 17          33.4          19               8
    ##  8 Mod7  #103                21.4        42.1          19               9
    ##  9 Mod7  #3/82/3-2           28          45.9          20               5
    ## 10 Mod7  #4/2/95/2           23.5        NA            19               9
    ## # ℹ 24 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# drop the rows with missing value in "gd0_weight"
```

## `mutate`

this is used to add or change variables.

``` r
mutate(litters_df, wt_gain = gd18_weight - gd0_weight)
```

    ## # A tibble: 49 × 9
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 3 more variables: pups_dead_birth <dbl>, pups_survive <dbl>, wt_gain <dbl>

``` r
# calculate wt_gain = gd18_weight - gd0_weight, and add "wt_gain" as the last column

mutate(litters_df, group = str_to_lower(group))
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 con7  #85                   19.7        34.7          20               3
    ##  2 con7  #1/2/95/2             27          42            19               8
    ##  3 con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 con8  #3/83/3-3             NA          NA            20               9
    ##  9 con8  #2/95/3               NA          NA            20               8
    ## 10 con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# converts the values of "group" (string) to lower case letters

mutate(
  litters_df, 
  wt_gain = gd18_weight - gd0_weight,
  group = str_to_lower(group)
)
```

    ## # A tibble: 49 × 9
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 con7  #85                   19.7        34.7          20               3
    ##  2 con7  #1/2/95/2             27          42            19               8
    ##  3 con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 con8  #3/83/3-3             NA          NA            20               9
    ##  9 con8  #2/95/3               NA          NA            20               8
    ## 10 con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 3 more variables: pups_dead_birth <dbl>, pups_survive <dbl>, wt_gain <dbl>

## `arrange`

``` r
arrange(litters_df, gd0_weight)
```

    ## # A tibble: 49 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Mod7  #59                 17          33.4          19               8
    ##  2 Mod7  #62                 19.5        35.9          19               7
    ##  3 Con7  #85                 19.7        34.7          20               3
    ##  4 Low8  #100                20          39.2          20               8
    ##  5 Mod7  #103                21.4        42.1          19               9
    ##  6 Mod7  #106                21.7        37.8          20               5
    ##  7 Low8  #53                 21.8        37.2          20               8
    ##  8 Low8  #4/84               21.8        35.2          20               4
    ##  9 Low7  #85/2               22.2        38.5          20               8
    ## 10 Mod7  #5/3/83/5-2         22.6        37            19               5
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# arrange the rows according to their gd0_weight values

arrange(litters_df, group, gd0_weight)
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  3 Con7  #1/2/95/2             27          42            19               8
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #5/4/3/83/3           28          NA            19               9
    ##  9 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## 10 Con8  #3/83/3-3             NA          NA            20               9
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# arrange the rows first according to their group,
# then according to their gd0_weight values
```

## `pipes`

`|>` and `%>%` both exist

``` r
litters_df = 
  read_csv("data/FAS_litters.csv") |> 
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

``` r
# same as 
# litters_df = read_csv("data/FAS_litters.csv")
# litters_df = janitor::clean_names(litters_df)

litters_df = 
  read_csv("data/FAS_litters.csv") |> 
  janitor::clean_names() |>
  select(-starts_with("pups")) |> #remove the columns start with "pups"
  mutate(
    group = str_to_lower(group), 
    wt_gain = gd18_weight - gd0_weight,
    # calculate wt_gain = gd18_weight - gd0_weight, and add it as the last column
  ) |>
  drop_na(wt_gain) |>
  arrange(group, wt_gain)
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
