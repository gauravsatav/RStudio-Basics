# Introduction


```r
library(datasets)
library(ggplot2)

ggplot(mtcars,aes(wt,mpg,color=as.factor(cyl)))+geom_point()
```

<img src="01-Introduction_files/figure-html/unnamed-chunk-1-1.png" width="672" />


