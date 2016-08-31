# Legend

* [Overview](#overview)
* [Auto Legend](#auto_legend)
* [Easy Auto Legend for Single Series Charts](#easy_auto_legend_for_single_series_charts)
* [Title](#title)
* [Positioning](#positioning)
* [Visualization](#visualization)
 * [Background](#background)
 * [Size](#size)
 * [Paging](#paging)
 * [Icon Type](#icon_type)
 * [Marker Symbol](#marker_symbol)
* [Series Management](#series_management)
* [Tooltip](#tooltip)
* [Custom Item](#custom_item)
* [Custom Legend](#custom_legend)
* [One Legend for Several Charts](#one_legend_for_several_charts)

## Overview

Legend is a table on a chart listing and explaining the symbols and colors used and with additional information that helps user to understand a chart.

In this article all legends features and setting are explained and demonstrated.

## Auto Legend 

To enable legend you have to specify {api:anychart.core.ui.Legend#enabled}enabled(true){api} parameter of {api:anychart.core.ui.Legend}legend(){api} method:

```
// create chart
var chart = anychart.line();

// enable legend
var legend = chart.legend();
legend.enabled(true);
```

By default legend shows all series names with a symbol that shows the color and the type of the series.

To enable such legend in your chart just enable it:

```
chart.legend(true);
```

In the live sample, please notice that when you move the mouse over the series name in legend - all series elements are highlighted

{sample}AS\_Legend\_01{sample}

## Easy Auto Legend for Single Series Charts

If you are showing a single series chart and want your legend to show all points names and values you should configure legend:

```
var legend = chart.legend();
// enable legend
legend.enabled(true);
// set source of legend items
legend.itemsSourceMode("categories");
```

To create a legend for single series chart you just have to set **categories** value for {api:anychart.core.ui.Legend#itemsSourceMode}itemsSourceMode(){api}.

{sample}AS\_Legend\_02{sample}

## Title

Sometimes you need the title to a legend and sometimes it is superfluous: to enable legend title you have to set {api:anychart.core.ui.Title#enabled}enabled(true){api} parameter of a legend title method as it is shown below

```
var title = chart.legend().title();
title.enabled(true);
```

To specify and format your own title for the legend use {api:anychart.core.ui.Title#text}text(){api} method of a {api:anychart.core.ui.Legend#title}title(){api}. For more information about title settings please refer to the [Title](../Appearance_Settings/Title) article.

```
var title = chart.legend().title();
title.useHtml(true);

// enables legend title
title.enabled(true);
title.text("Total sales<br><i style=\"color: #999; font-weight: 400; font-size: 11px;\">(Year 2004)</i>");

// set font size
title.fontSize(14);
title.hAlign("center");
```

Here is a sample bar chart and the legend has tuned title:

{sample}AS\_Legend\_03{sample}

## Positioning

Depending on the layout and type of your chart you can position legend to a desired place using {api:anychart.core.ui.Legend#position}position(){api} method of {api:anychart.core.ui.Legend}legend(){api}. 

As an addition to the {api:anychart.core.ui.Legend#position}position(){api} method, method {api:anychart.core.ui.Legend#align}align(){api} controls legend alignment.

{sample}AS\_Legend\_04{sample}

*Note:* possible values that can be passed to the {api:anychart.core.ui.Legend#align}align(){api} method are: *Left, Right, Top, Bottom and Center*. Also, possible values depend on the {api:anychart.core.ui.Legend#position}position(){api} parameter. With *Top* and *Bottom* legend position it is possible to use *Left, Right* and *Center* parameters of {api:anychart.core.ui.Legend#align}align(){api}. For *Left* and *Right* values of {api:anychart.core.ui.Legend#position}position(){api} it's possible to use *Top, Bottom* and *Center* parameters of {api:anychart.core.ui.Legend#align}align(){api} method.

## Visualization

As far as a legend is a part of a chart, its appearance should be tuned properly. Main aspects of legend visual appearance are described in this section.

### Background

Legend background allows you to configure the border and the inner color of the legend. Method {api:anychart.core.ui.Legend#background}background(){api} controls background visual appearance. To learn more about background setting please study the [background tutorial](Background).

{sample}AS\_Legend\_05{sample}

### Size

Legend size is controlled by {api:anychart.core.ui.Legend#height}height(){api} and {api:anychart.core.ui.Legend#width}width(){api} parameters. 
    
Sample Pie Chart with a legend of a fixed (75px - width, 140px height) size positioned to the *"Left"* of the chart, aligned to *"Top"*, with padding of 10 pixels:

```
var legend = chart.legend();
// set legend height to 140px
legend.height(140);
// set legend width to 95px
legend.width(95);
```

Here is a sample with adjusted legend size

{sample}AS\_Legend\_06{sample}

*Note:* the space between data plot and legend is controlled using {api:anychart.core.ui.Legend#padding}padding(){api} method.

### Paging

If legend items can't be displayed on a plot of a legend, {api:anychart.core.ui.Legend#paginator}paginator(){api} method controls legend page. Paginator can be placed anywhere inside the legend.

```
// legend settings
var paginator = chart.legend().paginator();
// set paginator layout
paginator.layout("vertical");
// place paginator on the right
paginator.orientation("right");
```

{sample}AS\_Legend\_07{sample}

### Icon Type

When you work with line, spline or stepline chart it's better to use point markers to distinguish different series. By default AnyChart charting library doesn't show marker symbols in legend - only a color representation. There are several methods responsible for icon types in legend. To tune markers in legend icons, adjust the {api:anychart.core.utils.LegendItemSettings#iconMarkerFill}iconMarkerFill(){api}, {api:anychart.core.utils.LegendItemSettings#iconType}iconType(){api} and other methods of the {api:anychart.core.ui.LegendItem}legendItem(){api} instance. 

In the sample below there are four line series, which markers are set of different colors, sizes and shapes. A pair of legend items are left with the default icons and another pair demonstrates tuning the legend item icon into its series marker.

```
var legendItems3 = series3.legendItem();
// series marker type in legend
legendItems3.iconType("line");

// settings for the legend item of the series
var legendItems4 = series4.legendItem();
// set type of icon marker in legend
legendItems4.iconType("line");
```
{sample}AS\_Legend\_08{sample}

The {api:anychart.core.utils.LegendItemSettings#iconType}iconType(){api} method makes legend items look the same as their series markers. Setting the icon type through this method allows to define different icon types for different legend items om the same chart; though, it's possible to set one legend item for the whole chart by setting a theme.

```
themeSettings = {
    "line": {
        "defaultSeriesSettings": {
            "line": {
                "legendItem": {
                    "iconType": "line"
                }
            }
        }
    }
  };

  anychart.theme(themeSettings);
```

{sample}AS\_Legend\_09{sample}


### Marker Symbol

It's possible to make legend items demonstrate markers of the series by setting "marker" to the {api:anychart.core.utils.LegendItemSettings#iconType}iconType(){api} method. This makes a default legend item transform into a marker of its series. This method is also used for setting a custom legend item icon. Look through the following sample.

```
var legendItems3 = series3.legendItem();
// series marker type in legend
legendItems3.iconType("marker");

// settings for legend item of the series
var item = series.legendItem()
// set inner color of icon marker
item.iconMarkerFill("gold");
// set border of icon marker
item.iconMarkerStroke("red");
// set type of icon marker
item.iconType("star6");
```

Here is a sample with different settings for a marker of legend item.

{sample}AS\_Legend\_10{sample}

### Tooltip

If you want to configure legend tooltips - you should do that using {api:anychart.core.ui.Legend#tooltip}tooltip(){api} methods. You can tune its visual appearance and format. In the following sample we will format tooltips of the legend to show detailed description information.

{sample}AS\_Legend\_11{sample}

## Series Management

You can easily control series of the chart using chart legend. You can hide and show any of the series by clicking on the legend items. Here is a sample of column chart with four series. One of the series is already disabled. Click on the last legend item to show hidden series. 

{sample}AS\_Legend\_12{sample}

## Custom Item

When creating legend you can add your own items with any information you want to see on the legend, to do that use {api:anychart.ui.Legend#itemsFormatter}itemsFormatter(){api} method. 

```
var legend = chart.legend();
// adjust legend items
legend.itemsFormatter(function(items){
  // push into items array
  items.push({
    // set text of a new item
    text: "item text "
  });
  // return items array
  return items;
});
```

In the sample chart below we've used custom item that adds *Total* data to legend.

{sample}AS\_Legend\_13{sample}

## Custom Legend

AnyChart JavaScript Framework sets no limits to the amount of legends on one chart plot. Legend can be a part chart as well as a separate unit. Sample below demonstrates three custom legend at the bottom of the chart. 

{sample}AS\_Legend\_14{sample}

## One Legend for Several Charts

As you can see, one legend can contain different information from one chart. Moreover, one legend can contain information from several charts. To add several chart into one legend use {api:anychart.ui.Legend#itemsSource}itemsSource(){api} method and define charts for legend's content.

```
// define charts
var chart2005 = anychart.column();
var chart2006 = anychart.column();

// create custom legend
var legend = anychart.ui.legend();
// set sources for legend items
legend.itemsSource([chart2005, chart2006]);
```

{sample}AS\_Legend\_15{sample}

## One Legend for Several Series

You can attache an event to a legend items. Use {api:anychart.core.ui.Legend#listen}listen(){api} method to set an event for a legend. List of possible event can be found in {api:anychart.enums.EventType}anychart.enums.EventType{api}. For additional information on events in AnyChart you can find in [Event Listeners tutorial](../Common_Settings/Event_Listeners)

```
// create legend
var legend = anychart.ui.legend();

// enable and disable series on legend item click
legend.listen("legendItemClick", function(event) {
  // get item's index
  var index = event["itemIndex"];
  // manage enabled/disabled state of the series
  chart2005.getSeries(index).enabled(! chart2005.getSeries(index).enabled());
  chart2006.getSeries(index).enabled(! chart2006.getSeries(index).enabled());
});
```

Sample below demonstrate managing several series with one legend item.

{sample}AS\_Legend\_16{sample}
