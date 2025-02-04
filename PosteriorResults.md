Posterior Results
================

``` r
library(here)
```

Run all models and available species in `RunModels.Rmd`. Save all output
to your working directory. Tp run this file, you need the following
WinBugs output files:

  - `sim_CDEM_1h`, `sim_CDEM_2h`, `sim_CDEM_3h`, `sim_CDEM_4h`
  - `sim_VAL_1h`, `sim_VAL_2h`, `sim_VAL_3h`, `sim_VAL_4h`
  - `sim_ZPAL_1h`, `sim_ZPAL_2h`. `sim_ZPAL_3h`, `sim_ZPAL_4h`

-----

## Table 1

Model comparison statistics. Done for CDEM model 1 (logit-normal,
homogeneous). Repeat code for other results.

``` r
load(here("output","sim_CDEM_1h"))
sim <- sim_CDEM_1h
load(here("data","data.y.CDEM"))
```

``` r
mat.mu<-array(NA, c(34,16))
for (j in 1:34)
  for (k in 1:16)
    mat.mu[j,k]<-mean(sim$sims.list$mu[ , j, k])

mat.y<-array(NA, c(34,16))
for (j in 1:34)
  for (k in 1:16)
    mat.y[j,k]<-rbinom(1, 1, mat.mu[j,k])

(G<-sum((mat.y - data.y.CDEM)^2, na.rm=TRUE))
## [1] 32
(P<-sum((var(mat.y))^2))
## [1] 1.768551
(D <- G + P)
## [1] 33.76855
```

-----

## FIGURE 3

plots of `alpha0.mn` for 3 species

``` r
lgt <- function(x){exp(x)/(1+exp(x))}
load(here("output","sim_CDEM_1h"))
load(here("output","sim_CDEM_2h"))
load(here("output","sim_CDEM_3h"))
load(here("output","sim_CDEM_4h"))
sim1 <- sim_CDEM_1h
rm(sim_CDEM_1h)
sim2 <- sim_CDEM_2h
rm(sim_CDEM_2h)
sim3 <- sim_CDEM_3h
rm(sim_CDEM_3h)
sim4 <- sim_CDEM_4h
rm(sim_CDEM_4h)

par(mfrow=c(1,3),oma=c(3,3,1,1), mar=c(2.1, 3.1, 3.8, 2.1))
plot(density(lgt(sim1$sims.list$alpha0.mn)),xlim=c(0,1.1),ylim=c(0,7),lwd=1.2,xlab="",ylab="",main="(a) CDEM",col="blue")
lines(density(lgt(sim2$sims.list$alpha0.mn)),lty=1,lwd=2,col="red")
lines(density(lgt(sim3$sims.list$alpha0.mn)),lty=2,lwd=2,col="red")
lines(density(lgt(sim4$sims.list$alpha0.mn)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(lgt(rnorm(nsim,0,1))),lty=3)

mtext(outer=T, line=-0.5, side=2, "Probability Density", cex=1) 
mtext(outer=T, line=2, side=1, expression(paste("Logistic-scaled mean occupancy probability (", italic(mu[0]),")", sep="")), cex=1.5) 

legend(.51,7.2,legend=c("Prior"),col=c("black"),lty=3,cex=1.1,bty="n")
legend(.51,6.5,legend=c("p constant","p vary"),col=c("blue"),lty=c(1,2),title="Logit-Normal",cex=1.1,bty="n")
legend(.51,4.8,legend=c("p constant","p vary"),col=c("red"),lty=c(1,2),title="Logit-CAR",cex=1.1,bty="n")
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
load(here("output","sim_VAL_1h"))
load(here("output","sim_VAL_2h"))
load(here("output","sim_VAL_3h"))
load(here("output","sim_VAL_4h"))
sim1 <- sim_VAL_1h
rm(sim_VAL_1h)
sim2 <- sim_VAL_2h
rm(sim_VAL_2h)
sim3 <- sim_VAL_3h
rm(sim_VAL_3h)
sim4 <- sim_VAL_4h
rm(sim_VAL_4h)

plot(density(lgt(sim1$sims.list$alpha0.mn)),xlim=c(0,1.1),ylim=c(0,7),lwd=1.2,xlab="",ylab="",main="(b) VAL",col="blue")
lines(density(lgt(sim2$sims.list$alpha0.mn)),lty=1,lwd=2,col="red")
lines(density(lgt(sim3$sims.list$alpha0.mn)),lty=2,lwd=2,col="red")
lines(density(lgt(sim4$sims.list$alpha0.mn)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(lgt(rnorm(nsim,0,1))),lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
load(here("output","sim_ZPAL_1h"))
load(here("output","sim_ZPAL_2h"))
load(here("output","sim_ZPAL_3h"))
load(here("output","sim_ZPAL_4h"))
sim1 <- sim_ZPAL_1h
rm(sim_ZPAL_1h)
sim2 <- sim_ZPAL_2h
rm(sim_ZPAL_2h)
sim3 <- sim_ZPAL_3h
rm(sim_ZPAL_3h)
sim4 <- sim_ZPAL_4h
rm(sim_ZPAL_4h)

plot(density(lgt(sim1$sims.list$alpha0.mn)),xlim=c(0,1.1),ylim=c(0,7),lwd=1.2,xlab="",ylab="",main="(c) ZPAL",col="blue")
lines(density(lgt(sim2$sims.list$alpha0.mn)),lty=1,lwd=2,col="red")
lines(density(lgt(sim3$sims.list$alpha0.mn)),lty=2,lwd=2,col="red")
lines(density(lgt(sim4$sims.list$alpha0.mn)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(lgt(rnorm(nsim,0,1))),lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r

rm(sim1);rm(sim2);rm(sim3);rm(sim4)
```

