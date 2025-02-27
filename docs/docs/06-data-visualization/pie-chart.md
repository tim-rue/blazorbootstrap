﻿---
title: Blazor Pie Chart Components
description: A Blazor Bootstrap pie chart component is a circular chart that shows the proportional values of different categories.
image: https://i.imgur.com/dDpIuzk.png

sidebar_label: Pie Chart
sidebar_position: 4
---

A Blazor Bootstrap pie chart component is a circular chart that shows the proportional values of different categories.

<img src="https://i.imgur.com/dDpIuzk.png" alt="Blazor Chart Component - Blazor Pie Chart" />

## Parameters

| Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:--|
| Height | int | | | Gets or sets chart height. | 1.0.0 |
| Width | int | | | Get or sets chart width. | 1.0.0 |

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
| Labels | `List<string>` | null | ✔️ | Gets or sets the Labels. | 1.0.0 |
| Datasets | `List<IChartDataset>` | null | ✔️ | Gets or sets the Datasets. | 1.0.0 |

## PieChartDataset Members

:::info
**PieChartDataset** implements **IChartDataset**.
:::

| Property Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:-|
| BackgroundColor | `List<string>` | null | | Get or sets the BackgroundColor. | 1.0.0 |
| BorderColor | `List<string>` | null | | Get or sets the BorderColor. | 1.0.0 |
| BorderWidth | `List<double>` | null | | Get or sets the BorderWidth. | 1.0.0 |
| Clip | string | null | | How to clip relative to chartArea. Positive value allows overflow, negative value clips that many pixels inside chartArea. 0 = clip at chartArea. Clipping can also be configured per side: clip: {left: 5, top: false, right: -2, bottom: 0} | 1.0.0 |
| Data | `List<double>` | null | | Get or sets the Data. | 1.0.0 |
| Datalabels | `PieChartDatasetDataLabels` | | | Get or sets the data labels | | 1.10.2 |
| Hidden | bool | false | | Configures the visibility state of the dataset. Set it to true, to hide the dataset from the chart. | 1.0.0 |
| HoverBackgroundColor | `List<string>` | null | ✔️ | Get or sets the HoverBackgroundColor. | 1.0.0 |
| HoverBorderColor | `List<string>` | null | ✔️ | Get or sets the HoverBorderColor. | 1.0.0 |
| HoverBorderWidth | `List<double>` | null | ✔️ | Get or sets the HoverBorderWidth. | 1.0.0 |
| Type | string | null | ✔️ | Get or sets the chart type. | 1.0.0 |

## PieChartDatasetDataLabels Members

| Property Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:--|
| Anchor | `string?` | `center` | | Gets or sets the anchor. | 1.10.2 |
| BorderWidth | `double?` | `2` | | Gets or sets the border width. | 1.10.2 |

## PieChartOptions Members

:::info
**PieChartOptions** implements **ChartOptions**.
:::

| Property Name | Type | Default | Required | Description | Added Version |
|:--|:--|:--|:--|:--|:--|
| Locale | `string?` | | | Gets or sets the locale. By default, the chart is using the default locale of the platform which is running on. | 1.10.0 |
| Plugins | `PieChartPlugins` | | | Gets or sets the Plugins. | 1.10.2 |
| Responsive | bool | false | | Gets or sets the Responsive. | 1.0.0 |

## Examples

### Prerequisites

Refer to the [getting started guide](/getting-started/blazor-webassembly) for setting up charts.

### How it works

In the following example, a categorical 12-color palette is used.

:::tip
For data visualization, you can use the predefined palettes `ColorBuilder.CategoricalTwelveColors` for a 12-color palette and `ColorBuilder.CategoricalSixColors` for a 6-color palette. 
These palettes offer a range of distinct and visually appealing colors that can be applied to represent different categories or data elements in your visualizations.
:::

<img src="https://i.imgur.com/ieBupT2.png" alt="Blazor Bootstrap: Pie Chart Component - How it works" />

```cshtml {} showLineNumbers
<PieChart @ref="pieChart" Width="500" Class="mb-5" />

<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await RandomizeAsync()"> Randomize </Button>
<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await AddDatasetAsync()"> Add Dataset </Button>
<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await AddDataAsync()">Add Data</Button>
```

