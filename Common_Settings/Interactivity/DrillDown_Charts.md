{:index 1}

# Drill-down Chart

* [Overview](#overview)
* [Step by Step Guide](#step-by-step-guide)
 * [Prepare Data](#prepare-data)
 * [Implement Drilldown](#implement-drilldown)
 * [Tune the Chart](#tune-the-chart)
 * [Drill-Up Button](#drill-up-button)
* [Improvements](#improvements)
 * [Multilevel Drilldown](#multilevel-drilldown)
 * [Change Series Type](#change-series-type)
 * [Table Data](#table-data) 
 * [Event Listeners](#event-listeners)

## Overview

Creating a chart with drilldown in AnyChart is very easy and can be done in using so-called event listeners and amazingly flexible API and data model. The very minimum you need is to create a chart, feed it proper data and then tell chart what to do when the point is clicked.

## Step by Step Guide

Сначала показать  самый крутой пример,  а потом перейти к пошаговому приходу к нему

{sample}CS\_Drilldown\_Chart\_03{sample}

### Prepare Data

Drilldown data can be organized like this, each row has x and value and a field where the drill-down data set set is stored. 

```
var data = [
    {"x": 2015, "value": 2195081, "drillDown": [
        {"x": "Q1", "value": 792026},
        {"x": "Q2", "value": 610501},
        {"x": "Q3", "value": 441843},
        {"x": "Q4", "value": 350711}
    ]},
    {"x": 2016, "value": 3257447, "drillDown": [
        {"x": "Q1", "value": 1378786},
        {"x": "Q2", "value": 571063},
        {"x": "Q3", "value": 510493},
        {"x": "Q4", "value": 797105}
    ]},
    {"x": 2017, "value": 1963407, "drillDown": [
        {"x": "Q1", "value": 499299},
        {"x": "Q2", "value": 649963},
        {"x": "Q3", "value": 571176},
        {"x": "Q4", "value": 242969}
    ]}
];
```

[Такие вставки делать когда нужно подавать ссылки на гибкость] X and Value are reserved names for AnyChart and it is the easiest way to go but you can use any names or even simple arrays using our data set mapping option, see more at Data Set Article:

Then we simply feed this data set to a constructor that, creates a chart and displays a chart on the page in some block-based element:

```
// create a chart
var chart = anychart.column(data);

// display chart in a div named 'container'
chart.container('container').draw();
```

### Implement Drilldown

And tell chart what to do when a point (single chart element, a column in this case) is clicked:

```
// when a 'pointClick' event happens
chart.listen('pointClick', function (e) {
  // check if there is drillDown data available
  if (e.point.get('drillDown')) {
    // if so, assign to the only data series we have
    chart.getSeries(0).data(e.point.get('drillDown'));
  }
  else {
    // otherwise assign this series the initial
    // dataset and return to the initial state
    chart.getSeries(0).data(data);
  }
});
```

That’s it, you can see it yourself: 

{sample}CS\_Drilldown\_Chart\_01{sample}

http://jsfiddle.net/89Lj8w0y/11/

Basically the work is done, this foundation provides us with all we need and we will now [tune the chart](#tune-the-chart), add [a drill-up button], [multi-level drill-down](#multilevel-drilldown) and ability to [define the series type of drill-down series](#change-series-type).

И на этом месте шаги где можно добавить:

## Tune the Chart

настройки красоты, где мы настраиваем оси, тултипы и интерактивность

{sample}CS\_Drilldown\_Chart\_02{sample}

## Drill-Up Button

Кнопку back каким-либо способом, при этом можно на самом деле показывать например только нашу кнопку

{sample}CS\_Drilldown\_Chart\_03{sample}

### jQuery Option

, но линковать примеры c jquery 

### Pure HTML Option

чистым html (ну или показывать с чистым html, а линковать нашу и jquery)

## Improvements

## Multilevel Drilldown

потом говорим что на самом деле изначальный код позволяет вставить многоуровневую вложенность и все будет тоже работать

{sample}CS\_Drilldown\_Chart\_04{sample}

## Change Series Type

Как вариант можно еще добавить потом выбор типа серии в данных http://jsfiddle.net/89Lj8w0y/12/

{sample}CS\_Drilldown\_Chart\_05{sample}

### Table Data

Если вы высираете данные в плоском виде, то можно и так - нужен пример с плоскими данными и организацией из них drilldown

{sample}CS\_Drilldown\_Chart\_06{sample}

### Event Listeners

сослаться и скаазть что можно много разного делать