-----

## FIGURE 4

plots of `sigma.a0` for 3 species

``` r
load(here("output","sim_CDEM_1h"))
load(here("output","sim_CDEM_2h"))
load(here("output","sim_CDEM_3h"))
load(here("output","sim_CDEM_4h"))
sim1 <- sim_CDEM_1h
rm(sim_CDEM_1h)
sim2 <- sim_CDEM_2h
rm(sim_CDEM_2h)
sim3 <- sim_CDEM_3h
rm(sim_CDEM_3h)
sim4 <- sim_CDEM_4h
rm(sim_CDEM_4h)

par(mfrow=c(1,3),oma=c(3,3,1,1), mar=c(2.1, 3.1, 3.8, 2.1))
plot(density(sqrt(sim1$sims.list$sig2.a0)),xlim=c(0,4),ylim=c(0,1.5),lwd=1.2,xlab="",ylab="",main="(a) CDEM",col="blue")
lines(density(sqrt(sim2$sims.list$sig2.a0)),lty=1,lwd=2,col="red")
lines(density(sqrt(sim3$sims.list$sig2.a0)),lty=2,lwd=2,col="red")
lines(density(sqrt(sim4$sims.list$sig2.a0)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(sqrt(rgamma(nsim,1,1))),lty=3)

mtext(outer=T, line=-0.5, side=2, "Probability Density", cex=1) 
mtext(outer=T, line=2, side=1, expression(paste("Between unit occupancy standard deviation (", italic(sigma[0]),")")), cex=1.5) 

legend("topleft",legend=c("Prior"),col=c("black"),lty=3,cex=1.1,bty="n")
legend(-.15,1.4,legend=c("p constant","p vary"),col=c("blue"),lty=c(1,2),title="Logit-Normal",cex=1.1,bty="n")
legend("topright",legend=c("p constant","p vary"),col=c("red"),lty=c(1,2),title="Logit-CAR",cex=1.1,bty="n")
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
load(here("output","sim_VAL_1h"))
load(here("output","sim_VAL_2h"))
load(here("output","sim_VAL_3h"))
load(here("output","sim_VAL_4h"))
sim1 <- sim_VAL_1h
rm(sim_VAL_1h)
sim2 <- sim_VAL_2h
rm(sim_VAL_2h)
sim3 <- sim_VAL_3h
rm(sim_VAL_3h)
sim4 <- sim_VAL_4h
rm(sim_VAL_4h)

plot(density(sqrt(sim1$sims.list$sig2.a0)),xlim=c(0,4),ylim=c(0,1.5),lwd=1.2,xlab="",ylab="",main="(b) VAL",col="blue")
lines(density(sqrt(sim2$sims.list$sig2.a0)),lty=1,lwd=2,col="red")
lines(density(sqrt(sim3$sims.list$sig2.a0)),lty=2,lwd=2,col="red")
lines(density(sqrt(sim4$sims.list$sig2.a0)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(sqrt(rgamma(nsim,1,1))),lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
load(here("output","sim_ZPAL_1h"))
load(here("output","sim_ZPAL_2h"))
load(here("output","sim_ZPAL_3h"))
load(here("output","sim_ZPAL_4h"))
sim1 <- sim_ZPAL_1h
rm(sim_ZPAL_1h)
sim2 <- sim_ZPAL_2h
rm(sim_ZPAL_2h)
sim3 <- sim_ZPAL_3h
rm(sim_ZPAL_3h)
sim4 <- sim_ZPAL_4h
rm(sim_ZPAL_4h)
plot(density(sqrt(sim1$sims.list$sig2.a0)),xlim=c(0,4),ylim=c(0,1.5),lwd=1.2,xlab="",ylab="",main="(c) ZPAL",col="blue")
lines(density(sqrt(sim2$sims.list$sig2.a0)),lty=1,lwd=2,col="red")
lines(density(sqrt(sim3$sims.list$sig2.a0)),lty=2,lwd=2,col="red")
lines(density(sqrt(sim4$sims.list$sig2.a0)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(sqrt(rgamma(nsim,1,1))),lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r


rm(sim1);rm(sim2)
```

