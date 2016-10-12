# Standalones

* [Overview](#overview)
* [Standalones List](#standalones_list)
* [Using Standalones](#using_standalones)
* [Custom Chart with Standalones](#custom_chart_with_standalones)

## Overview

Standalones are elements of the charting library. They are not charts or parts of charts themselves, they are building blocks that can be used out of a chart. Standalones do not depend on a chart, so they allow to create completely custom charts and manage them or add some custom elements to charts made with AnyChart solutions. 


## Standalones List

There are 7 stanalones AnyChart provides.

<table>
<tr>
<td>
Standalone
</td>
<td>
What it creates
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.Table}Table(){api}
</td>
<td>
A table 
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.Title}Title(){api}
</td>
<td>
A text element with settings of the title element
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.Legend}Legend(){api}
</td>
<td>
A legend
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.Label}Label(){api}
</td>
<td>
A text element with settings of the label element
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.axes.Linear}Linear{api}
</td>
<td>
A Linear Axis
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.axes.Polar}Polar{api}
</td>
<td>
A Polar Axis
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.axes.Radar}Radar{api}
</td>
<td>
A Radar Axis
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.axisMarkers.line}Line{api}
</td>
<td>
An axis marker of a Line type
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.axisMarkers.Radar}Radar{api}
</td>
<td>
An axis marker of a Radar type
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.axisMarkers.Radar}Text{api}
</td>
<td>
An axis marker of a Text type
</td>
</tr>

<tr>
<td>
{api:anychart.standalones.grids.linear}Linear{api}
</td>
<td>
A Linear grid
</td>
</tr>
<tr>
<td>
{api:anychart.standalones.grids.polar}Polar{api}
</td>
<td>
A Polar grid
</td>
</tr>
<tr>
<td>
{api:anychart.standalones.grids.radar}Radar{api}
</td>
<td>
A Radar grid
</td>
</tr>
</table>



## Using Standalones

Using standalone elements is no more complicated than using basic AnyChart elements. It is possible to create a chart with some standalone elements.

The following sample demonstrates adding a title element on a simple chart:

```
// add a title standalone object on the chart
title = anychart.standalones.title();
title.text("This is the title");
```

{sample}Standalones\_01{sample}

The difference between using a chart title and a standalone title is in positioning. A chart title is positioned automatically, as well as the chart padding. When use standalone title, it is necessary to set padding to the chart in order to prevent title from overlaying the series. Let's add a chart title to the chart, it will make the difference more evident.

```
// add a chart title
cTitle = chart.title("The chart title");
```

{sample}Standalones\_02{sample}

You can see that a chart title is demonstrated under a standalone title with no positioning settings, and the chart is shifted down a little automatically.

Let's set padding to the chart and add a table:

```
// create a table and fill it in
table = anychart.standalones.table();
table.rowsCount(3);
table.colsCount(5);
table.zIndex(100000000);
table.bounds("80%", "37%", 200, 100);
```

{sample}Standalones\_03{sample}

Now, let's set the chart width and add several series.

```
// set chart width
chart.width("80%");
```

{sample}Standalones\_04{sample}

You can notice that this sample now looks more like a dashboard. So, using standalones is one of the ways to create dashboards.

That is how standalone elements can be used within charts. Now, let's create a chart fully based on standalone & graphics elements.


## Custom Chart with Standalones

Using standalones in cooperation with AnyChart Graphics JS elements allows to create a completely custom chart. In this section a simple chart is being created with no elements provided by AnyChart.

Let's start with creating a linear axis with a scale and adding it on a stage:

```
// set the stage
stage = anychart.graphics.create("container");

// create an axis
yAxis = anychart.standalones.axes.linear();

// add scale
yAxis.scale(anychart.scales.linear());

// put the axis on a stage
yAxis.container(stage);
yAxis.draw();
```

{sample}Standalones\_05{sample}

Now, let's make the axis vertical as it is befits to the Y-Axis, and create the X-Axis with adjusting both of them.

```
// create axes
xAxis = anychart.standalones.axes.linear();
xAxis.orientation("bottom");
xAxis.padding().bottom(30);
xAxis.padding().right("40%");
xAxis.padding().left(67);
xAxis.scale(anychart.scales.linear());
```

{sample}Standalones\_06{sample}

Now it is the time to use Graphics JS to add some elements imitating chart points and a grid. Let's make it a Column Chart with two series.

```

```

{sample}Standalones\_07{sample}

As you can notice, there are more standalone elements that can be used in a chart or a dashboard. Let's add text elements and a table to make the sample look more like a dashboard.

```

```

{sample}Standalones\_08{sample}

