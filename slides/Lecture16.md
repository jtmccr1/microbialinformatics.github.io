---
title       : Microbial Informatics
subtitle    : Lecture 16
date        : October 17, 2014
author      : Patrick D. Schloss, PhD (microbialinformatics.github.io)
job         : Department of Microbiology & Immunology
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      #
widgets     : mathjax       # {mathjax, quiz, bootstrap}
mode        : standalone    # {selfcontained, standalone, draft}
knit        : slidify::knit2slides

---

## Announcements
* Project 1 is due on the 24th
* No class on Tuesday (study section)
* Read ***The Art of R Programming*** (Chapters 4 and 5)





---

## Review
* Programs and functions encapsulate repetitive problems
* Using functions makes it easier to debug your code since it reduces the amount of duplicated code

---

## Learning objectives
* How to design a small function from pseudocode
* Additional details about vectors and matrices

---

## Exercise: ChiSquared distribution revisited

*	The distribution of a sum of the squares of k indepdentently sampled normal random variables, where k is the degrees of freedom
* Procedure to create an empirical distribution
    1.	Draw k random variables from a normal distribution with mean 0.0 and standard deviation of 1.0
    2.	Square each of them
    3.  Sum them
    4.	Repeat many times and keep track of how many times you see each value
* Interested in the proportion of the distribution larger than our test statistic

---

## To do...

* Work with a partner and make a simple function called pchisq.rand.
* It should take the parameters: `k`, 	`chi.sq`, and `iters`
* The default value for `iters` should be 1000

* When you do the following:


```r
pchisq.rand(k=4, chi.sq=2, iters=10000)
```

* You should get a value near 0.2642411

---

## Creating a vector


```r
	x <- c(1,2,3)
```

or


```r
	x <- 1:3
	x <- 3:1
```

or


```r
x <- seq(1,3,1)
```

---

## Creating a vector


```r
	x <- vector(length=3)
	x[1] <- 1
	x[2] <- 2
	x[3] <- 3
```

---

## Creating a vector


```r
x<- c(x, c(1,2,3))
```

or


```r
x<- rep(c(1,2,3), 2)
```

---

##	Accessing values in a vector


```r
x[5]		#remember vector indices start at 1
x[5,1]		#is this correct?
v<-3:4
x[v]
x[length(x)]
x[-4]
x[-length(x)]
x[-c(1,2)]
```

---

## Mapping a vector onto a vector


```r
names(x) <- c("a", "b", "c", "d", "e", "f")
x["e"]
```

---

## Recycling: Automatic lengthening of a vector by repeating itself


```r
c(1,2,4) + c(6,0,9,20,22)	#how does R read this expression?  what does it equal?
```

---

##	Filtering:	Extracting subsets from a vector


```r
x <- rep(1:3,2)
x > 1
which(x>1)

subset(x, x>1)
x[x>1]
```

---

## Another method of using logical operators with vectors


```r
ifelse(x > 1, "dog", "cat")
ifelse(x > 1, x, x^2)

z <- seq(1:10)
ifelse(z>7, "C", ifelse(z>4, "B",ifelse(z>0, "A")))
```

---

## Vectorization:	Applying functions to vectors that are applied elementwise


```r
x <- seq(1:3)
y <- seq(3:5)

x>y
x+5
x+y
x^2
sqrt(x)	#many built in functions return vectors
```

---

## Matrices
*	Special types of vectors with extra attibutes: number of rows and number of columns


```r
z <- matrix(c(1,2,3,4,5,6), ncol=2)		#fills by columns
z <- matrix(c(1,2,3,4,5,6), nrow=2)		#fills by columns
z <- matrix(c(1,2,3,4,5,6), nrow=2, byrow=T)		#fills by rows

length(z)		#why?
dim(z)
nrow(z)
ncol(z)

colnames(z) <- c("a", "b", "c")
rownames(z) <- c("d", "e")
```

---

##	Indexing into matrices


```r
z[1,3]
z[2,]
z[,2:3]
z[,-1]
```

---

##	Operations on matrices


```r
y <- matrix(c(1,2,3,4), ncol=2)

y * 2
y * y
y %*% y

apply(y, 1, sum)
apply(y, 2, sum)
```

--- .segue .dark

## Questions?
