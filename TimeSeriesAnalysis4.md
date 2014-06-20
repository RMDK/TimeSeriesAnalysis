Time Series Analysis 4
========================================================
[Visit my website](http://rmdk.ca/projects/) for more like this! I would love to hear your feedback.

```r
library(astsa, quietly=TRUE, warn.conflicts=FALSE)
require(knitr)
library(ggplot2)
```
#### Data Sources:
Heavily borrowed from:

* Textbook: [Time Series Analysis and It's Application](http://www.stat.pitt.edu/stoffer/tsa3/)

* [Wikipedia](http://en.wikipedia.org/wiki/Stationary_process)

* [Online course](https://onlinecourses.science.psu.edu/stat510/?q=node/47) at Penn State

## 1.0 Forecasting with (non-seasonal) ARIMA Models

An ARIMA model expresses _x_<sub>_t_</sub> as a function of past values of _x_ and/or past and present time errors. When we try to forecast a value past the end of the series, we  might need values from the observed time series that have not been observed. For example, and AR(2) model uses the previous two _x_ values in its specification. To forecast the first value we need observed values for _x_<sub>_n_</sub> , and _x_<sub>_n - 1_</sub>. Yet, the second forecasted point requires a value that hasn't occurred yet. To remedy this, we use the first forecasted value to satisfy the forecasting of the second value.

An important component of this procedure involves keeping track of the standard error, which is increasing as we forecast more and more values into the "future". To do this we introduce the concept of psi-weights.

### 1.1 Psi-weight representation of an ARIMA model

##### To Do

## 2.0 Examples

Let's consider the water level data from before


```r
data <- c(14.3, 14.6, 13.5, 14.2, 12.1, 14.19, 14.55, 13.6, 14.59, 16.6, 15.4,
          12.89, 12.2, 12.15, 10.89, 11.11, 11.98, 13.44, 14.05, 13.91, 14.1,
          12.66, 14.6, 16.7, 15.4, 17.1, 15.45, 16.76, 15.7, 14.1, 15.3, 16.4,
          17.09, 16.8, 16.98, 16.39, 15.8, 15.1, 13.7, 13.79, 15.7)
# load built in commands for TSA diagnostics
source(url("http://lib.stat.cmu.edu/general/tsa2/Rcode/itall.R")) 
```

```
##   itall has been installed
```

```r
plot(data, type='b', ylab='water level')
```

<img src="figure/unnamed-chunk-3.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" width="504" />

Now forecast using the new built in functions...


```r
forecast<-sarima.for(data, 5, 1, 0, 0) # 5 forecasts with an AR(1) model
```

<img src="figure/unnamed-chunk-4.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" width="720" />

```r
forecast$pred # actual prediction values
```

```
## Time Series:
## Start = 42 
## End = 46 
## Frequency = 1 
## [1] 15.37 15.14 14.98 14.86 14.78
```

```r
forecast$se # standard error for prediction values
```

```
## Time Series:
## Start = 42 
## End = 46 
## Frequency = 1 
## [1] 1.152 1.411 1.525 1.579 1.606
```

> The red line represents our predictions, while the blue lines are the 95% confidence intervals.

#### Where will the forecast end up?

For a stationary model, the forecasts of future values eventually converge to the mean and stay there, this is what is already almost occuring in our prediction.

Obviously, this isn't a very productive prediction, as we would rather work with many years of data, and incorporate seasonal trends to make a more accurate prediction. We will do that next, and provide more examples.

Next lesson [here]()
