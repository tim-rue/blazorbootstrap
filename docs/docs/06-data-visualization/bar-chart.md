﻿---
title: Blazor Bar Chart
description: A Blazor Bootstrap bar chart component is used to represent data values as vertical bars. It is sometimes used to show trend data and to compare multiple data sets side by side.
image: https://i.imgur.com/IX3bajc.png

sidebar_label: Bar Chart
sidebar_position: 1
---

A Blazor Bootstrap bar chart component is used to represent data values as vertical bars. 
It is sometimes used to show trend data and to compare multiple data sets side by side.

<img src="https://i.imgur.com/IX3bajc.png" alt="Blazor Chart Component - Blazor Bar Chart" />

## Parameters

| Name | Type | Description | Required | Default | Added Version |
|:--|:--|:--|:--|:--|:--|
| Height | int | Gets or sets chart height. | | | 1.0.0 |
| Width | int | Gets or sets chart width. | | | 1.0.0 |

## Methods

| Name | Return type | Descritpion | Added Version |
|:--|:--|:--|:--|
| AddDataAsync | `ChartData` | Adds data to bar chart. | 1.10.0 |
| AddDatasetAsync | `ChartData` | Adds dataset to bar chart. | 1.10.0 |
| InitializeAsync | Task | Initialize Bar Chart. | 1.0.0 |
| UpdateAsync | Task | Update Bar Chart. | 1.0.0 |

## ChartData Members

| Property Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:--|
| Datasets | `List<IChartDataset>` | null | ✔️ | Gets or sets the Datasets. | 1.0.0 |
| Labels | `List<string>` | null | ✔️ | Gets or sets the Labels. | 1.0.0 |

## BarChartDataset Members

:::info
**BarChartDataset** implements **IChartDataset**.
:::

| Property Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:--|
| BackgroundColor | `List<string>` | null | | Get or sets the BackgroundColor. | 1.0.0 |
| BarPercentage | double | 0.8 | | Percent (0-1) of the available width each bar should be within the category width. 1.0 will take the whole category width and put the bars right next to each other. | 1.0.0 |
| BorderColor | `List<string>` | null | | Get or sets the BorderColor. | 1.0.0 |
| BorderRadius | int | 0 | | Border radius. | 1.0.0 |
| BorderWidth | `List<double>` | null | | Get or sets the BorderWidth. | 1.0.0 |
| CategoryPercentage | double | 0.8 | | Percent (0-1) of the available width each category should be within the sample width. | 1.0.0 |
| Clip | string | null | | How to clip relative to chartArea. Positive value allows overflow, negative value clips that many pixels inside chartArea. 0 = clip at chartArea. Clipping can also be configured per side: clip: {left: 5, top: false, right: -2, bottom: 0} | 1.0.0 |
| Datalabels | `BarChartDatasetDataLabels` | | | Get or sets the data labels | | 1.10.2 |
| Data | `List<double>` | null | | Get or sets the Data. | 1.0.0 |
| Hidden | bool | false | | Configures the visibility state of the dataset. Set it to true, to hide the dataset from the chart. | 1.0.0 |
| HoverBackgroundColor | `List<string>` | null | ✔️ | Get or sets the HoverBackgroundColor. | 1.0.0 |
| HoverBorderColor | `List<string>` | null | ✔️ | Get or sets the HoverBorderColor. | 1.0.0 |
| HoverBorderWidth | `List<double>` | null | ✔️ | Get or sets the HoverBorderWidth. | 1.0.0 |
| Label | string | null | | The label for the dataset which appears in the legend and tooltips. | 1.0.0 |
| Type | string | null | ✔️ | Get or sets the chart type. | 1.0.0 |
| XAxisID | string | null | | The ID of the x axis to plot this dataset on. | 1.0.0 |
| YAxisID | string | null | | The ID of the y axis to plot this dataset on. | 1.0.0 |

## BarChartDatasetDataLabels Members

