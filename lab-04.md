Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Anaelle Gackiere
Sys.Date()

### Load packages and data

``` r
# install.packages("devtools")
# devtools::install_github("rstudio-education/dsbox") did this for myself
library(tidyverse) 
library(dsbox) 
data ("dennys")
data ("laquinta")
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

There are 1643 rows and 6 columns for the Dennys dataset.Each row
represents one Dennys location and the variables include city, address,
state, zip, longitude, and latitude.

``` r
dim(dennys)
```

    ## [1] 1643    6

``` r
head(dennys)
```

    ## # A tibble: 6 × 6
    ##   address                        city       state zip   longitude latitude
    ##   <chr>                          <chr>      <chr> <chr>     <dbl>    <dbl>
    ## 1 2900 Denali                    Anchorage  AK    99503    -150.      61.2
    ## 2 3850 Debarr Road               Anchorage  AK    99508    -150.      61.2
    ## 3 1929 Airport Way               Fairbanks  AK    99701    -148.      64.8
    ## 4 230 Connector Dr               Auburn     AL    36849     -85.5     32.6
    ## 5 224 Daniel Payne Drive N       Birmingham AL    35207     -86.8     33.6
    ## 6 900 16th St S, Commons on Gree Birmingham AL    35294     -86.8     33.5

``` r
dim(laquinta) # just checking
```

    ## [1] 909   6

``` r
head(laquinta)
```

    ## # A tibble: 6 × 6
    ##   address                    city         state zip   longitude latitude
    ##   <chr>                      <chr>        <chr> <chr>     <dbl>    <dbl>
    ## 1 793 W. Bel Air Avenue      "\nAberdeen" MD    21001     -76.2     39.5
    ## 2 3018 CatClaw Dr            "\nAbilene"  TX    79606     -99.8     32.4
    ## 3 3501 West Lake Rd          "\nAbilene"  TX    79601     -99.7     32.5
    ## 4 184 North Point Way        "\nAcworth"  GA    30102     -84.7     34.1
    ## 5 2828 East Arlington Street "\nAda"      OK    74820     -96.6     34.8
    ## 6 14925 Landmark Blvd        "\nAddison"  TX    75254     -96.8     33.0

There are 909 rows and 6 columns for the La Quinta dataset. Each row
represents one La Quinta location and the variables include city,
address, state, zip, longitude, and latitude.

### Exercise 2

Remove this text, and add your answer for Exercise 2 here. Add code
chunks as needed. Don’t forget to label your code chunk. Do not use
spaces in code chunk labels.

### Exercise 3

…

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…

Add exercise headings as needed.
