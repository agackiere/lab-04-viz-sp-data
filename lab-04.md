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

### Exercise 2

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

### Exercise 3

On the Dennys website, I only see US locations. On the La Quinta
website, I saw that there are locations in Canada, Mexico, China, New
Zealand, Georgia, Turkey, United Arab Emirates, Columbia, and Ecuador.

### Exercise 4

One way to determine whether or not there are establishments outside the
United States would be by filtering the locations. You can check the
state column and make sure the entries fit the abbreviations for the US
states. I guess you could also plot or check the range of the longitudes
and latitudes, but that seems more time consuming. Another way is by
checking the zipcode; if they’re a different format, then that suggests
the location may not be US-based.

### Exercise 5 and 6

``` r
# filter states not in state abbreviation for Dennys
dennys %>%
  filter(!(state %in% states$abbreviation)) %>%
  nrow()
```

    ## [1] 0

``` r
    # added nrow() for peace of mind and makes sure it worked!

# add country variable
dennys %>%
  mutate(country = "United States")
```

    ## # A tibble: 1,643 × 7
    ##    address                        city    state zip   longitude latitude country
    ##    <chr>                          <chr>   <chr> <chr>     <dbl>    <dbl> <chr>  
    ##  1 2900 Denali                    Anchor… AK    99503    -150.      61.2 United…
    ##  2 3850 Debarr Road               Anchor… AK    99508    -150.      61.2 United…
    ##  3 1929 Airport Way               Fairba… AK    99701    -148.      64.8 United…
    ##  4 230 Connector Dr               Auburn  AL    36849     -85.5     32.6 United…
    ##  5 224 Daniel Payne Drive N       Birmin… AL    35207     -86.8     33.6 United…
    ##  6 900 16th St S, Commons on Gree Birmin… AL    35294     -86.8     33.5 United…
    ##  7 5931 Alabama Highway, #157     Cullman AL    35056     -86.9     34.2 United…
    ##  8 2190 Ross Clark Circle         Dothan  AL    36301     -85.4     31.2 United…
    ##  9 900 Tyson Rd                   Hope H… AL    36043     -86.4     32.2 United…
    ## 10 4874 University Drive          Huntsv… AL    35816     -86.7     34.7 United…
    ## # ℹ 1,633 more rows

``` r
dennys <- dennys %>%
  mutate(country = "United States")

unique(dennys$country)
```

    ## [1] "United States"

``` r
  # just verifying
```

### Exercise 7 and 8

``` r
# For La Quinta; non-US Codes 
laquinta %>%
  filter(!(state %in% state.abb)) %>%
  distinct(state)
```

    ## # A tibble: 11 × 1
    ##    state
    ##    <chr>
    ##  1 AG   
    ##  2 QR   
    ##  3 CH   
    ##  4 NL   
    ##  5 ANT  
    ##  6 ON   
    ##  7 VE   
    ##  8 PU   
    ##  9 SL   
    ## 10 FM   
    ## 11 BC

``` r
laquinta <- laquinta %>%
  mutate(country = case_when(
    state %in% state.abb ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state %in% c("AG", "QR", "CH", "NL", "PU", "SL") ~ "Mexico",
    state == "ANT" ~ "Colombia",
    state == "VE" ~ "Venezuela",
    state == "FM" ~ "China",
    TRUE ~ NA_character_
  ))

table(laquinta$country)
```

    ## 
    ##        Canada         China      Colombia        Mexico United States 
    ##             2             1             1             9           895 
    ##     Venezuela 
    ##             1

``` r
laquinta <- laquinta %>%
  filter(country == "United States")
```

### Exercise 9

Which states have the most and fewest Denny’s locations? What about La
Quinta? Is this surprising? Why or why not?

California has the most Dennys, and Delaware only has one. Texas has the
most La Quintas, while Maine only has one. This does not necessarily
surprise me, given that DE and ME are very small states, while TX and CA
are the most populous states in the US.

``` r
# states with most and least dennys

dennys %>%
  count(state) %>%
  slice_max(n, n = 1)
```

    ## # A tibble: 1 × 2
    ##   state     n
    ##   <chr> <int>
    ## 1 CA      403

``` r
dennys %>%
  count(state) %>%
  slice_min(n, n = 1)
```

    ## # A tibble: 1 × 2
    ##   state     n
    ##   <chr> <int>
    ## 1 DE        1

``` r
# states with most and least laquintas

laquinta %>%
  count(state) %>%
  slice_max(n, n = 1)
```

    ## # A tibble: 1 × 2
    ##   state     n
    ##   <chr> <int>
    ## 1 TX      237

``` r
laquinta %>%
  count(state) %>%
  slice_min(n, n = 1)
```

    ## # A tibble: 1 × 2
    ##   state     n
    ##   <chr> <int>
    ## 1 ME        1

``` r
# Denny’s locations per thousand square miles.
dennys %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

    ## # A tibble: 51 × 4
    ##    state     n name                     area
    ##    <chr> <int> <chr>                   <dbl>
    ##  1 AK        3 Alaska               665384. 
    ##  2 AL        7 Alabama               52420. 
    ##  3 AR        9 Arkansas              53179. 
    ##  4 AZ       83 Arizona              113990. 
    ##  5 CA      403 California           163695. 
    ##  6 CO       29 Colorado             104094. 
    ##  7 CT       12 Connecticut            5543. 
    ##  8 DC        2 District of Columbia     68.3
    ##  9 DE        1 Delaware               2489. 
    ## 10 FL      140 Florida               65758. 
    ## # ℹ 41 more rows

…

### Exercise 10

Which states have the most Denny’s locations per thousand square miles?
What about La Quinta?

``` r
# identifier var
dennys <- dennys %>%
  mutate(establishment = "Denny's")


laquinta <- laquinta %>%
  mutate(establishment = "La Quinta")

# join datasets
dn_lq <- bind_rows(dennys, laquinta)

# plot
ggplot(dn_lq, mapping = aes(
  x = longitude,
  y = latitude,
  color = establishment
)) +
  geom_point()
```

![](lab-04_files/figure-gfm/locations-miles-1.png)<!-- --> …

### Exercise 11

``` r
ggplot(
  dn_lq %>% filter(state == "NC"),
  aes(
    x = longitude,
    y = latitude,
    color = establishment
  )
) +
  geom_point(alpha = 0.5)
```

![](lab-04_files/figure-gfm/NC-1.png)<!-- --> …

### Exercise 12

``` r
ggplot(
  dn_lq %>% filter(state == "TX"),
  aes(
    x = longitude,
    y = latitude,
    color = establishment
  )
) +
  geom_point(alpha = 0.5)
```

![](lab-04_files/figure-gfm/Texas-1.png)<!-- -->

…
