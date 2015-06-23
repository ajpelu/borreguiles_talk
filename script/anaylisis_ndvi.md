``` r
library('plyr')
library('dplyr')
```

    ## 
    ## Attaching package: 'dplyr'
    ## 
    ## The following objects are masked from 'package:plyr':
    ## 
    ##     arrange, count, desc, failwith, id, mutate, rename, summarise,
    ##     summarize
    ## 
    ## The following object is masked from 'package:stats':
    ## 
    ##     filter
    ## 
    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library("ggplot2")
library('broom') # tidy results
```

Prepare data
------------

``` r
# Prepare data
machine <- 'ajpeluLap'

di <- paste('/Users/', machine, '/ownCloud/MS/CONGRESO_AEET2015/borreguiles/borreguiles_talk', sep='')

data <- read.csv(file=paste(di, '/data/ndvi_evi_borreguiles.csv', sep=''), header=TRUE, sep=";")
taus <- read.csv(file=paste(di, '/data/ndvi_tau_borreguiles.csv', sep=''), header=TRUE, sep=";")

df <- tbl_df(data)
df_tau <- tbl_df(taus)
```

Explore data of summer NDVI and EVI in Borreguiles
--------------------------------------------------

``` r
# spring NDVI slope
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), ndvi_i_primavera_pendiente)
```

    ## Source: local data frame [1 x 3]
    ## 
    ##        mean       sd       se
    ## 1 -27.33557 116.0539 7.075932

``` r
# spring NDVI tau
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), ndvi_i_primavera_tau)
```

    ## Source: local data frame [1 x 3]
    ## 
    ##          mean        sd          se
    ## 1 -0.02482156 0.1125146 0.006860136

``` r
# spring EVI slope
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), evi_i_primavera_pendiente)
```

    ## Source: local data frame [1 x 3]
    ## 
    ##        mean       sd       se
    ## 1 -52.98028 108.8513 6.636783

``` r
# spring EVI tau
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), evi_i_primavera_tau)
```

    ## Source: local data frame [1 x 3]
    ## 
    ##          mean        sd          se
    ## 1 -0.07634572 0.1536728 0.009369598

``` r
# summer NDVI slope          
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), ndvi_i_verano_pendiente)   
```

    ## Source: local data frame [1 x 3]
    ## 
    ##       mean       sd       se
    ## 1 254.4706 157.3385 9.593096

``` r
# summer NDVI tau  
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), ndvi_i_verano_tau)
```

    ## Source: local data frame [1 x 3]
    ## 
    ##        mean        sd         se
    ## 1 0.3358736 0.1764145 0.01075618

``` r
# summer EVI slope          
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), evi_i_verano_pendiente)   
```

    ## Source: local data frame [1 x 3]
    ## 
    ##       mean       sd       se
    ## 1 168.8105 100.9765 6.156645

``` r
# summer EVI tau  
df %>% summarise_each(funs(mean, sd,se=sd(.)/sqrt(n())), evi_i_verano_tau)
```

    ## Source: local data frame [1 x 3]
    ## 
    ##        mean        sd          se
    ## 1 0.3253271 0.1591637 0.009704384
