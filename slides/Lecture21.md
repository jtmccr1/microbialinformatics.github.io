---
title       : Microbial Informatics
subtitle    : Lecture 21
date        : November 6, 2014
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
* A new homework has been posted and is due on November 22nd
  * work with a partner
  * no more than one explicit loop
* Will have lab period on Friday
* Read Chapters 11 in TAoRP for background material on what is discussed today and Tuesday



---

## Review
* There are high level functions for getting structured data in and out of R - `write.table`, `read.table`
* There are low level functions for input and output that don't require defined data structure - `write`, `scan`, `readLines`

---

## Learning objectives

* Understand how to work with and manipulate character variables


---

## Remember...

Strings are atomic variables made up of characters, numbers, punctuation, etc.
You can form a string by puttting information between `"` and `"`.


```r
name <- "pat"
name
```

```
## [1] "pat"
```

---

## What would happen if we did...


```r
name[1] 
```

---

## What would happen if we did...


```r
name[1] 
```

```
## [1] "pat"
```

* Note that `name` is a vector and so `name[1]` will return the first element of that vector, not the first character of the vector.

---

## But how do we get the first character?

* Get substrings with the `substr` command


```r
substr(x, start, stop)
```

* `x` is the string of interest
* `start` is the position within the string where you want the substring to start
* `stop` is the position within the string where you want the substring to end

---

## For example...


```r
substr(name, 3, 3)
```

```
## [1] "t"
```

```r
substr(name, 2, 3)
```

```
## [1] "at"
```

```r
substr(name, 1, 1)
```

```
## [1] "p"
```

```r
substr(name, 2, 4)
```

```
## [1] "at"
```

---

## What if we have a vector of names?


```r
names <- c("pat", "sarah", "john", "emily", "mary", "susan")
substr(names, 1,2)
```

```
## [1] "pa" "sa" "jo" "em" "ma" "su"
```

---

## What do we need to know to return the last two characters of each person's name?

---

## What do we need to know to return the last two characters of each person's name?

* To get the length of each person's name use the `nchar` command:


```r
name.length <- nchar(names)
substr(names, name.length-2, name.length)
```

```
## [1] "pat" "rah" "ohn" "ily" "ary" "san"
```

* Oops! What happened? How do we fix it?

---

## What do we need to know to return the last two characters of each person's name?

* To get the length of each person's name use the `nchar` command:


```r
name.length <- nchar(names)
substr(names, name.length-1, name.length)
```

```
## [1] "at" "ah" "hn" "ly" "ry" "an"
```

* This is what is called a "fence post" error

---

## Say we have the following names...


```r
names <- c("Pat Schloss", "Mary O'Riordan", "Vince Young", "Kathy Spindler", "Harry Mobley", "Oveta Fuller", "Adam Lauring")
```

* I'd like to generate a vector of first and last names so I can re write the names in alphabetical "Last, First" format.

---

## We need to split the names using the `strsplit` function


```r
strsplit(x, split)
```

* `x` is the string
* `split` is the delimeter to split on
* The output is a list

---

## Let's try it out


```r
split.names <- strsplit(names, " ")
split.names
```

```
## [[1]]
## [1] "Pat"     "Schloss"
## 
## [[2]]
## [1] "Mary"      "O'Riordan"
## 
## [[3]]
## [1] "Vince" "Young"
## 
## [[4]]
## [1] "Kathy"    "Spindler"
## 
## [[5]]
## [1] "Harry"  "Mobley"
## 
## [[6]]
## [1] "Oveta"  "Fuller"
## 
## [[7]]
## [1] "Adam"    "Lauring"
```

---

## Where else could we use `strsplit`?

* Dates


```r
strsplit("11/8/2012", split="/")
```

```
## [[1]]
## [1] "11"   "8"    "2012"
```

* DNA sequences


```r
strsplit("ATGCATCTGA", split="")
```

```
## [[1]]
##  [1] "A" "T" "G" "C" "A" "T" "C" "T" "G" "A"
```

---

## Say we want to reformat our date to be separated by `-`'s

