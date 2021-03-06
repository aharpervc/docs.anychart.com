{:index 3}
Exports
======================

* [Overview](#overview)
* [Export server](#export_server)
* [File name](#file_name)
* [Image](#image)
 * [SVG](#svg)
 * [PNG](#png)
 * [JPG](#jpg)
* [PDF](#pdf)
* [Data](#data)
 * [CSV](#csv)
 * [Excel](#excel)
* [Chart Configuration](#configuration)
 * [JSON](#json)
 * [XML](#xml)

## Overview

AnyChart provides you with ability to export charts to images (SVG, PNG, JPG), PDF or data files (CSV, Excel). These options are available both via [Context menu](./UI_Controls/Context_Menu) and API. Every export has some fine tune options, including an ability to change file name. There is also a special option to save chart [configuration](#configuration) which may be used to debug charts and report issues.

## Export server

**IMPORTANT, DO NOT SKIP THIS PART**

AnyChart "save as" features work via [AnyChart Export Server](Server-side_Rendering), which is hosted at AnyChart.Com server. Although we do our best to keep AnyChart site up and running 24x7x365 - we **do not guarantee** export server availability. If you want to have full control over the ability of the component to export images, or just don't want to use  AnyChart Server due to the security or accessibility concerns - just run Export Server in server mode on the server you control and trust and configure your charts to custom_server.

Custom server address is set like this:

```
anychart.server("http://localhost:2000");
```

You can read all about AnyChart Export Server and Server-side rendering in [AnyChart Export Server](Server-side_Rendering) article.

## File name

If you want to change default file name for all exports at once you can use {api:anychart.exports#filename}anychart.exports.filename(){api} method:

```
anychart.exports.filename('custom_name');
```

After you do so, all files, images, pdf and data, will be saved under this name, unless you override it when calling specific methods as shown below.

## Image

AnyChart js charting library allows to save charts in 3 different image formats: SVG, PNG and JPG, using {api:anychart.core.Chart#saveAsSvg}saveAsSvg(){api}, {api:anychart.core.Chart#saveAsPng}saveAsPng(){api} and {api:anychart.core.Chart#saveAsJpg}saveAsJpg(){api} methods.

Each method has common parameter: filename, and special parameters depending on format.

### SVG

{api:anychart.core.Chart#saveAsSvg}saveAsSvg(){api} can be launched in two modes, one with width and height passed:

```
saveAsSvg({width: 360, height: 500, filename: 'custom_name'})
```

And another one with paper size and page orientation set:

```
saveAsSvg({paperSize: "A4", "landscape": false, "filename": "custom_name"});  
```

### PNG

With {api:anychart.core.Chart#saveAsPng}saveAsPng(){api} you can set width, height and quality in addition to file name:

```
saveAsPng({width: 360, height: 500, quality: 0.3, filename: "custom_name"});
```

### JPG

With {api:anychart.core.Chart#saveAsJpg}saveAsJpg(){api} you can set width, height, quality and forceTransparentWhite flag and in addition to file name:

```
saveAsJpg({width: 360, height: 500, quality: 0.3, forceTransparentWhite: "false", filename: "custom_name"});
```

To launch the export you need to use these methods as shown:

```
// save the chart in SVG format
chart.saveAsSvg();
// save the chart in PNG format
chart.saveAsPng();
// save the chart in JPG format
chart.saveAsJpg();
```

And here is a sample where you can see all methods in action:

{sample}Exports\_01{sample}

## PDF

To save chart in Pdf format use: {api:anychart.core.Chart#saveAsPdf}saveAsPdf{api} method:

```
// initiate saving chart in PDF format
chart.saveAsPdf();
```

{sample}Exports\_02{sample}

## Data

AnyChart provides several methods for saving current chart's data. Output formats are {api:anychart.core.Chart#saveAsCsv}CSV{api} and {api:anychart.core.Chart#saveAsXlsx}saveAsXlsx(){api} (Excel file).

{api:anychart.enums.ChartDataExportMode}ChartDataExportMode{api} parameter defines what data is exported: only the data used by chart (SPECIFIC), all data in the data set (RAW) and a special mode for stock charts allows to export grouped data (GROUPED).

### CSV

With {api:anychart.core.Chart#saveAsCsv}saveAsCsv(){api} you can set how you export data and file name:

```
saveAsCsv({chartDataExportMode: anychart.enums.ChartDataExportMode.RAW, csvSettings: {"rowsSeparator": "\n", "columnsSeparator": ",", "ignoreFirstRow": true}, filename: "csv_file"});
```

### Excel

With {api:anychart.core.Chart#saveAsXlsx}saveAsXlsx(){api} you can set how you export data and file name:

```
// initiate saving chart's data in Xlsx format
chart.saveAsXlsx({chartDataExportMode: anychart.enums.ChartDataExportMode.SPECIFIC, filename: "excel"});
```

To launch the export you need to use these methods as shown:

```
// initiate saving chart's data in Xlsx format
chart.saveAsXlsx();
// initiate saving chart's data in CSV format
chart.saveAsCsv();
```

{sample}Exports\_03{sample}

## Chart Configuration

Chart config may be saved using {api:anychart.core.Chart#saveAsXml}XML{api} and {api:anychart.core.Chart#saveAsJson}JSON{api} methods, this feature may be very useful in debug process or if you want to create some kind of import/export functionality for chart themselves. These methods get output of {api:anychart.core.Chart#toJson}toJson(){api} and {api:anychart.core.Chart#toXml}toXml(){api} methods and allow to save it as file. First parameter is boolean flag that defines if the current [Theme](../Appearance_Settings/Themes) is included in output configuration file.

### XML

```
// save chart data and configuration in XML format
chart.saveAsXml({includeTheme: "false", filename: "chart_xml"});
```

### JSON

```
// save chart data and configuration in Json format
chart.saveAsJson({includeTheme: "false", filename: "chart_json"});
```

Here is a sample of chart save as XML and save as JSON methods:

{sample}Exports\_04{sample}
