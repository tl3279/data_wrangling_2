data_wrangling_2
================
Tianqi Li
2024-10-16

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## 载入程序包：'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(httr)
library(p8105.datasets)
```

## Extracting tables

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"
drug_use_html = read_html(url)

drug_use_html |>
  html_table()
```

    ## [[1]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "12.90a"         "13.36"          "0.002"        "13.28b"          
    ##  3 "Northea… "13.88a"         "14.66"          "0.005"        "13.98"           
    ##  4 "Midwest" "12.40b"         "12.76"          "0.082"        "12.45"           
    ##  5 "South"   "11.24a"         "11.64"          "0.029"        "12.02"           
    ##  6 "West"    "15.27"          "15.62"          "0.262"        "15.53a"          
    ##  7 "Alabama" "9.98"           "9.60"           "0.426"        "9.90"            
    ##  8 "Alaska"  "19.60a"         "21.92"          "0.010"        "17.30"           
    ##  9 "Arizona" "13.69"          "13.12"          "0.364"        "15.12"           
    ## 10 "Arkansa… "11.37"          "11.59"          "0.678"        "12.79"           
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[2]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "7.96a"          "8.34"           "0.001"        "7.22"            
    ##  3 "Northea… "8.58a"          "9.28"           "0.001"        "7.68"            
    ##  4 "Midwest" "7.50a"          "7.92"           "0.009"        "6.64"            
    ##  5 "South"   "6.74a"          "7.02"           "0.044"        "6.31"            
    ##  6 "West"    "9.84"           "10.08"          "0.324"        "8.85"            
    ##  7 "Alabama" "5.57"           "5.35"           "0.510"        "4.98"            
    ##  8 "Alaska"  "11.85a"         "14.38"          "0.002"        "9.19"            
    ##  9 "Arizona" "8.80"           "8.51"           "0.570"        "8.30"            
    ## 10 "Arkansa… "6.70"           "7.17"           "0.240"        "6.22"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[3]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "1.91"           "1.95"           "0.276"        "5.60"            
    ##  3 "Northea… "2.01"           "2.04"           "0.634"        "5.85b"           
    ##  4 "Midwest" "1.95"           "1.96"           "0.854"        "5.31"            
    ##  5 "South"   "1.69"           "1.75"           "0.137"        "5.18"            
    ##  6 "West"    "2.20"           "2.21"           "0.868"        "6.37b"           
    ##  7 "Alabama" "1.42"           "1.49"           "0.383"        "4.46"            
    ##  8 "Alaska"  "3.01a"          "3.54"           "0.012"        "6.99"            
    ##  9 "Arizona" "2.16"           "2.15"           "0.934"        "6.58"            
    ## 10 "Arkansa… "1.82"           "1.84"           "0.794"        "5.78"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[4]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "1.66a"          "1.76"           "0.040"        "0.60"            
    ##  3 "Northea… "1.94a"          "2.18"           "0.012"        "0.60"            
    ##  4 "Midwest" "1.37"           "1.43"           "0.282"        "0.48"            
    ##  5 "South"   "1.45b"          "1.56"           "0.067"        "0.53"            
    ##  6 "West"    "2.03"           "2.05"           "0.816"        "0.82"            
    ##  7 "Alabama" "1.23"           "1.22"           "0.995"        "0.42"            
    ##  8 "Alaska"  "1.54a"          "2.00"           "0.010"        "0.51"            
    ##  9 "Arizona" "2.25"           "2.29"           "0.861"        "1.01"            
    ## 10 "Arkansa… "0.93"           "1.07"           "0.208"        "0.41"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[5]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "0.30"           "0.33"           "0.217"        "0.12"            
    ##  3 "Northea… "0.43a"          "0.54"           "0.007"        "0.13"            
    ##  4 "Midwest" "0.30"           "0.31"           "0.638"        "0.11"            
    ##  5 "South"   "0.27"           "0.26"           "0.444"        "0.12"            
    ##  6 "West"    "0.25"           "0.29"           "0.152"        "0.13"            
    ##  7 "Alabama" "0.22"           "0.27"           "0.171"        "0.10"            
    ##  8 "Alaska"  "0.70a"          "1.23"           "0.044"        "0.11"            
    ##  9 "Arizona" "0.32a"          "0.55"           "0.001"        "0.17"            
    ## 10 "Arkansa… "0.19"           "0.17"           "0.398"        "0.10"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[6]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "52.42"          "52.18"          "0.337"        "11.55a"          
    ##  3 "Northea… "57.80a"         "56.66"          "0.009"        "13.19"           
    ##  4 "Midwest" "55.14a"         "54.36"          "0.032"        "11.31a"          
    ##  5 "South"   "48.74"          "48.85"          "0.759"        "10.87a"          
    ##  6 "West"    "51.67"          "52.07"          "0.383"        "11.71a"          
    ##  7 "Alabama" "44.72"          "43.94"          "0.533"        "10.53a"          
    ##  8 "Alaska"  "54.02"          "54.98"          "0.444"        "9.22"            
    ##  9 "Arizona" "51.80"          "51.19"          "0.613"        "11.90b"          
    ## 10 "Arkansa… "42.45"          "41.81"          "0.588"        "9.90"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[7]]
    ## # A tibble: 57 × 4
    ##    State    Alcohol Use inPast M…¹ Alcohol Use inPast M…² Alcohol Use inPast M…³
    ##    <chr>    <chr>                  <chr>                  <chr>                 
    ##  1 "NOTE: … "NOTE: State and cens… "NOTE: State and cens… "NOTE: State and cens…
    ##  2 "Total … "22.76a"               "21.57"                "0.000"               
    ##  3 "Northe… "26.11"                "25.98"                "0.792"               
    ##  4 "Midwes… "23.73a"               "22.00"                "0.000"               
    ##  5 "South"  "20.68a"               "19.66"                "0.010"               
    ##  6 "West"   "22.73a"               "21.01"                "0.000"               
    ##  7 "Alabam… "19.25"                "18.19"                "0.305"               
    ##  8 "Alaska" "21.47b"               "23.91"                "0.058"               
    ##  9 "Arizon… "22.01a"               "19.25"                "0.009"               
    ## 10 "Arkans… "18.07"                "16.65"                "0.106"               
    ## # ℹ 47 more rows
    ## # ℹ abbreviated names: ¹​`Alcohol Use inPast Month(2013-2014)`,
    ## #   ²​`Alcohol Use inPast Month(2014-2015)`,
    ## #   ³​`Alcohol Use inPast Month(P Value)`
    ## 
    ## [[8]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "25.36a"         "24.56"          "0.000"        "7.42a"           
    ##  3 "Northea… "23.76"          "23.30"          "0.216"        "7.18a"           
    ##  4 "Midwest" "28.57a"         "27.39"          "0.000"        "8.58a"           
    ##  5 "South"   "26.91a"         "26.24"          "0.034"        "7.57a"           
    ##  6 "West"    "21.20a"         "20.29"          "0.015"        "6.31a"           
    ##  7 "Alabama" "31.62"          "30.46"          "0.295"        "8.43"            
    ##  8 "Alaska"  "29.30a"         "31.51"          "0.048"        "10.73"           
    ##  9 "Arizona" "22.14"          "22.51"          "0.678"        "6.81"            
    ## 10 "Arkansa… "35.57"          "34.05"          "0.188"        "10.89"           
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[9]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "21.05a"         "20.12"          "0.000"        "5.24a"           
    ##  3 "Northea… "19.69"          "19.13"          "0.101"        "5.10a"           
    ##  4 "Midwest" "23.84a"         "22.50"          "0.000"        "6.16a"           
    ##  5 "South"   "22.37a"         "21.41"          "0.001"        "5.22a"           
    ##  6 "West"    "17.43a"         "16.66"          "0.026"        "4.56a"           
    ##  7 "Alabama" "25.90"          "24.25"          "0.106"        "5.66"            
    ##  8 "Alaska"  "22.00a"         "24.64"          "0.008"        "6.15"            
    ##  9 "Arizona" "18.73"          "19.23"          "0.576"        "4.95"            
    ## 10 "Arkansa… "28.51"          "27.81"          "0.519"        "7.13"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[10]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "6.50a"          "6.14"           "0.001"        "2.76"            
    ##  3 "Northea… "6.64"           "6.39"           "0.193"        "2.88"            
    ##  4 "Midwest" "6.59a"          "6.25"           "0.033"        "2.70"            
    ##  5 "South"   "6.20a"          "5.76"           "0.003"        "2.65"            
    ##  6 "West"    "6.80"           "6.47"           "0.120"        "2.91"            
    ##  7 "Alabama" "5.76a"          "4.64"           "0.007"        "2.84b"           
    ##  8 "Alaska"  "6.72"           "7.43"           "0.153"        "2.12"            
    ##  9 "Arizona" "7.60b"          "6.66"           "0.062"        "3.37"            
    ## 10 "Arkansa… "5.23"           "4.88"           "0.347"        "2.63"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[11]]
    ## # A tibble: 57 × 16
    ##    State     `12+(2013-2014)` `12+(2014-2015)` `12+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "3.04"           "2.97"           "0.321"        "1.01"            
    ##  3 "Northea… "3.01"           "3.09"           "0.500"        "1.02"            
    ##  4 "Midwest" "3.06b"          "2.86"           "0.061"        "1.03"            
    ##  5 "South"   "2.92a"          "2.73"           "0.047"        "0.96"            
    ##  6 "West"    "3.25"           "3.37"           "0.409"        "1.05"            
    ##  7 "Alabama" "2.99a"          "2.34"           "0.026"        "0.98"            
    ##  8 "Alaska"  "3.21"           "3.67"           "0.200"        "0.77"            
    ##  9 "Arizona" "3.44"           "3.62"           "0.591"        "1.11"            
    ## 10 "Arkansa… "2.73"           "2.42"           "0.255"        "0.96"            
    ## # ℹ 47 more rows
    ## # ℹ 11 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>,
    ## #   `18+(2013-2014)` <chr>, `18+(2014-2015)` <chr>, `18+(P Value)` <chr>
    ## 
    ## [[12]]
    ## # A tibble: 57 × 10
    ##    State     `18+(2013-2014)` `18+(2014-2015)` `18+(P Value)` `18-25(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "4.15"           "4.05"           "0.325"        "4.52a"           
    ##  3 "Northea… "3.93"           "3.94"           "0.953"        "4.67a"           
    ##  4 "Midwest" "4.45"           "4.36"           "0.511"        "4.93a"           
    ##  5 "South"   "4.17"           "4.00"           "0.206"        "4.18a"           
    ##  6 "West"    "4.02"           "3.96"           "0.681"        "4.56b"           
    ##  7 "Alabama" "4.53"           "4.64"           "0.749"        "4.30"            
    ##  8 "Alaska"  "3.90"           "4.02"           "0.707"        "4.60a"           
    ##  9 "Arizona" "4.09"           "4.33"           "0.491"        "4.45"            
    ## 10 "Arkansa… "5.24"           "5.27"           "0.942"        "4.49"            
    ## # ℹ 47 more rows
    ## # ℹ 5 more variables: `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>
    ## 
    ## [[13]]
    ## # A tibble: 57 × 10
    ##    State     `18+(2013-2014)` `18+(2014-2015)` `18+(P Value)` `18-25(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "18.29"          "18.01"          "0.146"        "19.75a"          
    ##  3 "Northea… "17.87"          "17.76"          "0.735"        "20.80a"          
    ##  4 "Midwest" "18.61"          "18.34"          "0.356"        "20.45a"          
    ##  5 "South"   "18.01"          "17.82"          "0.519"        "18.22a"          
    ##  6 "West"    "18.79b"         "18.18"          "0.088"        "20.70a"          
    ##  7 "Alabama" "19.51"          "18.85"          "0.469"        "18.09"           
    ##  8 "Alaska"  "18.12"          "18.11"          "0.989"        "20.33a"          
    ##  9 "Arizona" "18.59"          "18.32"          "0.756"        "18.76"           
    ## 10 "Arkansa… "20.00"          "19.77"          "0.816"        "19.99"           
    ## # ℹ 47 more rows
    ## # ℹ 5 more variables: `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>
    ## 
    ## [[14]]
    ## # A tibble: 57 × 10
    ##    State     `18+(2013-2014)` `18+(2014-2015)` `18+(P Value)` `18-25(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "3.94"           "3.99"           "0.526"        "7.44a"           
    ##  3 "Northea… "3.81"           "3.93"           "0.407"        "7.60b"           
    ##  4 "Midwest" "4.11"           "4.14"           "0.791"        "7.83"            
    ##  5 "South"   "3.84"           "3.86"           "0.896"        "6.89a"           
    ##  6 "West"    "4.02"           "4.12"           "0.522"        "7.84"            
    ##  7 "Alabama" "3.98"           "4.02"           "0.885"        "7.31"            
    ##  8 "Alaska"  "4.21"           "4.68"           "0.237"        "8.30b"           
    ##  9 "Arizona" "4.23"           "4.34"           "0.775"        "7.04"            
    ## 10 "Arkansa… "4.58"           "4.41"           "0.682"        "6.67"            
    ## # ℹ 47 more rows
    ## # ℹ 5 more variables: `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>
    ## 
    ## [[15]]
    ## # A tibble: 57 × 13
    ##    State     `18+(2013-2014)` `18+(2014-2015)` `18+(P Value)` `12-17(2013-2014)`
    ##    <chr>     <chr>            <chr>            <chr>          <chr>             
    ##  1 "NOTE: S… "NOTE: State an… "NOTE: State an… "NOTE: State … "NOTE: State and …
    ##  2 "Total U… "6.63"           "6.64"           "0.915"        "11.01a"          
    ##  3 "Northea… "6.66"           "6.82"           "0.458"        "10.63a"          
    ##  4 "Midwest" "6.81"           "6.87"           "0.736"        "10.81a"          
    ##  5 "South"   "6.47"           "6.52"           "0.750"        "10.77a"          
    ##  6 "West"    "6.67"           "6.47"           "0.353"        "11.82a"          
    ##  7 "Alabama" "6.85"           "6.81"           "0.948"        "10.74"           
    ##  8 "Alaska"  "6.57"           "6.73"           "0.770"        "9.92a"           
    ##  9 "Arizona" "7.32"           "6.77"           "0.362"        "13.23"           
    ## 10 "Arkansa… "7.31"           "7.78"           "0.446"        "11.95"           
    ## # ℹ 47 more rows
    ## # ℹ 8 more variables: `12-17(2014-2015)` <chr>, `12-17(P Value)` <chr>,
    ## #   `18-25(2013-2014)` <chr>, `18-25(2014-2015)` <chr>, `18-25(P Value)` <chr>,
    ## #   `26+(2013-2014)` <chr>, `26+(2014-2015)` <chr>, `26+(P Value)` <chr>

