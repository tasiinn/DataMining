# EV Charging Data Analysis

<!-- Project Shields -->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Issues][issues-shield]][issues-url]
[![License][license-shield]][license-url]

<br />
<div align="center">
  <h3 align="center">EV Charging Data Analysis</h3>

  <p align="center">
    An end-to-end data analysis project exploring EV charging behavior, energy consumption, and infrastructure usage patterns in municipal parking lots and garages.
    <br />
    Statistical analysis, feature engineering, and visualization were used to uncover temporal usage trends, location-based differences, and infrastructure planning insights.
  </p>
</div>

---

## Table of Contents

- [About The Project](#about-the-project)
- [Project Goals](#project-goals)
- [Dataset](#dataset)
- [Why This Project Matters](#why-this-project-matters)
- [Tech Stack](#tech-stack)
- [Why Each Tool Was Used](#why-each-tool-was-used)
- [Methodology](#methodology)
- [Key Analyses Performed](#key-analyses-performed)
- [Key Findings](#key-findings)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Future Improvements](#future-improvements)
- [Acknowledgments](#acknowledgments)

---

## About The Project

This project analyzes electric vehicle charging session data from **NYC municipal parking lots and garages** to better understand how charging infrastructure is being used in practice.

The workflow covers the full analytics pipeline:
- cleaning raw operational data,
- engineering time- and location-based features,
- exploring usage distributions,
- running inferential statistical tests,
- and translating findings into infrastructure and planning insights.

The final cleaned dataset contains **199,035 charging sessions** across **8 locations** and spans **July 31, 2021 to November 5, 2025**.

This project was developed as a course-based data analysis report and presentation, with a focus on producing both statistically grounded findings and stakeholder-friendly visual explanations.

---

## Project Goals

The main goals of this project were to:

- understand when EV charging demand is highest,
- compare charging behavior across weekdays, weekends, and locations,
- analyze energy delivery and charging duration distributions,
- study differences between charger manufacturers,
- and generate insights that could support **urban planning, charger deployment, maintenance decisions, and grid-aware operations**.

---

## Dataset

The project uses EV charging session data published through **NYC Open Data** for municipal parking lots and garages.

### Data includes
- session date,
- connected and disconnected time,
- station name,
- location name,
- connector ID,
- anonymized user identifier (`ID Tag`),
- charge duration,
- connected duration,
- energy provided in kWh,
- session status,
- engineered weekday/weekend/holiday indicators,
- inferred charger manufacturer.

### Final processed dataset
- **Rows:** 199,035
- **Columns:** 15
- **Locations:** 8
- **Session types:** PAID and ROAMING
- **Manufacturers identified:** EVB, BTC Power, EVX, Fast Charger (Multiple), Unknown, Other

### Data preparation highlights
- removed irrelevant columns such as driver-level identifiers and invalidity fields,
- removed disconnected or incomplete records,
- standardized location names with inconsistent spellings/abbreviations,
- converted duration fields to numeric values,
- engineered temporal features such as weekday, weekend, and holiday flags,
- inferred charger manufacturer from station naming conventions.

---

## Why This Project Matters

EV adoption is increasing, but infrastructure planning cannot rely on intuition alone. Real charging-session data helps answer practical questions such as:

- When do chargers experience peak demand?
- Do charging patterns change on weekends?
- Which locations consume the most energy?
- Are some charger brands associated with longer or more variable sessions?
- Where should future investment or maintenance effort be prioritized?

By answering these questions, the project connects raw operational data to decisions that matter for **cities, utilities, planners, and EV service operators**.

---

## Tech Stack

- **R**
- **R Markdown**
- **tidyverse**
- **dplyr**
- **ggplot2**
- **lubridate**
- **knitr**
- **kableExtra**
- **psych**
- **car**
- **corrplot**
- **gridExtra**
- **FSA** (for post-hoc nonparametric testing)
- **LaTeX / PDF output**
- **PowerPoint** (for presenting findings)

---

## Why Each Tool Was Used

### R
R was the core language used for the project because it is strong for statistical computing, exploratory data analysis, and reproducible research.

### R Markdown
R Markdown was used to combine code, analysis, plots, and written interpretation in a single reproducible document. This made the project easier to organize and present as a formal report.

### tidyverse
The `tidyverse` ecosystem simplified the full workflow, especially for cleaning, transforming, reshaping, and summarizing the data.

### dplyr
`dplyr` was used for filtering rows, selecting columns, creating engineered features, grouping data, and computing summary statistics efficiently.

### ggplot2
`ggplot2` was used to build the project's visualizations, including bar charts, boxplots, histograms, Q-Q plots, and heatmaps. It was chosen because it provides flexible and publication-quality graphics.

### lubridate
`lubridate` made it easier to work with dates and times, especially when extracting weekdays and hour-of-day usage patterns.

### knitr and kableExtra
These packages were used to generate cleaner summary tables for the report, improving readability and presentation quality.

### psych
`psych` supported descriptive statistical analysis and helped summarize distribution-level behavior.

### car
The `car` package was used for statistical diagnostics such as Q-Q plot generation and distribution checking.

### corrplot
`corrplot` supports correlation-based visual analysis and was included to help explore relationships between numerical variables.

### gridExtra
`gridExtra` is useful for arranging multiple plots and outputs into organized report layouts.

### FSA
`FSA` was used for post-hoc Dunn testing after significant Kruskal-Wallis results, allowing pairwise comparison across locations when nonparametric assumptions were needed.

### LaTeX / PDF output
The final report was rendered to PDF to produce a polished, shareable deliverable suitable for class submission and portfolio use.

### PowerPoint
Presentation slides were used to convert the technical analysis into a more concise, stakeholder-friendly summary of findings and implications.

---

## Methodology

### 1. Data Cleaning
The raw data was cleaned by removing irrelevant columns, filtering out unusable session records, handling missing values, and standardizing inconsistent location labels.

### 2. Feature Engineering
Additional variables were created to support richer analysis:
- weekday,
- weekend flag,
- holiday flag for 2024,
- manufacturer label inferred from station names,
- hour-of-day fields derived from connection and disconnection times.

### 3. Descriptive Analysis
The project explored distributions of:
- session status,
- weekday usage,
- weekend vs weekday activity,
- locations,
- charging start and end times,
- energy delivered,
- charging duration,
- and manufacturer-level differences.

### 4. Statistical Inference
To move beyond visual description, the project applied inferential testing:
- **Wilcoxon rank-sum tests** for weekday vs weekend comparisons,
- **Kruskal-Wallis tests** for location-based energy differences,
- **Chi-square tests** for dependence between location and energy category,
- **proportion tests** for weekend usage behavior,
- and **variance/F-tests** for comparing dispersion across groups.

### 5. Interpretation for Real-World Use
Instead of stopping at charts and p-values, the analysis connected the statistical findings to infrastructure planning, pricing, maintenance, and capacity strategy.

---

## Key Analyses Performed

- Charging session distribution by **session status**
- Usage distribution by **day of week**
- **Weekday vs weekend** usage comparison
- Charging **start-time and end-time** hotspot analysis
- **Boxplots by manufacturer** for energy and charge duration
- Measures of center and dispersion for major numerical fields
- **Total and average energy** by location and weekday
- **Heatmaps** of charging demand by weekday and hour
- **Weekend vs weekday inferential testing**
- **Location-based inferential testing** using nonparametric methods
- **Proportion inference** for weekend charging behavior
- **Variance comparison** across usage types and time groups

---

## Key Findings

### 1. Usage is concentrated on weekdays, but weekends are still substantial
About **70.83%** of sessions occurred on weekdays and **29.17%** on weekends, showing that weekend demand is large enough to matter operationally.

### 2. Weekend charging behavior differs significantly from weekday behavior
Wilcoxon tests showed statistically significant differences in both **energy provided** and **charge duration** between weekends and weekdays.

### 3. Demand peaks during weekday afternoons and evenings
Charging activity was highest during late-day weekday periods, which likely reflects commuter and after-work charging behavior.

### 4. Location matters
Energy usage patterns varied significantly across top locations. Statistical testing showed that location and energy category were not independent, meaning where a charger is located strongly affects how it is used.

### 5. Court Square stood out as a high-usage site
The project presentation identified **Court Square Municipal Parking Garage** as one of the strongest locations in terms of energy consumption and weekend usage intensity.

### 6. Manufacturer-level differences are operationally relevant
Although median energy output was similar across manufacturers, some charger groups showed much larger variation and more extreme outliers in both energy delivery and charge duration.

### 7. The data is highly skewed
Both `Energy Provided (kWh)` and especially `Charge Duration (min)` were right-skewed, which justified the use of nonparametric tests in several parts of the analysis.

---

## Project Structure

```bash
EV-Charging-Analysis/
├── README.md
├── EV_data_analysis.rmd          # Main R Markdown analysis file
├── EV_data_analysis.pdf          # Full written report
├── EV_data_processed.csv         # Final cleaned dataset used for analysis
├── EV_project_First_Presentation.pptx   # Presentation summarizing findings
└── assets/                       # Optional folder for screenshots/plots if added later
```

---

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/zubaerchowdhury/NYC-EV-Charging-Analysis.git
cd your-repo-name
```

### 2. Install required R packages
```r
packages <- c(
  "tidyverse", "knitr", "kableExtra", "corrplot", "psych", "car",
  "moments", "gridExtra", "ggplot2", "dplyr", "lubridate", "FSA"
)
install.packages(setdiff(packages, rownames(installed.packages())))
```

### 3. Update the data path if needed
In the R Markdown file, make sure the input CSV path matches your local project structure.

### 4. Render the report
```r
rmarkdown::render("EV_data_analysis.rmd")
```

---

## Future Improvements

- build predictive models for charger demand forecasting,
- analyze holiday effects across multiple years,
- incorporate weather and event data,
- study location-level capacity utilization over time,
- create an interactive dashboard for operational monitoring,
- explore user segmentation if privacy-safe demographic or behavioral metadata becomes available.

---

## Acknowledgments

- **NYC Open Data** for publishing EV charging session data
- Course instructors and peers who contributed to the academic project workflow
- The open-source R ecosystem for making the full analysis pipeline reproducible and presentation-ready

---

## Notes for GitHub Showcase

To make this repository stronger as a portfolio project, consider adding:
- screenshots of the best charts in an `assets/` folder,
- a short section titled **Business Impact** or **Infrastructure Insights**,
- and a few highlighted visuals near the top of the README for quicker recruiter-friendly scanning.

---

<!-- MARKDOWN LINKS & IMAGES -->
[contributors-shield]: https://img.shields.io/github/contributors/zubaerchowdhury/NYC-EV-Charging-Analysis.svg?style=for-the-badge
[contributors-url]: https://github.com/zubaerchowdhury/NYC-EV-Charging-Analysis/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/zubaerchowdhury/NYC-EV-Charging-Analysis.svg?style=for-the-badge
[forks-url]: https://github.com/zubaerchowdhury/NYC-EV-Charging-Analysis/network/members
[issues-shield]: https://img.shields.io/github/issues/zubaerchowdhury/NYC-EV-Charging-Analysis.svg?style=for-the-badge
[issues-url]: https://github.com/zubaerchowdhury/NYC-EV-Charging-Analysis/issues
[license-shield]: https://img.shields.io/github/license/zubaerchowdhury/NYC-EV-Charging-Analysis.svg?style=for-the-badge
[license-url]: https://github.com/zubaerchowdhury/NYC-EV-Charging-Analysis/blob/main/LICENSE
