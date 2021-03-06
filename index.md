---
title       : Time Series Decomposition App
subtitle    : Developing Data Products Project
author      : lvillalt
job         :
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : standalone # {selfcontained, draft}
#knit        : slidify::knit2slides
---

## Time Series Decomposition in Data Analysis

Historical data very often will consist of sequences of observations over time, what is referred to as a time series.

Using time series decomposition as part of the exploratory data analysis can be useful even for data sets that, on the surface, are not based on time series.

One possible use case is ruling out, or ruling in, cyclical factors when taking measurements. For example, when aggregating measurements from multiple sensors, spread out over an area, it would be useful to know if certain sensors go offline on a particular day or month. Cyclical patterns like that could possibly affect the distribution of the measurements.

#### The Shiny App

This shiny application provides a sandbox to experiment with time series decomposition, using the `ts` class to define time series objects. And then `decompose()` to perform Moving Average decomposition, Structural Time Series Models using `StructTS()`, and Seasonal Decomposition by Loess using `stl()`. The App has four predefined time series, with up to 15 years of daily data, and can also accept upload of univariate *.csv files.

--- .class #id 

## Some types of Time Series models

**The Application calculates structural time series models using the R commands** 

`tsY <- StructTS(Freq, type="trend")`

`plot(cbind(fitted(tsY), resids=resid(tsY)))`

#### Structural Time Series Models

$y_t = \mu {_t} + \psi {_t} + \gamma {_t} + \epsilon {_t}, t = 1,..., T$

where $\mu{_t}$, $\psi {_t}$, $\gamma {_t}$, and $\epsilon {_t}$, are the trend, cycle, seasonal and irregular components respectively.

The state space form of a time series model is made up of

$\alpha_t = T{_t}\alpha_{t - 1} + \eta {_t}, t = 1,..., T$ a *transition* equation,

$y_t = z{_t}'\alpha_{t} + \epsilon {_t}, t = 1,..., T$ and a *measurement* equation.

Harvey, A.C. & Peters, S., *Estimation Procedures for Structural Time
Series Models*, Journal of Forecasting, Vol. 9, 89-108 (1990)

---

## Seasonal Decomposition by Loess

**The Application calculates Seasonal Decomposition by Loess using the R command stl() as follows** 

`TimeSeries <- ts(Freq, frequency=365)` *(for predefined time series)*

`TimeSeries <- ts(Freq, frequency=12)` *(for uploaded time series)*

`plot(stl(TimeSeries, "per"))`

Cleveland defined STL for a model 

$Y_v = T{_v} + S{_v} + R{_v}, v = 1,..., N$

where $T{_v}$, $S{_v}$, and $R{_v}$ are the trend, seasonal, and residual components.

Cleveland, R.B. *et. al*, *STL: A Seasonal Trend Decomposition Procedure Based on Loess*, Journal of Official Statistics, Vol. 6, No. 1, 3-73 (1990)

---

## Possible Uses

The App can be used to explore analyses with Time Series Decomposition, both with the four predefined time series, and by uploading a univariate time series via a *.csv file.

Both predefined and uploaded time series can be explored via plots, and dynamic tabular views.

While defining and explaining all these types of time series decompositions is beyond the scope of this Shiny App; it is my hope that this useful tool provides a spark of interest in the subject matter.