```cs {} showLineNumbers
@code {
    private PieChart pieChart = default!;
    private PieChartOptions pieChartOptions = default!;
    private ChartData chartData = default!;
    private string[]? backgroundColors;

    private int datasetsCount = 0;
    private int dataLabelsCount = 0;

    private Random random = new();

    protected override void OnInitialized()
    {
        backgroundColors = ColorBuilder.CategoricalTwelveColors;
        chartData = new ChartData { Labels = GetDefaultDataLabels(4), Datasets = GetDefaultDataSets(1) };

        pieChartOptions = new();
        pieChartOptions.Responsive = true;
        pieChartOptions.Plugins.Title.Text = "2022 - Sales";
        pieChartOptions.Plugins.Title.Display = true;
    }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await pieChart.InitializeAsync(chartData, pieChartOptions);
        }
        await base.OnAfterRenderAsync(firstRender);
    }

    private async Task RandomizeAsync()
    {
        if (chartData is null || chartData.Datasets is null || !chartData.Datasets.Any()) return;

        var newDatasets = new List<IChartDataset>();

        foreach (var dataset in chartData.Datasets)
        {
            if (dataset is PieChartDataset pieChartDataset
                && pieChartDataset is not null
                && pieChartDataset.Data is not null)
            {
                var count = pieChartDataset.Data.Count;

                var newData = new List<double>();
                for (var i = 0; i < count; i++)
                {
                    newData.Add(random.Next(0, 100));
                }

                pieChartDataset.Data = newData;
                newDatasets.Add(pieChartDataset);
            }
        }

        chartData.Datasets = newDatasets;

        await pieChart.UpdateAsync(chartData, pieChartOptions);
    }

    private async Task AddDatasetAsync()
    {
        if (chartData is null || chartData.Datasets is null) return;

        var chartDataset = GetRandomPieChartDataset();
        chartData = await pieChart.AddDatasetAsync(chartData, chartDataset, pieChartOptions);
    }

    private async Task AddDataAsync()
    {
        if (dataLabelsCount >= 12)
            return;

        if (chartData is null || chartData.Datasets is null)
            return;

        var data = new List<IChartDatasetData>();
        foreach (var dataset in chartData.Datasets)
        {
            if (dataset is PieChartDataset pieChartDataset)
                data.Add(new PieChartDatasetData(pieChartDataset.Label, random.Next(0, 100), backgroundColors![dataLabelsCount]));
        }

        chartData = await pieChart.AddDataAsync(chartData, GetNextDataLabel(), data);

        dataLabelsCount += 1;
    }

    #region Data Preparation

    private List<IChartDataset> GetDefaultDataSets(int numberOfDatasets)
    {
        var datasets = new List<IChartDataset>();

        for (var index = 0; index < numberOfDatasets; index++)
        {
            datasets.Add(GetRandomPieChartDataset());
        }

        return datasets;
    }

    private PieChartDataset GetRandomPieChartDataset()
    {
        datasetsCount += 1;
        return new() { Label = $"Team {datasetsCount}", Data = GetRandomData(), BackgroundColor = GetRandomBackgroundColors() };
    }

    private List<double> GetRandomData()
    {
        var data = new List<double>();
        for (var index = 0; index < dataLabelsCount; index++)
        {
            data.Add(random.Next(0, 100));
        }

        return data;
    }

    private List<string> GetRandomBackgroundColors()
    {
        var colors = new List<string>();
        for (var index = 0; index < dataLabelsCount; index++)
        {
            colors.Add(backgroundColors![index]);
        }

        return colors;
    }

    private List<string> GetDefaultDataLabels(int numberOfLabels)
    {
        var labels = new List<string>();
        for (var index = 0; index < numberOfLabels; index++)
        {
            labels.Add(GetNextDataLabel());
            dataLabelsCount += 1;
        }

        return labels;
    }

    private string GetNextDataLabel() => $"Product {dataLabelsCount + 1}";

    private string GetNextDataBackgrounfColor() => backgroundColors![dataLabelsCount];

    #endregion  Data Preparation
}
```