| Property Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:--|
| Align | `string?` | `center` | | Gets or sets the align. | 1.10.2 |
| Anchor | `string?` | `center` | | Gets or sets the anchor. | 1.10.2 |

## BarChartOptions Members

:::info
**BarChartOptions** implements **ChartOptions**.
:::

| Property Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:--|
| IndexAxis | string | x | | The base axis of the chart. 'x' for vertical charts and 'y' for horizontal charts. | 1.0.0 |
| Interaction | `Interaction` | | | Gets or sets the Interaction. | 1.0.0 |
| Layout | `ChartLayout` | | | Gets or sets the ChartLayout. | 1.0.0 |
| Locale | `string?` | | | Gets or sets the locale. By default, the chart is using the default locale of the platform which is running on. | 1.10.0 |
| Plugins | `BarChartPlugins` | | | Gets or sets the Plugins. | 1.10.2 |
| Responsive | bool | false | | Gets or sets the Responsive. | 1.0.0 |
| Scales | `Scales` | | | Gets or sets the Scales. | 1.0.0 |

## Examples

### Prerequisites

Refer to the [getting started guide](/getting-started/blazor-webassembly) for setting up charts.

### How it works

In the following example, a categorical 12-color palette is used.

:::tip
For data visualization, you can use the predefined palettes `ColorBuilder.CategoricalTwelveColors` for a 12-color palette and `ColorBuilder.CategoricalSixColors` for a 6-color palette. 
These palettes offer a range of distinct and visually appealing colors that can be applied to represent different categories or data elements in your visualizations.
:::

<img src="https://i.imgur.com/uAWY4pV.png" alt="Blazor Bootstrap: Bar Chart Component - How it works" />

```cshtml {} showLineNumbers
<BarChart @ref="barChart" Width="800" Class="mb-4" />

<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await RandomizeAsync()"> Randomize </Button>
<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await AddDatasetAsync()"> Add Dataset </Button>
<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await AddDataAsync()">Add Data</Button>
<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await ShowHorizontalBarChartAsync()">Horizontal Bar Chart</Button>
<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await ShowVerticalBarChartAsync()">Vertical Bar Chart</Button>
```

