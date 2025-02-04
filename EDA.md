EDA
================

``` r
library(here)
```

### Load data

``` r
# data: the raw data for snorkeling method '97
# data2: the raw data for rake method '97
data <- read.csv(here("data","dataW97.csv"))
data2 <- read.csv(here("data","dataB97.csv"))
```

`data.y.SPECIES`: the 34\*16 binary data for SPECIES by sites and cells,
including both scuba and rake methods.

``` r

load(here("data","data.y.CDEM"))
load(here("data","data.y.ZPAL"))
load(here("data","data.y.VAL"))
```

observed occupancy rates by sampling units (proportion of subunits)

``` r
prop.CDEM <- apply(data.y.CDEM,1,mean,na.rm=T)
prop.VAL <- apply(data.y.VAL,1,mean,na.rm=T)
prop.ZPAL <- apply(data.y.ZPAL,1,mean,na.rm=T)
```

unit-level summary of observed occupancy

``` r
summary(prop.CDEM); sd(prop.CDEM)
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.0000  0.0000  0.0625  0.2270  0.4844  0.9375
## [1] 0.2966214
summary(prop.VAL); sd(prop.VAL)
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.0000  0.1250  0.6625  0.5597  0.9375  1.0000
## [1] 0.4033148
summary(prop.ZPAL); sd(prop.ZPAL)
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 0.00000 0.00000 0.09375 0.15331 0.25000 0.62500
## [1] 0.1829966
```

## FIGURE 2

observed proportion of subunits with SAV detected

``` r
par(mfrow=c(1,3))
par(mfrow=c(1,3),oma=c(3,3,1,1), mar=c(2.1, 3.1, 3.8, 2.1))

plA <- 1:16    # all plots
plW <- c(2,4,5,7,10,12,13,15)  # water
plB <- c(1,3,6,8,9,11,14,16)  # boat-based

boxplot(
  apply(data.y.CDEM[,plW],1,mean,na.rm=T),
  apply(data.y.CDEM[,plB],1,mean,na.rm=T),
  apply(data.y.CDEM[,plA],1,mean,na.rm=T),
  names=c("In-water","Boat-based","Both"), 
  main="(a) CDEM",
  cex=1)

mtext(outer=T, line=-0.5, side=2, "Detection proportion at each unit", cex=1) 
mtext(outer=T, line=2, side=1, "Detection method", cex=1.5) 

boxplot(
  apply(data.y.VAL[,plW],1,mean,na.rm=T),
  apply(data.y.VAL[,plB],1,mean,na.rm=T),
  apply(data.y.VAL[,plA],1,mean,na.rm=T),
  names=c("In-water","Boat-based","Both"), 
  main="(b) VAL")

boxplot(
  apply(data.y.ZPAL[,plW],1,mean,na.rm=T),
  apply(data.y.ZPAL[,plB],1,mean,na.rm=T),
  apply(data.y.ZPAL[,plA],1,mean,na.rm=T),
  names=c("In-water","Boat-based","Both"), 
  main="(c) ZPAL")
```

![](EDA_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->
