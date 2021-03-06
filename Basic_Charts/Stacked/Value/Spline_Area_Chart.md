{:index 3}
# Stacked Spline Area Chart

* [Overview](#overview)
* [Quick Start](#quick_start)
* [Adjusting](#adjusting)

## Overview

A Stacked Spline Area Chart is a multi-series Spline Area Chart that displays the trend of the value each series contributes over time or categories. The difference between simple Area Chart and Spline Area is that points and angles are replaced with a single spline.

The concept of stacking in AnyChart is described in this article: [Stacked (Overview)](../Overview).

## Quick Start

To build a Stacked Spline Area Chart, create a multi-series [Spline Area Chart](../../Spline_Area_Chart) and set the {api:anychart.scales.Linear#stackMode}stackMode(){api} method into <strong>value</strong>:

```
// create a chart
var chart = chart.area();

// enable the value stacking mode
chart.yScale().stackMode("value");

// create splineArea series
var series1 = chart.splineArea(seriesData_1);
var series2 = chart.splineArea(seriesData_2);
```

{sample}BCT\_Stacked\_Spline\_Area\_Chart{sample}

## Adjusting

The Spline Area series' settings are mostly the same as other series'. The majority of information about adjusting series in AnyChart is given in the [General Settings article](../../General_Settings).