-----

## FIGURE 5

plots of `sigma.a1` for 3 species

``` r
load(here("output","sim_CDEM_1h"))
load(here("output","sim_CDEM_2h"))
load(here("output","sim_CDEM_3h"))
load(here("output","sim_CDEM_4h"))
sim1 <- sim_CDEM_1h
rm(sim_CDEM_1h)
sim2 <- sim_CDEM_2h
rm(sim_CDEM_2h)
sim3 <- sim_CDEM_3h
rm(sim_CDEM_3h)
sim4 <- sim_CDEM_4h
rm(sim_CDEM_4h)

par(mfrow=c(1,3),oma=c(3,3,1,1), mar=c(2.1, 3.1, 3.8, 2.1))
plot(density(sqrt(sim1$sims.list$sig2.a1),bw=.08),xlim=c(0,2.4),ylim=c(0,1.8),lwd=1.2,xlab="",ylab="",main="(a) CDEM",col="blue")
lines(density(sqrt(sim2$sims.list$sig2),bw=.08),lty=1,lwd=2,col="red")
lines(density(sqrt(sim3$sims.list$sig2),bw=.08),lty=2,lwd=2,col="red")
lines(density(sqrt(sim4$sims.list$sig2.a1),bw=.08),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(sqrt(rgamma(nsim,1,1))),lty=3)

mtext(outer=T, line=-0.5, side=2, "Probability Density", cex=1) 
mtext(outer=T, line=2, side=1, expression(paste("Within unit occupancy standard deviations (", italic(sigma[1])," and ", italic(sigma[2]),")")), cex=1.5) 

legend(1.1,1.9,legend=c("Prior"),col=c("black"),lty=3,cex=1.1,bty="n")
legend(1.1,1.75,legend=c("p constant","p vary"),col=c("blue"),lty=c(1,2),title=expression(paste("Logit-Normal (", italic(sigma[1]),")")),cex=1.1,bty="n")
legend(1.1,1.3,legend=c("p constant","p vary"),col=c("red"),lty=c(1,2),title=expression(paste("Logit-CAR (", italic(sigma[2]),")")),cex=1.1,bty="n")
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
load(here("output","sim_VAL_1h"))
load(here("output","sim_VAL_2h"))
load(here("output","sim_VAL_3h"))
load(here("output","sim_VAL_4h"))
sim1 <- sim_VAL_1h
rm(sim_VAL_1h)
sim2 <- sim_VAL_2h
rm(sim_VAL_2h)
sim3 <- sim_VAL_3h
rm(sim_VAL_3h)
sim4 <- sim_VAL_4h
rm(sim_VAL_4h)

plot(density(sqrt(sim1$sims.list$sig2.a1),bw=.08),xlim=c(0,2.4),ylim=c(0,1.8),lwd=1.2,xlab="",ylab="",main="(b) VAL",col="blue")
lines(density(sqrt(sim2$sims.list$sig2),bw=.08),lty=1,lwd=2,col="red")
lines(density(sqrt(sim3$sims.list$sig2),bw=.08),lty=2,lwd=2,col="red")
lines(density(sqrt(sim4$sims.list$sig2.a1),bw=.08),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(sqrt(rgamma(nsim,1,1))),lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
load(here("output","sim_ZPAL_1h"))
load(here("output","sim_ZPAL_2h"))
load(here("output","sim_ZPAL_3h"))
load(here("output","sim_ZPAL_4h"))
sim1 <- sim_ZPAL_1h
rm(sim_ZPAL_1h)
sim2 <- sim_ZPAL_2h
rm(sim_ZPAL_2h)
sim3 <- sim_ZPAL_3h
rm(sim_ZPAL_3h)
sim4 <- sim_ZPAL_4h
rm(sim_ZPAL_4h)

plot(density(sqrt(sim1$sims.list$sig2.a1),bw=.08),xlim=c(0,2.4),ylim=c(0,1.8),lwd=1.2,xlab="",ylab="",main="(c) ZPAL",col="blue")
lines(density(sqrt(sim2$sims.list$sig2),bw=.08),lty=1,lwd=2,col="red")
lines(density(sqrt(sim3$sims.list$sig2),bw=.08),lty=2,lwd=2,col="red")
lines(density(sqrt(sim4$sims.list$sig2.a1),bw=.08),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
lines(density(sqrt(rgamma(nsim,1,1))),lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r

rm(sim1);rm(sim2)
```