* We can use the `paste` function to stitch the vector together
* `paste(x, y, sep=" ", collapse=NULL)`
* `x` and `y` are two vectors - need only supply one
* `sep` is the character to use to paste the two vectors to each other
* `collapse` is the character to use to merge the elements of the final vector

---

## Try it out with dates


```r
date <- unlist(strsplit("11/8/2012", split="/"))
date
```

```
## [1] "11"   "8"    "2012"
```

```r
paste(date, collapse="-")
```

```
## [1] "11-8-2012"
```

```r
paste("Today is", date, sep=":", collapse="-")
```

```
## [1] "Today is:11-Today is:8-Today is:2012"
```

```r
paste("Today is", paste(date, collapse="-"), sep=": ")
```

```
## [1] "Today is: 11-8-2012"
```

---

## Perhaps you want to paste strings together without using a separator


```r
paste("Today is", paste(date, collapse="-"), sep=": ")
```

```
## [1] "Today is: 11-8-2012"
```

```r
paste("Today is: ", paste(date, collapse="-"), sep="")
```

```
## [1] "Today is: 11-8-2012"
```

```r
paste0("Today is: ", paste(date, collapse="-"))
```

```
## [1] "Today is: 11-8-2012"
```

---

## Let's return to the list of names

* Given a list of names in `First Last` format, can you convert them to `Last, First` format and then alphabetize them?
* Your input should be the `names` vector
* Your output should look like:


```
##      Oveta Fuller      Adam Lauring      Harry Mobley    Mary O'Riordan 
##   "Fuller, Oveta"   "Lauring, Adam"   "Mobley, Harry" "O'Riordan, Mary" 
##       Pat Schloss    Kathy Spindler       Vince Young 
##    "Schloss, Pat" "Spindler, Kathy"    "Young, Vince"
```

---

## Let's return to the list of names


```r
last.first <- function(name){
	split.names <- unlist(strsplit(name, " "))
	l.f <- paste(split.names[2], split.names[1], sep=", ")
	return(l.f)
}
convert.names <- sapply(names, last.first)
sort(convert.names)
```

```
##      Oveta Fuller      Adam Lauring      Harry Mobley    Mary O'Riordan 
##   "Fuller, Oveta"   "Lauring, Adam"   "Mobley, Harry" "O'Riordan, Mary" 
##       Pat Schloss    Kathy Spindler       Vince Young 
##    "Schloss, Pat" "Spindler, Kathy"    "Young, Vince"
```

---

## Formatting text output with `sprintf`


```r
i <- 8
sprintf("the square of %d is %d", i, i^2)
```

```
## [1] "the square of 8 is 64"
```

```r
sprintf("the square root of %d is %6.2f", i, sqrt(i))
```

```
## [1] "the square root of 8 is   2.83"
```

```r
sprintf("%d times 1e6 is %.3e", i, i * 1e6)
```

```
## [1] "8 times 1e6 is 8.000e+06"
```

---

## Things to notice

* `%s` reserves the place for an string
* `%d` reserves the place for an integer
* `%f` reserves the place for an decimal number
* `%e` reserves the place for an number in scientific notation
* For `%f` and `%e` the format is `%m.n`. `n` indicates the number of values to the right of the decimal place to include and `m` indicates the total number of spaces to allot the string
* The output is a string
* Of course, you can do all of this in the text block of a knitr document

---

## Another useful way to format output to text


```r
format(x, trim = FALSE, digits = NULL, nsmall = 0L,
       justify = c("left", "right", "centre", "none"),
       width = NULL, na.encode = TRUE, scientific = NA,
       big.mark = "",   big.interval = 3L,
       small.mark = "", small.interval = 5L,
       decimal.mark = ".", zero.print = NULL,
       drop0trailing = FALSE, ...)`
```

* `x` is a number
* `trim` is whether to right justify numbers to a common width
* `digits` is the maximum number of significant digits
* `nsmall` is the minimum number of digits to the right of the decimal 

--- .segue .dark

## Questions?
