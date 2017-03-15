{:index 3}
# Axes Labels Formatting

* [Overview](#overview)
* [Enable or Disable](#enable_or_disable)
* [Formatting Labels](#formatting_labels)
 * [Prefixes and Postfixes](#prefixes_and_postfixes)
 * [Number Formatting](#number_formatting)
 * [Label Length](#label_length)
* [Visual Appearance](#visual_appearance)
 * [Font](#font)
 * [Background](#background)
* [Positioning](#positioning)
 * [Labels Alignment](#labels_alignment)
 * [Padding](#padding)
 * [Rotation](#rotation)
 * [Stagger Mode](#stagger_mode)
* [First and Last Labels](#first_and_last_labels)
* [Y-Axis Labels: Fixed Width](#y-axis_labels-fixed-width)
* [X-Axis Labels: Fixed Width and Text Wrapping](#x-axis-labels-wrapping-width)
* [Overlapping](#overlapping)

## Overview

With AnyChart, you've got a full control over the axes labels: you can format them, tune visual appearance and position. All major settings and features of axes labels are described in this tutorial.

## Enable or Disable

Each axis in AnyChart JavaScript graphs has its own labels settings. By default labels for all axes are enabled. You can enable or disable labels for the given axis using enabled method of {api:anychart.core.axes.Linear#labels}labels(){api} method:

```
var labels = chart.xAxis().labels();
labels.enabled(false);
```

A line chart with labels enabled for both Y-Axes and disabled for X-Axis is shown in the sample below.

{sample}AGST\_Labels\_Formatting\_01{sample}

## Formatting Labels

In order to make a chart readable and understandable it is very important to format axes labels in a proper way, e.g. add "$" prefix if values are in dollars or add "°F" postfix if values are in Fahrenheit degrees.
  
You have full control over the axis labels in {api:anychart.core.ui.LabelsFactory#textFormatter}textFormatter(){api} parameter of {api:anychart.core.axes.Linear#labels}labels(){api} method.
  
It's possible to make text formatting easier using tokens - special strings that are the component can parse. A token looks like *{%KeywordName}*, for example *{%Value}* or *{%AxisName}*. Before displaying each token is being replaced by the corresponding value. In the [Text Formatters article](Text_Formatters#tokens_list) you can find a list of available tokens.

Text Formatter works with function or with a string with or without tokens. A default axis label shows the value, the default formatting looks like this if it is represented by a function:

```
chart.yAxis().textFormatter(function(){
  return this.value
});
```

The following code sample demonstrates the same with the string formatting:

```
chart.yAxis().textFormatter("{%Value}");
```

Tokens can be also used in XML and JSON, unlike other formatting methods. Setting tokens through the JSON format looks like this:

```
"labels":{
  "enabled":true,
  "textFormatter":"$ {%Value}{groupsSeparator: }"
}
```

### Prefixes and Postfixes

To add a prefix or a postfix to the labels use {api:anychart.core.ui.LabelsFactory#textFormatter}textFormatter(){api} method with the token:

```
chart.yAxis().labels().textFormatter("${%Value}");
```

Or you can create a formatting function and so more. This code recalculates the dollar-axis values into euro and sets the euro sign as the prefix:

```
chart.yAxis().labels().textFormatter(function(){
  var value = this.value;
  // scale USD to EUR and rouns the result
  value = Math.round(value*0.7094716);
  return "€ " + value;
});
```

{sample}AGST\_Labels\_Formatting\_02{sample}

### Number Formatting

It might be necessary to format the value that corresponds to the label, e.g. do scaling or some mathematical operations using tokens, textFormatter or any other javascript functions.
  
Here is a sample of a financial chart with euro and dollar axes. Axis that represents dollar rate is set as the main one and the additional euro axis gets value from the dollar axis and transforms it into euro according to the exchange rate. Some separators are added to adjust X-axis labels visual appearance.

```
// formats labels of additional axis
var yLabels1 = chart.yAxis(1).labels();
yLabels1.textFormatter("€ {%Value}{scale:(113e-2)|()}");
```

{sample}AGST\_Labels\_Formatting\_03{sample}

Find more about text formatting parameters in the [Text Formatters article](Common_Settings/Text_Formatters#formatting_parameters).

### Label Length

If the label value is too long, it is possible to limit the number of characters using standard javascript method **substr()**: 

```
// limits length of x axis labels to 3 or less
chart.xAxis().labels().textFormatter(function(){
  var value = this.value;
  // limit the number of symbols to 3
  value = value.substr(0, 3);
  return value
});
```

{sample}AGST\_Labels\_Formatting\_04{sample}

Another way to limit the labels' length is to use the {api:anychart.core.ui.Label#width}width(){api} and the {api:anychart.core.ui.LabelsFactory.Label#textOverflow}textOverflow(){api} methods. The {api:anychart.core.ui.LabelsFactory.Label#textOverflow}textOverflow(){api} method allows to set how to show the text which overflows the defined width: simply cut it or to show it with an ellipsis.

```
// format labels
chart.xAxis().labels().width(45);
chart.xAxis().labels().height(50);
chart.xAxis().labels().textOverflow(anychart.graphics.vector.Text.TextOverflow.ELLIPSIS);
```

{sample}AGST\_Labels\_Formatting\_05{sample}

To limit the number of decimal characters or edit the separator use [formatting parameters](Common_Settings/Text_Formatters#formatting_parameters).

## Visual Appearance

The visual appearance of axes labels can be customized according to the chart design. Label visual settings consist of background settings (which include margins, inner color, and border) and font settings.  
  
Learn more about these settings in: [Background tutorial](../Appearance_Settings/Background), [Text Settings tutorial](../Appearance_Settings/Text_Settings).

### Font

Font settings of labels are configured as any text. You can specify font face, size and color or set the text to HTML mode using {api:anychart.core.ui.Label#fontFamily}fontFamily(){api}, {api:anychart.core.ui.Label#fontSize}fontSize(){api}, {api:anychart.core.ui.Label#fontColor}fontColor(){api} and {api:anychart.core.ui.Label#useHtml}useHtml(){api} methods. 

```
var labels = chart.xAxis().labels();
labels.fontFamily("Courier");
labels.fontSize(12);
labels.fontColor("#125393");
labels.fontWeight("bold");
labels.useHtml(false);
```

### Background

Labels background is configured using the (api:anychart.core.ui.Label#background).background(){api} method:

```   
// background settings
var xLabelsBackground = chart.xAxis().labels().background();
xLabelsBackground.enabled(true);
xLabelsBackground.stroke("#cecece");
xLabelsBackground.cornerType("round");
xLabelsBackground.corners(5);
```

{sample}AGST\_Labels\_Formatting\_06{sample}

Find more about background settings in [Background tutorial](../Appearance_Settings/Background).

## Positioning

AnyChart provides a number of options to control the position of axes labels, depending on the values displayed - choose where and how labels should be placed, whether they should be rotated or staggered and set alignment.

### Labels Alignment

To specify how labels are aligned use {api:anychart.graphics.vector.Text#hAlign}hAlign(){api} and {api:anychart.graphics.vector.Text#vAlign}vAlign(){api} methods.

```
// format labels
chart.yAxis().labels().hAlign("center");
chart.xAxis().labels().offsetY(5);
```

{sample}AGST\_Labels\_Formatting\_07{sample}

### Padding

To change the paddings between the label's background borders and the text use {api:anychart.core.ui.Label#padding}padding(){api}. This parameter's value is to be set in px. Padding may contain up to 4 values in the following order: Top, Right, Bottom and Left. It is not necessary to set all 4 values. 

```
chart.yAxis().labels().padding(0, 10, 15, 0);
```

### Rotation

One of the most useful features of label positioning is ability to show rotated labels. To rotate labels set the angle of rotation in the {api:anychart.core.ui.LabelsFactory#rotation}rotation(){api} method:

```
chart.yAxis().labels().rotation(90)
```

{sample}AGST\_Labels\_Formatting\_09{sample}

### Stagger Mode

Stagger mode is a setting that allows to place labels into several lines. Use the {api:anychart.core.axes.Linear#staggerMode} and the {api:anychart.core.axes.Linear#staggerLines}staggerLines(){api} methods to enable and configure this mode:

```
// enable stagger mode
chart.xAxis().staggerMode(true);
// adjust settings for stagger mode
chart.xAxis().staggerLines(2);
```

{sample}AGST\_Labels\_Formatting\_10{sample}

## First and Last Labels

There are special methods to force showing or hiding the first label and the last label. You can force them to be shown or hide them using the {api:anychart.core.axes.Linear#drawFirstLabel}drawFirstLabel(){api} and {api:anychart.core.axes.Linear#drawLastLabel}drawLastLabel(){api} methods.

```
// disable first and last labels
chart.xAxis().drawFirstLabel(false);
chart.xAxis().drawLastLabel(false);
```

{sample}AGST\_Labels\_Formatting\_11{sample}

<a name="y-axis_labels-fixed-width"/>
## Y-Axis Labels: Fixed Width

It's possible to set fixed custom width for Y axis labels. This function may be of great use in dashboards when it's necessary to sync several charts left and/or right border, which is especially needed when they are displayed in a column and share the same X-axis arguments.

To set the axis width use {api:anychart.core.ui.Label#width}width(){api} attribute for {api:anychart.core.ui.Label}labels(){api}, which accepts positive integer values in pixels:

```
// set yAxis labels width
chart.yAxis().labels().width(50);
```

{sample}AGST\_Labels\_Formatting\_13{sample}

<a name="x-axis-labels-wrapping-width"/>
## X-Axis Labels: Fixed Width and Text Wrapping

Sometimes you may encounter a situation when names shown in labels are too long and chart engine removes some of them because they don't fit the chart size. If you want to show labels anyway you can allow labels to overlap, or change the overflow mode, or set fixed width to the labels and make them wrap their content.

The following example demonstrates the standard behavior of the X-axis labels. As you can see long labels cause the component to skip several labels in order to prevent overlapping:

{sample}AGST\_Labels\_Formatting\_14{sample}

The following sample demonstrates exactly the same configuration but the labels width is set manually to 60 pixels. In this case, component wraps text in order to fit the width:
  
To adjust the labels' width and allow or forbid the labels' text wrapping use {api:anychart.core.ui.Label#width}width(){api} and {api:anychart.core.ui.LabelsFactory#textWrap}textWrap(){api} methods:

```
chart.xAxis().labels().width(60);
chart.xAxis().labels().textWrap("byLetter");
```

{sample}AGST\_Labels\_Formatting\_15{sample}

The following example demonstrates the same data displayed on a bar chart. In order to align multiline text to the right side {api:anychart.graphics.vector.Text#hAlign}hAlign(){api} attribute is set to right:

{sample}AGST\_Labels\_Formatting\_16{sample}

## Overlapping

The {api:anychart.core.axes.Linear#overlapMode}overlapMode(){api} of a chart's {api:anychart.core.axes.Linear}axis{api} can set mode to **noOverlap** and **allowOverlap*:

```
chart.xAxis().overlapMode("allowOverlap");
```

**Note**: overlapping is disabled by default. The sample below demonstrates x labels with overlapping allowed:

{sample}AGST\_Labels\_Formatting\_17{sample}