# River Water Quality Analysis in North England (2023–2025)

## Project Overview

This project investigates changes in river water quality across North England between 2023 and 2025. Using water quality monitoring data, the analysis examines annual trends, compares catchments and sub-areas, and explores relationships between selected water quality indicators.

## Research Question

**Did river water quality in North England improve or decline between 2023 and 2025, and which catchments and pollutants drive the change?**

## Project Objectives

- Assess the structure, coverage and quality of the datasets.

- Compare key river water-quality indicators across 2023, 2024 and 2025.

- Compare water quality patterns across the selected catchments and assess how they changed between 2023 and 2025

- Communicate findings, limitations and potential implications through clear tables, visualisations and a reproducible report.

## Project Structure

``` text
WaterQualityAnalysis/
├── README.md
├── Water Quality Analysis Report.qmd
└── Data/
    ├── WaterQuality23.csv
    ├── WaterQuality24.csv
    └── WaterQuality25.csv
```

- README.md: Provides project information, data source details, software requirements, and instructions for reproducing the analysis.
- Water Quality Analysis Report.qmd: Contains the R code, statistical analyses, tables, visualisations, and written interpretation of the results.
- Data/: Contains the three annual water quality datasets used in the project.
- `WaterQuality23.csv` — 2023 water quality data.
- `WaterQuality24.csv` — 2024 water quality data.
- `WaterQuality25.csv` — 2025 water quality data.

The datasets are combined and prepared for analysis. The main analysis focuses on river or running surface water samples and seven selected indicators.

# Water Quality Indicators

The analysis focuses on river or running surface water samples and seven selected water quality indicators. Sampling sites with records across all three years are selected to support comparisons over time. However, this does not guarantee that every site has measurements for every indicator in every year. The analysis examines the following seven indicators:

1.  Nitrate as N
2.  Orthophosphate, reactive as P
3.  Ammoniacal Nitrogen as N
4.  Oxygen, Dissolved, % Saturation
5.  BOD: 5 Day ATU
6.  Temperature of Water
7.  pH

These indicators provide information about nutrient concentrations, oxygen conditions, organic pollution, water temperature, and the acidity or alkalinity of river water.

## Methodology

### 1. Data preparation

The three annual datasets are imported and combined into one dataset. Relevant fields are prepared for analysis, including sampling-site identifiers, year, sample material type, indicator, measurement unit, sampling date, and numerical result.

### 2. Data filtering and cleaning

The analysis retains river or running surface water samples, the seven selected indicators, and sites with records across all three study years. Coded or text-only results and rows without a usable numeric result are excluded from the numerical analysis.

Results reported below a detection limit are flagged and assigned a value based on half the reported limit. This is an estimation used to enable numerical analysis; it does not represent the exact measured concentration, so findings involving censored values particularly ammoniacal nitrogen should be interpreted cautiously.

### 3. Descriptive statistics

Annual summary statistics, including the median and first and third quartiles (Q1 and Q3), are calculated for each indicator to describe the centre and spread of the measurements.

### Water Quality Indicators Summary
![Water Quality Indicators Summary](<images/Indicators summary.png>)

### 4. Visualisation

The report uses visualisations to explore annual distributions, seasonal patterns, spatial patterns, catchment differences, and relationships between selected indicators. Some distribution plots use a logarithmic scale and include positive measurements only, where required by the scale.

### 5. Statistical testing

Kruskal–Wallis tests are used to assess whether measurements differ between years for each indicator. P-values are adjusted for multiple testing, and effect sizes are calculated to help distinguish statistical significance from the magnitude of observed differences. Dunn’s post-hoc tests are then used to compare pairs of years for indicators with significant overall results.

These tests treat observations as independent. Because sampling sites may be measured repeatedly, this assumption may not always hold; the report discusses this as a limitation. Statistical significance alone does not establish that a change is environmentally important.

### Statistical Tests
![Statistical Testing](<images/Statistical testing.png>)

### 6. Catchment and sub-area comparison

Median measurements are compared across selected sub-areas, including changes between 2023 and 2025. Sub-areas are included in relevant comparisons only when they meet the minimum sampling-site threshold specified in the analysis. These comparisons are descriptive and may reflect differences in sampling coverage as well as environmental conditions.

### Catchment and Sub-area Comparison
![Catchment and Sub-area Comparison](<images/Catchment and sub-area comparison.png>)

### 7. Correlation analysis

Spearman correlation analysis is used to explore associations between selected indicators. Correlations are interpreted as associations, not evidence that one indicator causes a change in another.

### Correlation Analysis
![Correlation Analysis](<images/Correlation analysis.png>)


## Tools and Technologies

The project uses:

- **R** for data preparation, statistical analysis, and visualisation.
- **Quarto** for preparing and rendering the analytical report.
- **RStudio** as the development environment.
- **tidyverse** and **ggplot2** for data manipulation and visualisation.
- **rstatix** for statistical tests and effect-size calculations.
- **knitr** for formatting tables in the report.
- **scales** for formatting plot axes and labels.

## How to Run the Project

Follow the steps below to run the water quality analysis in RStudio.

### Prerequisites

Ensure that the following software is installed on your computer:

- R: Required to execute the analysis code.