-----

## FIGURE 6

plot of posterior means of z props for logit-normal occupancy and
heterogeneous detection model.

``` r
pl <- 1:16    # all plots
pl <- c(2,4,5,7,10,12,13,15)  # water
pl <- c(1,3,6,8,9,11,14,16)  # boat-based
load(here("data","data.y.CDEM"))
load(here("data","data.y.ZPAL"))
load(here("data","data.y.VAL"))
prop.CDEM <- apply(data.y.CDEM[,pl],1,mean,na.rm=T)
prop.VAL <- apply(data.y.VAL[,pl],1,mean,na.rm=T)
prop.ZPAL <- apply(data.y.ZPAL[,pl],1,mean,na.rm=T)

load(here("output","sim_CDEM_4h"))
sim4 <- sim_CDEM_4h
rm(sim_CDEM_4h)
z4.mns <- sim4$mean$propz
z4.ci <- sim4$summary[73:106,c(3,7)]

par(mfrow=c(1,3),oma=c(3,3,1,1), mar=c(2.1, 3.1, 3.8, 2.1))
plot(1:34,z4.mns,pch=1,main="(a) CDEM",xlab="",ylab="")
segments(1:34,z4.ci[1:34,1],1:34,z4.ci[1:34,2],lty=1)
points(1:34,apply(data.y.CDEM[,c(1,3,6,8,9,11,14,16) ],1,mean,na.rm=T),pch=17)  # boat
points(1:34,apply(data.y.CDEM[,c(2,4,5,7,10,12,13,15) ],1,mean,na.rm=T),pch=15)  #water
abline(h=mean(plogis(sim4$sims.list$alpha0.mn)),col="red")
abline(h=plogis(sim4$summary[70,c(3,7)]),col="red",lty=2)

mtext(outer=T, line=-0.5, side=2, "Estimated occupancy proportion", cex=1) 
mtext(outer=T, line=2, side=1, "Unit", cex=1.4) 
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
load(here("output","sim_VAL_4h"))
sim4 <- sim_VAL_4h
rm(sim_VAL_4h)
z4.mns <- sim4$mean$propz
z4.ci <- sim4$summary[73:106,c(3,7)]

plot(1:34,z4.mns,pch=1,main="(b) VAL",xlab="",ylab="")
segments(1:34,z4.ci[1:34,1],1:34,z4.ci[1:34,2],lty=1)
points(1:34,apply(data.y.VAL[,c(1,3,6,8,9,11,14,16) ],1,mean,na.rm=T),pch=17)  # boat
points(1:34,apply(data.y.VAL[,c(2,4,5,7,10,12,13,15) ],1,mean,na.rm=T),pch=15)  #water
abline(h=mean(plogis(sim4$sims.list$alpha0.mn)),col="red")
abline(h=plogis(sim4$summary[70,c(3,7)]),col="red",lty=2)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

``` r
load(here("output","sim_ZPAL_4h"))
sim4 <- sim_ZPAL_4h
rm(sim_ZPAL_4h)
z4.mns <- sim4$mean$propz
z4.ci <- sim4$summary[73:106,c(3,7)]

