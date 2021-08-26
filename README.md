# RLinearRegression

Linear regression is used to predict the value of a variable based on the value of another variable. Using scatterplots, we can create a linear regression line to show correlation. I am going to show how to do this in both base R and ggplot2


# Base R
We are going to use the `trees` dataset that is already in R to create a basic scatterplot and later add a regression line. We are going to create a basic scatterplot with girth as the x-variable and height as the y-variable, or the dependent.

```r
# load and view dataset
trees = trees
View(trees)
# plot
plot(trees$Height, trees$Girth)
```

### Add Labels and Color
We can label the axes and title the graph using the following functions:
`xlab()` - x-axis title
`ylab()` - y-axis title
`main()` - main graph title
`pch()` - shape of plotted points, numbered from 1-20, google to view the different shapes
`col()` - color of plotted points

```r
# add labels
plot(trees$Height, trees$Girth,
     xlab = "Tree Height", ylab = "Tree Girth",
     pch = 16, col = "purple", main = "Tree Height and Girth")
```

## Linear Model
The `lm()` function allows us to see the coefficients of the regression line for the datapoints on the scatterplot:

```r
> lm(trees$Girth ~ trees$Height)

Call:
lm(formula = trees$Girth ~ trees$Height)

Coefficients:
 (Intercept)  trees$Height  
     -6.1884        0.2557  
```

To actually plot this, we use the `abline()` and `lm()` functions:

```r
# plot line within graph
abline(lm(trees$Girth ~ trees$Height))
```

### Residuals, standard error, and degrees of freedom
Base R also allows us to find other statistics about our dataset, but to do this, we will have to assign a name to our `lm()` variable

```r
# assign name to lm
model = lm(trees$Girth ~ trees$Height)
# view summary
> summary(model)

Call:
lm(formula = trees$Girth ~ trees$Height)

Residuals:
    Min      1Q  Median      3Q     Max 
-4.2386 -1.9205 -0.0714  2.7450  4.5384 

Coefficients:
             Estimate Std. Error t value
(Intercept)  -6.18839    5.96020  -1.038
trees$Height  0.25575    0.07816   3.272
             Pr(>|t|)   
(Intercept)   0.30772   
trees$Height  0.00276 **
---
Signif. codes:  
  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’
  0.1 ‘ ’ 1

Residual standard error: 2.728 on 29 degrees of freedom
Multiple R-squared:  0.2697,	Adjusted R-squared:  0.2445 
F-statistic: 10.71 on 1 and 29 DF,  p-value: 0.002758
```

# ggplot2
ggplot2 is a great data visualization package that is used to add extra detail and has more capabilities than base R. We can use the same dataset, `trees`, but we need to ensure that the variables we want are numeric within R with the `str()` function

```r
str(trees)
'data.frame':	31 obs. of  3 variables:
 $ Girth : num  8.3 8.6 8.8 10.5 10.7 10.8 11 11 11.1 11.2 ...
 $ Height: num  70 65 63 72 81 83 66 75 80 75 ...
 $ Volume: num  10.3 10.3 10.2 16.4 18.8 19.7 15.6 18.2 22.6 19.9 ...
```
All are numeric, so we are ready to go! Let's load the library and begin making a plot with the `ggplot()` function. If you do not already have `ggplot2` installed, use `install.packages("ggplot2")` to do so.

```r
# load library
library(ggplot2)
# plot
ggplot(trees, aes(x = Height, y = Girth)) +
  geom_point()
```
`trees` - this is the dataset we are using
`aes(x = Height, y = Girth)` - R is case sensitive, so we need to ensure that both are capitalized
 ` + geom_point()` - this "adds" what type of graph we want to the function, telling the computer we want a scatterplot.
 
 ## Add regression line
We can quickly add a regression model in ggplot by adding another function to our graph, just as we added our scatterplot function, we add `geom_smooth(method = lm)`

```r
# add regression line
ggplot(trees, aes(x = Height, y = Girth)) +
  geom_point(size = 4) +
  geom_smooth(method = lm)
  ```
 The extra lines around are the confidence interval