Focus on the first table

``` r
table_marj = 
  drug_use_html |> 
  html_table() |> 
  first() |>
  slice(-1)
```

NYC cost of living

``` r
nyc_cost = 
  read_html("https://www.bestplaces.net/cost_of_living/city/new_york/new_york") |>
  html_table(header = TRUE) |>
  first()
nyc_cost
```

    ## # A tibble: 8 × 4
    ##   Categories       `New York` `New York` `United States`
    ##   <chr>            <chr>      <chr>      <chr>          
    ## 1 Overall          172.5      121.5      100.0          
    ## 2 Grocery          116.6      103.8      100            
    ## 3 Health           127.6      120.7      100.0          
    ## 4 Housing          224.3      127.9      100.0          
    ## 5 Median Home Cost $677,200   $413,600   $338,100       
    ## 6 Utilities        150.5      115.9      100            
    ## 7 Transportation   181.1      140.7      100.0          
    ## 8 Miscellaneous    136.4      121.8      100.0

# CSS Selectors

``` r
swm_html = 
  read_html("https://www.imdb.com/list/ls070150896/")
```

``` r
title_vec = 
  swm_html |>
  html_elements(".ipc-title-link-wrapper .ipc-title__text") |>
  html_text()

metascore_vec = 
  swm_html |>
  html_elements(".metacritic-score-box") |>
  html_text()

runtime_vec = 
  swm_html |>
  html_elements(".dli-title-metadata-item:nth-child(2)") |>
  html_text()

swm_df = 
  tibble(
    title = title_vec,
    score = metascore_vec,
    runtime = runtime_vec)

swm_df|>
  knitr::kable()
```