plot(1:34,z4.mns,pch=1,main="(c) ZPAL",xlab="",ylab="",ylim=c(0,1))
segments(1:34,z4.ci[1:34,1],1:34,z4.ci[1:34,2],lty=1)
points(1:34,apply(data.y.ZPAL[,c(1,3,6,8,9,11,14,16) ],1,mean,na.rm=T),pch=17)  # boat
points(1:34,apply(data.y.ZPAL[,c(2,4,5,7,10,12,13,15) ],1,mean,na.rm=T),pch=15)  #water
abline(h=mean(plogis(sim4$sims.list$alpha0.mn)),col="red")
abline(h=plogis(sim4$summary[70,c(3,7)]),col="red",lty=2)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

-----

## FIGURE 7

plots of p (in-water) for 3 species

``` r
load(here("output","sim_CDEM_1h"))
load(here("output","sim_CDEM_2h"))
load(here("output","sim_CDEM_3h"))
load(here("output","sim_CDEM_4h"))
sim1 <- sim_CDEM_1h
rm(sim_CDEM_1h)
sim2 <- sim_CDEM_2h
rm(sim_CDEM_2h)
sim3 <- sim_CDEM_3h
rm(sim_CDEM_3h)
sim4 <- sim_CDEM_4h
rm(sim_CDEM_4h)

par(mfrow=c(1,3),oma=c(3,3,1,1), mar=c(2.1, 3.1, 3.8, 2.1))
plot(density(sim1$sims.list$p),xlim=c(0.2,1),ylim=c(0,15),lwd=1.2,xlab="",ylab="",main="(a) CDEM",col="blue")
lines(density(sim2$sims.list$p),lty=1,lwd=2,col="red")
lines(density(sim3$sims.list$p),lty=2,lwd=2,col="red")
lines(density(sim4$sims.list$p),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
abline(h=1,lty=3)

mtext(outer=T, line=-0.5, side=2, "Probability Density", cex=1) 
mtext(outer=T, line=2, side=1, expression(paste("In-water detection probability ", italic(p[1]), sep="")), cex=1.5) 

legend(.1,7.2+8,legend=c("Prior"),col=c("black"),lty=3,cex=1.1,bty="n")
legend(.1,6.5+8,legend=c("p constant","p vary"),col=c("blue"),lty=c(1,2),title="Logit-Normal",cex=1.1,bty="n")
legend(.1,4.8+8,legend=c("p constant","p vary"),col=c("red"),lty=c(1,2),title="Logit-CAR",cex=1.1,bty="n")
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
load(here("output","sim_VAL_1h"))
load(here("output","sim_VAL_2h"))
load(here("output","sim_VAL_3h"))
load(here("output","sim_VAL_4h"))
sim1 <- sim_VAL_1h
rm(sim_VAL_1h)
sim2 <- sim_VAL_2h
rm(sim_VAL_2h)
sim3 <- sim_VAL_3h
rm(sim_VAL_3h)
sim4 <- sim_VAL_4h
rm(sim_VAL_4h)

plot(density((sim1$sims.list$p)),xlim=c(0.2,1),ylim=c(0,35),lwd=1.2,xlab="",ylab="",main="(b) VAL",col="blue")
lines(density((sim2$sims.list$p)),lty=1,lwd=2,col="red")
lines(density((sim3$sims.list$p)),lty=2,lwd=2,col="red")
lines(density((sim4$sims.list$p)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
abline(h=1,lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
load(here("output","sim_ZPAL_1h"))
load(here("output","sim_ZPAL_2h"))
load(here("output","sim_ZPAL_3h"))
load(here("output","sim_ZPAL_4h"))
sim1 <- sim_ZPAL_1h
rm(sim_ZPAL_1h)
sim2 <- sim_ZPAL_2h
rm(sim_ZPAL_2h)
sim3 <- sim_ZPAL_3h
rm(sim_ZPAL_3h)
sim4 <- sim_ZPAL_4h
rm(sim_ZPAL_4h)

plot(density((sim1$sims.list$p)),xlim=c(0.2,1),ylim=c(0,7),lwd=1.2,xlab="",ylab="",main="(c) ZPAL",col="blue")
lines(density((sim2$sims.list$p)),lty=1,lwd=2,col="red")
lines(density((sim3$sims.list$p)),lty=2,lwd=2,col="red")
lines(density((sim4$sims.list$p)),lty=2,lwd=2,col="blue")
nsim <- dim(sim2$sims.matrix)[1]
abline(h=1,lty=3)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r

rm(sim1);rm(sim2);rm(sim3);rm(sim4)
```

