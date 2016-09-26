# Notes and Pitfalls of converting Matlab code to R
This is pitfalls I encountered when I convert Matlab code to R code. This is a pretty rough version. I will add details latter

## var1 <-var2
1. Matlab: var1< (-var2), comparison
2. R: var1<- var2, assignment

## subsetting
1. Matlab:()
2. R:[], in R () used for function call

## sequence generation
1. Matlab: 1:0 generate empty matrix. safe in matlab for loop
2. R: 1:0 will generate  c(1,0), not safe in R for loop

## transpose
1. Matlab ' prime symbol
2. R: t() function

## matrix multiplication
1. Matlab: *, in matlab .* means multiplication
2. R: "%\*%", in R * means element-wise multiplication

## Association rule a.\*b\*c
1. Matlab: (a.\*b)*c
2. R: a\*(b%\*%c)

Produce completely different results

## max, min functions
min max functions will behave differently when input is NULL(NA,NaN) in R and Matlab

## find function
1. Matlab
2. R

## struct in Matlab vs list in R

## how to implement multiple return in R?

## missing value or not a number
1. Matlab: NaN
2. R: NA, NaN

## dim number,1&2?
1. Matlab
2. R

## variance
1. Matlab:var(mat)
2. R: apply(mat,2,var)

## random number generator
1. matlab: gammarnd,unifrnd,exprnd,norminv,normcdf,betacdf
2. R: rgamma,runif,rexp,qnorm,pnorm

rate vs scale for gamma and exponential distribution

14, custom utility function explained
"unique"" behaves different

15, smallest number
This is number is machine dependent.
1. Matlab: eps
2. R: .Machine$double.eps

## Assignment with transpose.
p is column vector
1. Matlab: mat[k,:]<- p'
2. R: mat[k,]<- p

It seems R is loose with dimension compatibility checking.


---
**rule of thumb for following rng functions:**

Name in R(prefix in R, suffix in Matlab)
1. density(d,pdf)
2. Probability function(p,cdf)
3. quantile function(q,inv)
4. random number generator(r,rnd)
---
## exponential rng
1. Matlab: exprnd(mu), here is the mu = 1/rate
2. R: rexp(n,rate = 1);

So Matlab:

 ```
 exprnd(2)

```
is equavilent to R:

```r
rexp(1,1/2)
```

## gamma rng
1. Matlab: gammarnd(shape,scale)
2. R: rgamma(n, shape, rate = 1, scale = 1/rate)
3. Rcpp::R: dobule R::rgamma(double a, dobule scale)

## beta rng


1. R:

```
dbeta(x, shape1, shape2, ncp = 0, log = FALSE)
pbeta(q, shape1, shape2, ncp = 0, lower.tail = TRUE, log.p = FALSE)
qbeta(p, shape1, shape2, ncp = 0, lower.tail = TRUE, log.p = FALSE)
rbeta(n, shape1, shape2, ncp = 0)

```
2. Matlab:

```
betapdf(X,A,B)
betacdf(x,a,b)
betainv(P,A,B)
betarnd(A,B)
```
3. Rcpp:R

```
double 	dbeta (double x, double a, double b, int lg)
double 	pbeta (double x, double p, double q, int lt, int lg)
double 	qbeta (double a, double p, double q, int lt, int lg)
double 	rbeta (double a, double b)

```