| title                                              | score | runtime |
|:---------------------------------------------------|:------|:--------|
| 1\. Star Wars: Episode I - The Phantom Menace      | 51    | 2h 16m  |
| 2\. Star Wars: Episode II - Attack of the Clones   | 54    | 2h 22m  |
| 3\. Star Wars: Episode III - Revenge of the Sith   | 68    | 2h 20m  |
| 4\. Star Wars: Episode IV - A New Hope             | 90    | 2h 1m   |
| 5\. Star Wars: Episode V - The Empire Strikes Back | 82    | 2h 4m   |
| 6\. Star Wars: Episode VI - Return of the Jedi     | 58    | 2h 11m  |
| 7\. Star Wars: Episode VII - The Force Awakens     | 80    | 2h 18m  |
| 8\. Star Wars: Episode VIII - The Last Jedi        | 84    | 2h 32m  |
| 9\. Star Wars: Episode IX - The Rise of Skywalker  | 53    | 2h 21m  |

``` r
url = "http://books.toscrape.com"

books_html = read_html(url)

books_titles = 
  books_html |>
  html_elements("h3") |>
  html_text2()

books_stars = 
  books_html |>
  html_elements(".star-rating") |>
  html_attr("class")

books_price = 
  books_html |>
  html_elements(".price_color") |>
  html_text()

books = tibble(
  title = books_titles,
  stars = books_stars,
  price = books_price
)

books |>
  knitr::kable()
```

