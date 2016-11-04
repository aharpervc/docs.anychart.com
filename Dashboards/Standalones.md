# Standalones

* [Overview](#overview)
* [Standalones List](#standalones_list)
* [Using Standalones](#using_standalones)
 * [Scales](#scales)
 * [Legend](#legend)
 * [Axes](#axes)
 * [Color Range](#color_range)
 * [DataGrid](#datagrid)
* [Custom Chart with Standalones](#custom_chart_with_standalones)


## Overview

Standalones are elements of the charting library. They are not charts or parts of charts themselves, they are building blocks that can be used out of a chart. Standalones do not depend on a chart, so they allow to create completely custom charts and manage them or add some custom elements to charts made with AnyChart solutions. 


## Standalones List

There is a list of all standalones AnyChart provides.

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

<tr>
<td>
{api:anychart.standalones.grids.radar}Scale{api}
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

There are more standalone elements you can use. Let's try a Label element and add some description text. Also you can use {api:anychart.standalones.grids.linear}a linear standalone grid{api} in the chart.

```
// set chart width
chart.width("80%");
```

{sample}Standalones\_05{sample}

You can notice that this sample now looks more like a dashboard. So, using standalones is one of the ways to create dashboards.

Below you can find several sample adding standalone elements to the chart.

### Scales

It is possible to create a scale separately from the chart and then use them together.

```
// create a standalone scale
scaleNew = anychart.standalones.scale();
```
а шкал standalone нет

### Legend

It is possible to create a custom standalone legend and edit it in a way you need it to behave or to use one legend for several charts.

```
// create a standalone legend
legend = anychart.standalones.legend();
```

{sample}Standalones\_06{sample}

A standalone legend has neither color nor connection to the series of the chart. There are two ways to set the legend items: it is possible to use the {api:anychart.standalones.Legend#items}items(){api} method and set all items as a simple dataset, or you can set all items automatically - this way is quite practical when there are many charts combined on a stage or when there is no sense in showing a legend for each chart (or if it is inconvenient). 

A standalone legend view can be edited as a chart one. Let's set the items as a dataset through the {api:anychart.standalones.Legend#items}items(){api} method and add the colors to the legend due to the series and make it to select all points of the selected series instead of disabling it. To set the colors to the icons, use the {api:anychart.core.ui.LegendItem#iconFill}iconFill(){api} method. It is also possible to set icon colors through the "iconFill" field in the dataset.

```
legend.items([
    {index: 0, text: "Kansas", iconFill: "#64b5f6"},
    {index: 1, text: "Florida", iconFill: "#1976d2"},
    {index: 2, text: "Arizona", iconFill: "#ef6c00"},
    {index: 3, text: "Washington", iconFill: "#ffd54f"}, 
    {index: 4, text: "Massachusetts", iconFill: "#455a64"},
    {index: 5, text: "Texas", iconFill: "#96a6a6"},
    {index: 6, text: "Iowa", iconFill: "#dd2c00"}
]);
```

{sample}Standalones\_07{sample}

The next sample demonstrates the {api:anychart.standalones.Legend#itemsSource}itemsSource{api} method, which makes it easier to unite several legends if necessary.

```
legend.items([
    {index: 0, text: "Kansas", iconFill: "#64b5f6"},
    {index: 1, text: "Florida", iconFill: "#1976d2"},
    {index: 2, text: "Arizona", iconFill: "#ef6c00"},
    {index: 3, text: "Washington", iconFill: "#ffd54f"}, 
    {index: 4, text: "Massachusetts", iconFill: "#455a64"},
    {index: 5, text: "Texas", iconFill: "#96a6a6"},
    {index: 6, text: "Iowa", iconFill: "#dd2c00"}
]);
```

{sample}Standalones\_08{sample}

### Axes

Adding a standalone axis can be a great choice when you need to use one axis for several charts. Let's create a sample with five [Sparkline Charts](../Basic_Chart_Types/)

```
// add an axis
addAxis = anychart.standalones.axes.linear();
```

{sample}Standalones\_09{sample}

тут какая то фигня со спарклайнами, аж совсем


### Color Range

Color Range is a tool showing how important is this or that value compared to other. It is possible to add a {api:anychart.standalones.ColorRange}standalone Color Range{api} on a chart. The best chart types for standalone creating are Maps, Heat Maps, Tree Maps and other scatter charts. Let's start with a simple HeatMap.

```
// create a heat map
```

{sample}Standalones\_10{sample}

10

### DataGrid

11

### TimeLine

12

### ResourceList

13


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

{sample}Standalones\_14{sample}

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

{sample}Standalones\_13{sample}

Now it is the time to use Graphics JS to add some elements imitating chart points and a grid. Let's make it a Column Chart with two series.

```

```

{sample}Standalones\_14{sample}

As you can notice, there are more standalone elements that can be used in a chart or a dashboard. Let's add text elements and a table to make the sample look more like a dashboard.

```

```

{sample}Standalones\_15{sample}