- RStudio: Used to open and work with the Quarto report.

- Quarto: Required to render the report.

### Step 1: Set Up the Project Files

Ensure that your project folder contains the Quarto report, the README file, and a Data/ directory containing the three original CSV files:

- Data/WaterQuality23.csv

- Data/WaterQuality24.csv

- Data/WaterQuality25.csv

Maintain this folder structure because the analysis uses relative file paths to access the datasets.

### Step 2: Install the Required R Packages

Open RStudio and run the following command in the R console to install the main packages used in the analysis:

```{r}
install.packages(c("tidyverse", "scales", "rstatix", "knitr"))
```

These packages support data manipulation, visualisation, statistical testing, and table formatting. Install any additional packages required by the report if necessary.

### Step 3: Open the Quarto Report

Open Water Quality Analysis Report.qmd in RStudio.

### Step 4: Run the Analysis

In RStudio, click Render at the top of the Quarto editor to execute the code and generate the report.

Alternatively, run the following command in the RStudio Console from the project directory:

```{r}
quarto::quarto_render("Water Quality Analysis Report.qmd")
```

### Step 5: Review the Output

After rendering, check that the report contains the expected tables, figures, descriptive statistics, correlation analysis, and statistical test results.

If an error occurs, check that the required packages are installed, the CSV filenames are correct, and the Data/ directory is in the expected location.

### Reproducibility

The analysis uses the three annual water quality datasets provided for the project and the R code contained in the Quarto report. Reproducing the analysis requires the same input files, the correct directory structure, and the necessary software and R packages.

The exact package requirements are determined by the functions used in the report. If rendering reports a missing package, install it and render the report again.

## Key Findings

The analysis identified the following key findings between 2023 and 2025:

- Nitrate: Median concentration decreased from 1.49 mg/L in 2023 to 0.843 mg/L in 2025.

- Orthophosphate: Median concentration decreased from 0.021 mg/L in 2023 to 0.014 mg/L in 2025.

- Ammoniacal nitrogen: Median concentration remained stable at 0.015 mg/L across all three years.

- Biochemical oxygen demand (BOD): Median concentration remained at 1.5 mg/L, with no statistically significant difference between years.

- Dissolved oxygen saturation: Median increased slightly from 98.8% in 2023 to 99.4% in 2025.

- pH: Median increased slightly from 7.97 to 8.03.

- Water temperature: Median decreased from 10°C in 2023 to 9.3°C in 2025, after reaching 8.9°C in 2024.

- Statistical significance: Six of the seven indicators showed statistically significant differences across years, but all effect sizes were small.

- Geographical variation: Wear & Tees generally recorded higher median nutrient concentrations than Northumberland & Tyne.

These findings should be confirmed against the final rendered report, particularly after the final data filtering. Catchment-specific percentage changes should be interpreted alongside sampling coverage and the treatment of results below detection limits.

## Limitations

- Sampling coverage: Although the analysis includes sites with records across all three years, the number of observations may vary between years and sites, potentially affecting comparisons.

- Repeated measurements: The Kruskal–Wallis test assumes independent observations, but repeated measurements at the same sites may violate this assumption.

- Detection limits: Ammoniacal nitrogen results include substituted values for measurements below detection limits. The proportion of censored results increased from 22.7% in 2023 to 29.7% in 2025, which may affect the interpretation of trends.

- Statistical significance: Six indicators showed statistically significant differences between years, but all reported effect sizes were small.

- Correlation and causation: Associations between indicators do not establish the causes of observed changes.

- Geographical coverage: The catchment comparison focused on Northumberland & Tyne and Wear & Tees and three nutrient indicators, so the findings may not represent all catchments or aspects of river water quality.

## Conclusion

River water quality across North England showed some signs of improvement between 2023 and 2025, particularly through reductions in median nitrate and orthophosphate concentrations and a slight increase in dissolved oxygen saturation. However, the small effect sizes and limited changes in other indicators mean that an overall improvement across all aspects of water quality cannot be established.

Catchment comparisons showed that Wear & Tees recorded the largest reductions in orthophosphate (52.5%) and ammoniacal nitrogen (54.5%), while Northumberland & Tyne recorded the larger reduction in nitrate (47.8%, compared with 9.5% in Wear & Tees). These findings highlight differences in how water quality changed across the two catchments and identify nutrient concentrations that warrant continued monitoring.

## Recommendations

Based on the findings, the following actions are recommended:

- Prioritise monitoring in Wear & Tees: Investigate the generally higher nutrient concentrations to identify locations that may require closer monitoring.

- Continue monitoring nutrient levels: Track nitrate and orthophosphate concentrations to determine whether the observed reductions persist.

- Review below-detection-limit results: Consider how the treatment of censored ammoniacal nitrogen measurements affects the interpretation of trends.

- Investigate relationships between indicators: Explore associations between nutrient concentrations and dissolved oxygen without assuming causation.

- Improve sampling consistency: Promote more consistent monitoring across sites and years to strengthen comparisons over time.

These recommendations should be considered alongside the study's limitations. Further evidence is required before specific pollution sources or causes can be established.


## Author

**Wisdom Ogbeche**

[GitHub Profile](https://github.com/Gogathebrains4)