| title                               | stars             | price  |
|:------------------------------------|:------------------|:-------|
| A Light in the …                    | star-rating Three | £51.77 |
| Tipping the Velvet                  | star-rating One   | £53.74 |
| Soumission                          | star-rating One   | £50.10 |
| Sharp Objects                       | star-rating Four  | £47.82 |
| Sapiens: A Brief History …          | star-rating Five  | £54.23 |
| The Requiem Red                     | star-rating One   | £22.65 |
| The Dirty Little Secrets …          | star-rating Four  | £33.34 |
| The Coming Woman: A …               | star-rating Three | £17.93 |
| The Boys in the …                   | star-rating Four  | £22.60 |
| The Black Maria                     | star-rating One   | £52.15 |
| Starving Hearts (Triangular Trade … | star-rating Two   | £13.99 |
| Shakespeare’s Sonnets               | star-rating Four  | £20.66 |
| Set Me Free                         | star-rating Five  | £17.46 |
| Scott Pilgrim’s Precious Little …   | star-rating Five  | £52.29 |
| Rip it Up and …                     | star-rating Five  | £35.02 |
| Our Band Could Be …                 | star-rating Three | £57.25 |
| Olio                                | star-rating One   | £23.88 |
| Mesaerion: The Best Science …       | star-rating One   | £37.59 |
| Libertarianism for Beginners        | star-rating Two   | £51.33 |
| It’s Only the Himalayas             | star-rating Two   | £45.17 |

## API

``` r
nyc_water = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.json") |> 
  content("text") |>
  jsonlite::fromJSON() |>
  as_tibble()
```

``` r
brfss_smart2010 = 
  GET("https://chronicdata.cdc.gov/resource/acme-vg9e.csv",
      query = list("$limit" = 5000)) |> 
  content("parsed")
```

    ## Rows: 5000 Columns: 23
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (16): locationabbr, locationdesc, class, topic, question, response, data...
    ## dbl  (6): year, sample_size, data_value, confidence_limit_low, confidence_li...
    ## lgl  (1): locationid
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
poke = 
  GET("http://pokeapi.co/api/v2/pokemon/1") |>
  content()
```

Need to distil the data

## Strings and regex

``` r
string_vec = c("my", "name", "is", "jeff")

str_detect(string_vec, "jeff")
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
str_replace(string_vec, "jeff", "Jeff")
```

    ## [1] "my"   "name" "is"   "Jeff"

^\* for beginning \*\$ for end

``` r
string_vec = c(
  "i think we all rule for participating",
  "i think i have been caught",
  "i think this will be quite fun actually",
  "it will be fun, i think"
  )

str_detect(string_vec, "^i think")
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
str_detect(string_vec, "i think$")
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
string_vec = c(
  "Time for a Pumpkin Spice Latte!",
  "went to the #pumpkinpatch last weekend",
  "Pumpkin Pie is obviously the best pie",
  "SMASHING PUMPKINS -- LIVE IN CONCERT!!"
  )

str_detect(string_vec,"[Pp]umpkin")
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
string_vec = c(
  '7th inning stretch',
  '1st half soon to begin. Texas won the toss.',
  'she is 5 feet 4 inches tall',
  '3AM - cant sleep :('
  )

str_detect(string_vec, "^[0-9][a-zA-Z]")
```

    ## [1]  TRUE  TRUE FALSE  TRUE

. matches with everything

``` r
string_vec = c(
  'Its 7:11 in the evening',
  'want to go to 7-11?',
  'my flight is AA711',
  'NetBios: scanning ip 203.167.114.66'
  )

str_detect(string_vec, "7.11")
```

    ## [1]  TRUE  TRUE FALSE  TRUE

Need to specify []().using double  

``` r
string_vec = c(
  'The CI is [2, 5]',
  ':-]',
  ':-[',
  'I found the answer on pages [6-7]'
  )

str_detect(string_vec, "\\[")
```

    ## [1]  TRUE FALSE  TRUE  TRUE

## Factors

``` r
vec_sex = factor(c("male", "male", "female", "female"))
vec_sex
```

    ## [1] male   male   female female
    ## Levels: female male

``` r
as.numeric(vec_sex)
```

    ## [1] 2 2 1 1

``` r
vec_sex = fct_relevel(vec_sex, "male")
vec_sex
```

    ## [1] male   male   female female
    ## Levels: male female

``` r
as.numeric(vec_sex)
```

    ## [1] 1 1 2 2

## NSDUH

``` r
data_marj = 
  table_marj |>
  select(-contains("P Value")) |>
  pivot_longer(
    -State,
    names_to = "age_year", 
    values_to = "percent") |>
  separate(age_year, into = c("age", "year"), sep = "\\(") |>
  mutate(
    year = str_replace(year, "\\)", ""),
    percent = str_replace(percent, "[a-c]$", ""),
    percent = as.numeric(percent)) |>
  filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))