```cs {} showLineNumbers
@code {
    private BarChart barChart = default!;
    private BarChartOptions barChartOptions = default!;
    private ChartData chartData = default!;

    private int datasetsCount = 0;
    private int labelsCount = 0;
    private string[] months = { "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December" };
    private Random random = new();

    protected override void OnInitialized()
    {
        chartData = new ChartData { Labels = GetDefaultDataLabels(6), Datasets = GetDefaultDataSets(3) };
        barChartOptions = new BarChartOptions { Responsive = true, Interaction = new Interaction { Mode = InteractionMode.Index } };
    }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await barChart.InitializeAsync(chartData, barChartOptions);
        }
        await base.OnAfterRenderAsync(firstRender);
    }

    private async Task RandomizeAsync()
    {
        if (chartData is null || chartData.Datasets is null || !chartData.Datasets.Any()) return;

        var newDatasets = new List<IChartDataset>();

        foreach (var dataset in chartData.Datasets)
        {
            if (dataset is BarChartDataset barChartDataset
                && barChartDataset is not null
                && barChartDataset.Data is not null)
            {
                var count = barChartDataset.Data.Count;

                var newData = new List<double>();
                for (var i = 0; i < count; i++)
                {
                    newData.Add(random.Next(200));
                }

                barChartDataset.Data = newData;
                newDatasets.Add(barChartDataset);
            }
        }

        chartData.Datasets = newDatasets;

        await barChart.UpdateAsync(chartData, barChartOptions);
    }

    private async Task AddDatasetAsync()
    {
        if (chartData is null || chartData.Datasets is null) return;

        if (datasetsCount >= 12)
            return;

        var chartDataset = GetRandomBarChartDataset();
        chartData = await barChart.AddDatasetAsync(chartData, chartDataset, barChartOptions);
    }

    private async Task AddDataAsync()
    {
        if (chartData is null || chartData.Datasets is null)
            return;

        if (labelsCount >= 12)
            return;

        var data = new List<IChartDatasetData>();
        foreach (var dataset in chartData.Datasets)
        {
            if (dataset is BarChartDataset barChartDataset)
                data.Add(new BarChartDatasetData(barChartDataset.Label, random.Next(200)));
        }

        chartData = await barChart.AddDataAsync(chartData, GetNextDataLabel(), data);
    }

    private async Task ShowHorizontalBarChartAsync()
    {
        barChartOptions.IndexAxis = "y";
        await barChart.UpdateAsync(chartData, barChartOptions);
    }

    private async Task ShowVerticalBarChartAsync()
    {
        barChartOptions.IndexAxis = "x";
        await barChart.UpdateAsync(chartData, barChartOptions);
    }

    #region Data Preparation

    private List<IChartDataset> GetDefaultDataSets(int numberOfDatasets)
    {
        var datasets = new List<IChartDataset>();

        for (var index = 0; index < numberOfDatasets; index++)
        {
            datasets.Add(GetRandomBarChartDataset());
        }

        return datasets;
    }

    private BarChartDataset GetRandomBarChartDataset()
    {
        var c = ColorBuilder.CategoricalTwelveColors[datasetsCount].ToColor();

        datasetsCount += 1;

        return new BarChartDataset()
            {
                Label = $"Product {datasetsCount}",
                Data = GetRandomData(),
                BackgroundColor = new List<string> { c.ToRgbString() },
                BorderColor = new List<string> { c.ToRgbString() },
                BorderWidth = new List<double> { 0 },
            };
    }

    private List<double> GetRandomData()
    {
        var data = new List<double>();
        for (var index = 0; index < labelsCount; index++)
        {
            data.Add(random.Next(200));
        }

        return data;
    }

    private List<string> GetDefaultDataLabels(int numberOfLabels)
    {
        var labels = new List<string>();
        for (var index = 0; index < numberOfLabels; index++)
        {
            labels.Add(GetNextDataLabel());
        }

        return labels;
    }

    private string GetNextDataLabel()
    {
        labelsCount += 1;
        return months[labelsCount - 1];
    }

    #endregion Data Preparation
}
```