[See the demo here.](https://demos.blazorbootstrap.com/charts/pie-chart#how-it-works)

### Data labels

<img src="https://i.imgur.com/dDpIuzk.png" alt="Blazor Bootstrap: Pie Chart Component - Data labels" />

```cshtml {} showLineNumbers
<PieChart @ref="pieChart" Width="500" Class="mb-5" />

<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await RandomizeAsync()"> Randomize </Button>
<Button Type="ButtonType.Button" Color="ButtonColor.Primary" Size="Size.Small" @onclick="async () => await AddDataAsync()">Add Data</Button>
```

```cs {28,94,96,98} showLineNumbers
@code {
    private PieChart pieChart = default!;
    private PieChartOptions pieChartOptions = default!;
    private ChartData chartData = default!;
    private string[]? backgroundColors;

    private int datasetsCount = 0;
    private int dataLabelsCount = 0;

    private Random random = new();

    protected override void OnInitialized()
    {
        backgroundColors = ColorBuilder.CategoricalTwelveColors;
        chartData = new ChartData { Labels = GetDefaultDataLabels(4), Datasets = GetDefaultDataSets(3) };

        pieChartOptions = new();
        pieChartOptions.Responsive = true;
        pieChartOptions.Plugins.Title.Text = "2022 - Sales";
        pieChartOptions.Plugins.Title.Display = true;
    }

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            // pass the plugin name to enable the data labels
            await pieChart.InitializeAsync(chartData: chartData, chartOptions: pieChartOptions, plugins: new string[] { "ChartDataLabels" });
        }
        await base.OnAfterRenderAsync(firstRender);
    }

    private async Task RandomizeAsync()
    {
        if (chartData is null || chartData.Datasets is null || !chartData.Datasets.Any()) return;

        var newDatasets = new List<IChartDataset>();

        foreach (var dataset in chartData.Datasets)
        {
            if (dataset is PieChartDataset pieChartDataset
                && pieChartDataset is not null
                && pieChartDataset.Data is not null)
            {
                var count = pieChartDataset.Data.Count;

                var newData = new List<double>();
                for (var i = 0; i < count; i++)
                {
                    newData.Add(random.Next(0, 100));
                }

                pieChartDataset.Data = newData;
                newDatasets.Add(pieChartDataset);
            }
        }

        chartData.Datasets = newDatasets;

        await pieChart.UpdateAsync(chartData, pieChartOptions);
    }

    private async Task AddDataAsync()
    {
        if (dataLabelsCount >= 12)
            return;

        if (chartData is null || chartData.Datasets is null)
            return;

        var data = new List<IChartDatasetData>();
        foreach (var dataset in chartData.Datasets)
        {
            if (dataset is PieChartDataset pieChartDataset)
                data.Add(new PieChartDatasetData(pieChartDataset.Label, random.Next(0, 100), backgroundColors![dataLabelsCount]));
        }

        chartData = await pieChart.AddDataAsync(chartData, GetNextDataLabel(), data);

        dataLabelsCount += 1;
    }

    #region Data Preparation

    private List<IChartDataset> GetDefaultDataSets(int numberOfDatasets)
    {
        var datasets = new List<IChartDataset>();

        for (var index = 0; index < numberOfDatasets; index++)
        {
            var dataset = GetRandomPieChartDataset();

            if (index == 0)
                dataset.Datalabels.Anchor = "end";
            else if (index == numberOfDatasets - 1)
                dataset.Datalabels.Anchor = "end";
            else
                dataset.Datalabels.Anchor = "center";

            datasets.Add(dataset);
        }

        return datasets;
    }

    private PieChartDataset GetRandomPieChartDataset()
    {
        datasetsCount += 1;
        return new() { Label = $"Team {datasetsCount}", Data = GetRandomData(), BackgroundColor = GetRandomBackgroundColors() };
    }

    private List<double> GetRandomData()
    {
        var data = new List<double>();
        for (var index = 0; index < dataLabelsCount; index++)
        {
            data.Add(random.Next(0, 100));
        }

        return data;
    }

    private List<string> GetRandomBackgroundColors()
    {
        var colors = new List<string>();
        for (var index = 0; index < dataLabelsCount; index++)
        {
            colors.Add(backgroundColors![index]);
        }

        return colors;
    }

    private List<string> GetDefaultDataLabels(int numberOfLabels)
    {
        var labels = new List<string>();
        for (var index = 0; index < numberOfLabels; index++)
        {
            labels.Add(GetNextDataLabel());
            dataLabelsCount += 1;
        }

        return labels;
    }

    private string GetNextDataLabel() => $"Product {dataLabelsCount + 1}";

    private string GetNextDataBackgrounfColor() => backgroundColors![dataLabelsCount];

    #endregion  Data Preparation
}
```

[See the demo here.](https://demos.blazorbootstrap.com/charts/pie-chart#data-labels)