```

``` r
data_marj |>
  filter(age == "12-17") |> 
  mutate(State = fct_reorder(State, percent)) |> 
  ggplot(aes(x = State, y = percent, color = year)) + 
    geom_point() + 
    theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

![](data_wrangling_2_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

## Different datasets

Restaurant inspections

``` r
data("rest_inspec")

rest_inspec |> 
  group_by(boro, grade) |> 
  summarize(n = n()) |> 
  pivot_wider(names_from = grade, values_from = n)
```

    ## `summarise()` has grouped output by 'boro'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 6 × 8
    ## # Groups:   boro [6]
    ##   boro              A     B     C `Not Yet Graded`     P     Z  `NA`
    ##   <chr>         <int> <int> <int>            <int> <int> <int> <int>
    ## 1 BRONX         13688  2801   701              200   163   351 16833
    ## 2 BROOKLYN      37449  6651  1684              702   416   977 51930
    ## 3 MANHATTAN     61608 10532  2689              765   508  1237 80615
    ## 4 Missing           4    NA    NA               NA    NA    NA    13
    ## 5 QUEENS        35952  6492  1593              604   331   913 45816
    ## 6 STATEN ISLAND  5215   933   207               85    47   149  6730

``` r
rest_inspec =
  rest_inspec |>
  filter(grade %in% c("A", "B", "C"), boro != "Missing") |> 
  mutate(boro = str_to_title(boro))

rest_inspec |> 
  filter(str_detect(dba, "[Pp][Ii][Zz][Zz][Aa]")) |> 
  group_by(boro, grade) |> 
  summarize(n = n()) |> 
  pivot_wider(names_from = grade, values_from = n)
```

    ## `summarise()` has grouped output by 'boro'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 5 × 4
    ## # Groups:   boro [5]
    ##   boro              A     B     C
    ##   <chr>         <int> <int> <int>
    ## 1 Bronx          1170   305    56
    ## 2 Brooklyn       1948   296    61
    ## 3 Manhattan      1983   420    76
    ## 4 Queens         1647   259    48
    ## 5 Staten Island   323   127    21

``` r
rest_inspec |> 
  filter(str_detect(dba, "[Pp][Ii][Zz][Zz][Aa]")) |>
  ggplot(aes(x = boro, fill = grade)) + 
  geom_bar() 
```

![](data_wrangling_2_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

``` r
rest_inspec |> 
  filter(str_detect(dba, "[Pp][Ii][Zz][Zz][Aa]")) |>
  mutate(boro = fct_infreq(boro)) |>
  ggplot(aes(x = boro, fill = grade)) + 
  geom_bar() 
```

![](data_wrangling_2_files/figure-gfm/unnamed-chunk-20-2.png)<!-- -->

rename

``` r
rest_inspec |> 
  filter(str_detect(dba, regex("pizza", ignore_case = TRUE))) |>
  mutate(
    boro = fct_infreq(boro),
    boro = fct_recode(boro, "The City" = "Manhattan")) |>
  ggplot(aes(x = boro, fill = grade)) + 
  geom_bar()
```

![](data_wrangling_2_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

Weather

``` r
weather_df = 
  rnoaa::meteo_pull_monitors(
    c("USW00094728", "USW00022534", "USS0023B17S"),
    var = c("PRCP", "TMIN", "TMAX"), 
    date_min = "2021-01-01",
    date_max = "2023-12-31") |>
  mutate(
    name = recode(
      id, 
      USW00094728 = "CentralPark_NY", 
      USW00022534 = "Molokai_HI",
      USS0023B17S = "Waterhole_WA"),
    tmin = tmin / 10,
    tmax = tmax / 10) |>
  select(name, id, everything())
```

    ## Registered S3 method overwritten by 'hoardr':
    ##   method           from
    ##   print.cache_info httr

    ## using cached file: C:\Users\ltquc\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USW00094728.dly

    ## date created (size, mb): 2024-10-16 15:12:29.471384 (8.67)

    ## file min/max dates: 1869-01-01 / 2024-10-31

    ## using cached file: C:\Users\ltquc\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USW00022534.dly

    ## date created (size, mb): 2024-10-16 15:13:05.012676 (3.942)

    ## file min/max dates: 1949-10-01 / 2024-10-31

    ## using cached file: C:\Users\ltquc\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USS0023B17S.dly

    ## date created (size, mb): 2024-10-16 15:13:23.956675 (1.041)

    ## file min/max dates: 1999-09-01 / 2024-10-31

``` r
weather_df |>
  mutate(name = forcats::fct_relevel(name, c("Molokai_HI", "CentralPark_NY", "Waterhole_WA"))) |> 
  ggplot(aes(x = name, y = tmax)) + 
  geom_violin(aes(fill = name), color = "blue", alpha = .5) + 
  theme(legend.position = "bottom")
```

    ## Warning: Removed 19 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](data_wrangling_2_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

``` r
weather_df |>
  mutate(name = forcats::fct_reorder(name, tmax)) |> 
  ggplot(aes(x = name, y = tmax)) + 
  geom_violin(aes(fill = name), color = "blue", alpha = .5) + 
  theme(legend.position = "bottom")
```

    ## Warning: There was 1 warning in `mutate()`.
    ## ℹ In argument: `name = forcats::fct_reorder(name, tmax)`.
    ## Caused by warning:
    ## ! `fct_reorder()` removing 19 missing values.
    ## ℹ Use `.na_rm = TRUE` to silence this message.
    ## ℹ Use `.na_rm = FALSE` to preserve NAs.

    ## Warning: Removed 19 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](data_wrangling_2_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

``` r
weather_df |>
  mutate(name = forcats::fct_relevel(name, c("Molokai_HI", "CentralPark_NY", "Waterhole_WA"))) |> 
  lm(tmax ~ name, data = _)
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ name, data = mutate(weather_df, name = forcats::fct_relevel(name, 
    ##     c("Molokai_HI", "CentralPark_NY", "Waterhole_WA"))))
    ## 
    ## Coefficients:
    ##        (Intercept)  nameCentralPark_NY    nameWaterhole_WA  
    ##              28.40              -10.53              -20.84

PULSE

``` r
pulse_data = 
  haven::read_sas("./data/public_pulse_data.sas7bdat") |>
  janitor::clean_names() |>
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit", 
    names_prefix = "bdi_score_",
    values_to = "bdi") |>
  select(id, visit, everything()) |>
  mutate(
    visit = str_replace(visit, "bl", "00m"),
    visit = factor(visit)) |>
  arrange(id, visit)

print(pulse_data, n = 12)
```

    ## # A tibble: 4,348 × 5
    ##       id visit   age sex     bdi
    ##    <dbl> <fct> <dbl> <chr> <dbl>
    ##  1 10003 00m    48.0 male      7
    ##  2 10003 01m    48.0 male      1
    ##  3 10003 06m    48.0 male      2
    ##  4 10003 12m    48.0 male      0
    ##  5 10015 00m    72.5 male      6
    ##  6 10015 01m    72.5 male     NA
    ##  7 10015 06m    72.5 male     NA
    ##  8 10015 12m    72.5 male     NA
    ##  9 10022 00m    58.5 male     14
    ## 10 10022 01m    58.5 male      3
    ## 11 10022 06m    58.5 male      8
    ## 12 10022 12m    58.5 male     NA
    ## # ℹ 4,336 more rows

Airbnb

``` r
data("nyc_airbnb")

nyc_airbnb |>
  filter(neighbourhood_group == "Manhattan") |> 
  mutate(
    neighbourhood = fct_reorder(neighbourhood, price)) |> 
  ggplot(aes(x = neighbourhood, y = price)) +
  geom_boxplot() +
  coord_flip() + 
  ylim(0, 1000)
```

    ## Warning: Removed 109 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](data_wrangling_2_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->
