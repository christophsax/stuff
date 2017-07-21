Reshape
=======

Eqivalents of R base, tidyverse, data.table or reshape2

## Example

```r
stocks <- data.frame(
  time = as.Date('2009-01-01') + 0:9,
  X = rnorm(10, 0, 1),
  Y = rnorm(10, 0, 2),
  Z = rnorm(10, 0, 4)
)


## Wide to long

### tidyverse

```r
library(tidyr)
gather(stocks, key = stock, value = price, X, Y, Z)
gather(stocks, key = stock, value = price, -time)  # negative col selection
```

### rbase 

```r
z <- reshape(stocks, varying = c("X", "Y", "Z"), v.names = "price", direction = "long", times = c("X", "Y", "Z"), timevar = "stock", idvar = "time")
rownames(z) <- NULL
```

### data.table

```r
library(data.table)
melt(as.data.table(stocks), id.vars = "time")
```

### reshape2

```r
library(reshape2)
melt(stocks, id.vars = "time")
```