[See the demo here.](https://demos.blazorbootstrap.com/charts/bar-chart#how-it-works)

### Horizontal bar chart

<img src="https://i.imgur.com/MIMC8wz.png" alt="Blazor Bootstrap: Bar Chart Component - Horizontal bar chart" />

```cshtml {} showLineNumbers
<BarChart @ref="barChart" Height="300" Class="mb-4" />
```

```cs {} showLineNumbers
@code {
    private BarChart barChart = default!;
    private BarChartOptions barChartOptions = default!;
    private ChartData chartData = default!;

    protected override void OnInitialized()
    {
        var labels = new List<string> { "Chrome", "Firefox", "Safari", "Edge" };
        var datasets = new List<IChartDataset>();

        var dataset1 = new BarChartDataset()
            {
                Data = new List<double> { 55000, 15000, 18000, 21000 },
                BackgroundColor = new List<string> { ColorBuilder.CategoricalTwelveColors[0] },
                BorderColor = new List<string> { ColorBuilder.CategoricalTwelveColors[0] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset1);

        chartData = new ChartData { 
            Labels = labels, 
            Datasets = datasets };

        barChartOptions = new BarChartOptions();
        barChartOptions.Responsive = true;
        barChartOptions.Interaction = new Interaction { Mode = InteractionMode.Y };
        barChartOptions.IndexAxis = "y";

        barChartOptions.Scales.X.Title.Text = "Visitors";
        barChartOptions.Scales.X.Title.Display = true;

        barChartOptions.Scales.Y.Title.Text = "Browser";
        barChartOptions.Scales.Y.Title.Display = true;

        barChartOptions.Plugins.Legend.Display = false;
    }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await barChart.InitializeAsync(chartData, barChartOptions);
        }
        await base.OnAfterRenderAsync(firstRender);
    }
}
```

[See the demo here.](https://demos.blazorbootstrap.com/charts/bar-chart#horizontal-bar-chart)

### Stacked bar chart

<img src="https://i.imgur.com/jMIvDFZ.png" alt="Blazor Bootstrap: Bar Chart Component - Stacked bar chart" />

```cshtml {} showLineNumbers
<BarChart @ref="barChart" Height="300" Class="mb-4" />
```

```cs {} showLineNumbers
@code {
    private BarChart barChart = default!;
    private BarChartOptions barChartOptions = default!;
    private ChartData chartData = default!;

    protected override void OnInitialized()
    {
        var colors = ColorBuilder.CategoricalTwelveColors;

        var labels = new List<string> { "Chrome", "Firefox", "Safari", "Edge" };
        var datasets = new List<IChartDataset>();

        var dataset1 = new BarChartDataset()
            {
                Label = "Windows",
                Data = new List<double> { 28000, 8000, 2000, 17000 },
                BackgroundColor = new List<string> { colors[0] },
                BorderColor = new List<string> { colors[0] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset1);

        var dataset2 = new BarChartDataset()
            {
                Label = "macOS",
                Data = new List<double> { 8000, 10000, 14000, 8000 },
                BackgroundColor = new List<string> { colors[1] },
                BorderColor = new List<string> { colors[1] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset2);

        var dataset3 = new BarChartDataset()
            {
                Label = "Other",
                Data = new List<double> { 28000, 10000, 14000, 8000 },
                BackgroundColor = new List<string> { colors[2] },
                BorderColor = new List<string> { colors[2] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset3);

        chartData = new ChartData
            {
                Labels = labels,
                Datasets = datasets
            };

        barChartOptions = new();
        barChartOptions.Responsive = true;
        barChartOptions.Interaction = new Interaction { Mode = InteractionMode.Y };
        barChartOptions.IndexAxis = "y";

        barChartOptions.Scales.X.Title.Text = "Visitors";
        barChartOptions.Scales.X.Title.Display = true;

        barChartOptions.Scales.Y.Title.Text = "Browser";
        barChartOptions.Scales.Y.Title.Display = true;

        barChartOptions.Scales.X.Stacked = true;
        barChartOptions.Scales.Y.Stacked = true;

        barChartOptions.Plugins.Title.Text = "Operating system";
        barChartOptions.Plugins.Title.Display = true;
    }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await barChart.InitializeAsync(chartData, barChartOptions);
        }
        await base.OnAfterRenderAsync(firstRender);
    }
}
```

[See the demo here.](https://demos.blazorbootstrap.com/charts/bar-chart#stacked-bar-chart)

### Locale

By default, the chart is using the default locale of the platform on which it is running. 
In the following example, you will see the chart in the **German** locale (**de_DE**).

<img src="https://i.imgur.com/3qndkPO.png" alt="Blazor Bootstrap: Bar Chart Component - Locale" />

```cshtml {} showLineNumbers
<BarChart @ref="barChart" Height="300" Class="mb-4" />
```

```cs {} showLineNumbers
@code {
    private BarChart barChart = default!;
    private BarChartOptions barChartOptions = default!;
    private ChartData chartData = default!;

    protected override void OnInitialized()
    {
        var colors = ColorBuilder.CategoricalTwelveColors;

        var labels = new List<string> { "Chrome", "Firefox", "Safari", "Edge" };
        var datasets = new List<IChartDataset>();

        var dataset1 = new BarChartDataset()
            {
                Label = "Windows",
                Data = new List<double> { 28000, 8000, 2000, 17000 },
                BackgroundColor = new List<string> { colors[0] },
                BorderColor = new List<string> { colors[0] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset1);

        var dataset2 = new BarChartDataset()
            {
                Label = "macOS",
                Data = new List<double> { 8000, 10000, 14000, 8000 },
                BackgroundColor = new List<string> { colors[1] },
                BorderColor = new List<string> { colors[1] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset2);

        var dataset3 = new BarChartDataset()
            {
                Label = "Other",
                Data = new List<double> { 28000, 10000, 14000, 8000 },
                BackgroundColor = new List<string> { colors[2] },
                BorderColor = new List<string> { colors[2] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset3);

        chartData = new ChartData
            {
                Labels = labels,
                Datasets = datasets
            };

        barChartOptions = new();
        barChartOptions.Locale = "de-DE";
        barChartOptions.Responsive = true;
        barChartOptions.Interaction = new Interaction { Mode = InteractionMode.Y };
        barChartOptions.IndexAxis = "y";

        barChartOptions.Scales.X.Title.Text = "Visitors";
        barChartOptions.Scales.X.Title.Display = true;

        barChartOptions.Scales.Y.Title.Text = "Browser";
        barChartOptions.Scales.Y.Title.Display = true;

        barChartOptions.Scales.X.Stacked = true;
        barChartOptions.Scales.Y.Stacked = true;

        barChartOptions.Plugins.Title.Text = "Operating system";
        barChartOptions.Plugins.Title.Display = true;
    }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await barChart.InitializeAsync(chartData, barChartOptions);
        }
        await base.OnAfterRenderAsync(firstRender);
    }
}
```

[See the demo here.](https://demos.blazorbootstrap.com/charts/bar-chart#locale)

### Data labels

<img src="https://i.imgur.com/em6943w.png" alt="Blazor Bootstrap: Bar Chart Component - Data labels" />

```cshtml {} showLineNumbers
<BarChart @ref="barChart" Height="300" Class="mb-4" />
```

```cs {72} showLineNumbers
@code {
    private BarChart barChart = default!;
    private BarChartOptions barChartOptions = default!;
    private ChartData chartData = default!;

    protected override void OnInitialized()
    {
        var colors = ColorBuilder.CategoricalTwelveColors;

        var labels = new List<string> { "Chrome", "Firefox", "Safari", "Edge" };
        var datasets = new List<IChartDataset>();

        var dataset1 = new BarChartDataset()
            {
                Label = "Windows",
                Data = new List<double> { 28000, 8000, 2000, 17000 },
                BackgroundColor = new List<string> { colors[0] },
                BorderColor = new List<string> { colors[0] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset1);

        var dataset2 = new BarChartDataset()
            {
                Label = "macOS",
                Data = new List<double> { 8000, 10000, 14000, 8000 },
                BackgroundColor = new List<string> { colors[1] },
                BorderColor = new List<string> { colors[1] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset2);

        var dataset3 = new BarChartDataset()
            {
                Label = "Other",
                Data = new List<double> { 28000, 10000, 14000, 8000 },
                BackgroundColor = new List<string> { colors[2] },
                BorderColor = new List<string> { colors[2] },
                BorderWidth = new List<double> { 0 },
            };
        datasets.Add(dataset3);

        chartData = new ChartData
            {
                Labels = labels,
                Datasets = datasets
            };

        barChartOptions = new();
        barChartOptions.Responsive = true;
        barChartOptions.Interaction = new Interaction { Mode = InteractionMode.Y };
        barChartOptions.IndexAxis = "y";

        barChartOptions.Scales.X.Title.Text = "Visitors";
        barChartOptions.Scales.X.Title.Display = true;

        barChartOptions.Scales.Y.Title.Text = "Browser";
        barChartOptions.Scales.Y.Title.Display = true;

        barChartOptions.Scales.X.Stacked = true;
        barChartOptions.Scales.Y.Stacked = true;

        barChartOptions.Plugins.Title.Text = "Operating system";
        barChartOptions.Plugins.Title.Display = true;
    }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            // pass the plugin name to enable the data labels
            await barChart.InitializeAsync(chartData: chartData, chartOptions: barChartOptions, plugins: new string[] { "ChartDataLabels" });
        }
        await base.OnAfterRenderAsync(firstRender);
    }
}
```

[See the demo here.](https://demos.blazorbootstrap.com/charts/bar-chart#data-labels)
