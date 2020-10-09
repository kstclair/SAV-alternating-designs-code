Data Clean Up for Modeling
================

``` r
library(here)
```

This file cleans up the original data to provide single species data
sets used in our models.

### Enter in raw data

``` r
data <- read.csv(here("data","dataW97.csv"))  # in water
data2 <- read.csv(here("data","dataB97.csv"))  # in boat
```

### Subunit info

Numbers are the unit identifier for each subunit.

``` r
C <- c(
1,1,1,1,1,1,1,1,
2,2,2,2,2,2,2,2,
3,3,3,3,3,3,3,3,
4,4,4,4,4,4,4,4,
5,5,5,5,5,5,5,5,
6,6,6,6,6,6,6,6,
7,7,7,7,7,7,7,7,
8,8,8,8,8,8,8,8,
9,9,9,9,9,9,9,9,
10,10,10,10,10,10,10,10,
11,11,11,11,11,11,11,11,
12,12,12,12,12,12,12,12,
13,13,13,13,13,13,13,13,
14,14,14,14,14,14,14,14,
15,15,15,15,15,15,15,15,
16,16,16,16,16,16,16,16,
17,17,17,17,17,17,17,17,
18,18,18,18,18,18,18,18,
19,19,19,19,19,19,19,19,
20,20,20,20,20,20,20,20,
21,21,21,21,21,21,21,21,
22,22,22,22,22,22,22,22,
23,23,23,23,23,23,23,23,
24,24,24,24,24,24,24,24,
25,25,25,25,25,25,25,25,
26,26,26,26,26,26,26,26,
27,27,27,27,27,27,27,27,
28,28,28,28,28,28,28,28,
29,29,29,29,29,29,29,29,
30,30,30,30,30,30,30,30,
31,31,31,31,31,31,31,31,
32,32,32,32,32,32,32,32,
33,33,33,33,33,33,33,33,
34,34,34,34,34,34,34,34
)
```

### Pick your species

CDEM is column 4, ZPAL is column 11, VAL is column 13

``` r
#species: VAL=13; CDEM=4; ZPAL=11 
S <-  4                        
```

### Create species specific data for WinBUGS modeling

Change the species column `S` to change species.

``` r
data[,1] <- C                     # making the unit numbers ordered
data2[ ,1] <- C                   # making the unit numbers ordered

y<-array(NA, c(34,16))

## water-based subunits
for (k in c(2,4,5,7,10,12,13,15))
  for (j in 1:34)
    for (l in 1:272){
      if (data[l,1] == j & data[l,2] == k)
        y[j,k]<-data[l, S]
      }
## boat-based subunits
for (k in c(1,3,6,8,9,11,14,16))
  for (j in 1:34)
    for (l in 1:272){
      if (data2[l,1] == j & data2[l,2] == k)
        y[j,k] <- data2[l,S]
      }
```