-----

## FIGURE 8

plot of posterior in-boat detection probabilities for logit-normal
occupancy and heterogeneous detection model.

``` r
pl <- 1:16    # all plots
pl <- c(2,4,5,7,10,12,13,15)  # water
pl <- c(1,3,6,8,9,11,14,16)  # boat-based
load(here("data","data.y.CDEM"))
load(here("data","data.y.ZPAL"))
load(here("data","data.y.VAL"))
prop.CDEM <- apply(data.y.CDEM[,pl],1,mean,na.rm=T)
prop.VAL <- apply(data.y.VAL[,pl],1,mean,na.rm=T)
prop.ZPAL <- apply(data.y.ZPAL[,pl],1,mean,na.rm=T)

load(here("output","sim_CDEM_4h"))
sim4 <- sim_CDEM_4h
rm(sim_CDEM_4h)
q4.mns <- sim4$mean$q
q4.ci <- sim4$summary[73:106-3-34,c(3,7)]
z4.mns <- sim4$mean$propz

par(mfrow=c(1,3),oma=c(3,3,1,1), mar=c(2.1, 3.1, 3.8, 2.1))
plot(1:34,q4.mns,pch=1,main="(a) CDEM",xlab="",ylab="", ylim=c(0,1))
segments(1:34,q4.ci[1:34,1],1:34,q4.ci[1:34,2],lty=1)
points(1:34, z4.mns, col="blue", pch = 17)
abline(h=mean(q4.mns),col="red")
abline(h=c(mean(q4.ci[,1]), mean(q4.ci[,2])),col="red",lty=2)

mtext(outer=T, line=-0.5, side=2, expression(paste("In-boat detection probability ", italic(p[2]), sep="")), cex=1.5) 
mtext(outer=T, line=2, side=1, "Unit", cex=1.4) 
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

``` r
load(here("output","sim_VAL_4h"))
sim4 <- sim_VAL_4h
rm(sim_VAL_4h)
q4.mns <- sim4$mean$q
q4.ci <- sim4$summary[73:106-3-34,c(3,7)]
z4.mns <- sim4$mean$propz

plot(1:34,q4.mns,pch=1,main="(b) VAL",xlab="",ylab="", ylim=c(0,1))
segments(1:34,q4.ci[1:34,1],1:34,q4.ci[1:34,2],lty=1)
points(1:34, z4.mns, col="blue", pch = 17)
abline(h=mean(q4.mns),col="red")
abline(h=c(mean(q4.ci[,1]), mean(q4.ci[,2])),col="red",lty=2)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

``` r
load(here("output","sim_ZPAL_4h"))
sim4 <- sim_ZPAL_4h
rm(sim_ZPAL_4h)
q4.mns <- sim4$mean$q
q4.ci <- sim4$summary[73:106-3-34,c(3,7)]
z4.mns <- sim4$mean$propz

plot(1:34,q4.mns,pch=1,main="(c) ZPAL",xlab="",ylab="",ylim=c(0,1))
segments(1:34,q4.ci[1:34,1],1:34,q4.ci[1:34,2],lty=1)
points(1:34, z4.mns, col="blue", pch = 17)
abline(h=mean(q4.mns),col="red")
abline(h=c(mean(q4.ci[,1]), mean(q4.ci[,2])),col="red",lty=2)
```

![](PosteriorResults_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->
