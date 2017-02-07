---
title: Candlestick Charts in R | Examples | Plotly
name: Candlestick Charts
permalink: r/candlestick-charts/
description: How to create candlestick charts in R.
layout: base
thumbnail: thumbnail/candlestick.jpg
language: r
page_type: example_index
has_thumbnail: true
display_as: financial
order: 2
output:
  html_document:
    keep_md: true
---



### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.

```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.5.6.9000'
```

### Basic Candlestick


```r
library(plotly)
library(quantmod)

msft <- getSymbols("MSFT", auto.assign = F)
dat <- as.data.frame(msft)
dat$date <- index(msft)
dat <- subset(dat, date >= "2016-01-01")

names(dat) <- sub("^MSFT\\.", "", names(dat))

p <- plot_ly(dat, x = ~date, xend = ~date, color = ~Close > Open, 
             colors = c("red", "forestgreen"), hoverinfo = "none") %>%
       add_segments(y = ~Low, yend = ~High, size = I(1)) %>%
       add_segments(y = ~Open, yend = ~Close, size = I(3)) %>%
       layout(showlegend = FALSE, yaxis = list(title = "Price")) %>%
       rangeslider()

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="finance/basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4297.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

#Reference

See [https://plot.ly/r/reference](https://plot.ly/r/reference) for more information and chart attribute options!