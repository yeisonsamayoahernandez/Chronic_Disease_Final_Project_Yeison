# Diabetes Prevalence in U.S. Adults: Men vs. Women Across States

Final project for the UCSF PROPEL Introduction to R and Statistics course.

## Research question

In 2022, did adult men and women in U.S. states have different diabetes prevalence?

As a follow-up, I also looked at whether states with higher adult obesity have higher adult diabetes.

## Dataset

**U.S. Chronic Disease Indicators (CDI)** from the CDC, downloaded from Data.gov:
https://catalog.data.gov/dataset/u-s-chronic-disease-indicators

The CDI combines state-level estimates for many chronic disease topics from sources like BRFSS, vital statistics, and others. Each row is a summary estimate for a state, year, and group (for example, the percent of women in California with diabetes). It's public data with no individual-level or protected health information.

I compressed the original file (`export.csv`, 127 MB) and is is stored as gzip-compressed, `data/export.csv.gz` (about 9 MB) so it fits under GitHub's 100 MB file limit.

For the analysis I kept only:
- "Diabetes among adults" and "Obesity among adults" (BRFSS)
- Year 2022
- Age-adjusted prevalence (%)
- The 50 states + DC (national total and territories removed)

## Methods

- **Descriptive:** summary statistics with `group_by()` and `summarize()`, a bar plot, a histogram, and a paired plot comparing men and women within each state
- **Inferential:** the Wilcoxon signed-rank test (paired, men vs. women within each state). It was used because the paired differences were not normally distributed (Shapiro-Wilk test). A paired t-test is included as a check.
- **Regression:** simple linear regression of state diabetes prevalence on state obesity prevalence, with diagnostic plots

## Main results

- Men had higher diabetes prevalence than women in 46 of 51 locations, by about 1.2 percentage points on average (Wilcoxon signed-rank p < 0.001).
- Each 1-point increase in state obesity prevalence went with about a 0.3-point increase in diabetes prevalence (R² = 0.45).

## Files

| `Chronic_Disease_Final_Project.Rproj` | RStudio project file
| `Final_Analysis.Rmd` | All code, plots, and written analysis |
| `Final_Analysis.html` | Knitted version of the notebook |
| `data/export.csv.gz` | Original CDI dataset (compressed) |
| `README.md` | This file |
| `prompts.txt` | AI prompts used while making the project |

## R packages

- `tidyverse` (includes `dplyr`, `tidyr`, `ggplot2`, and `readr`)
- `rmarkdown` and `knitr` (for knitting; these come with RStudio)

## How to run

1. Download or clone this folder.
2. Double-click `Chronic_Disease_Final_Project.Rproj` to open it in RStudio. This sets the working directory to the project folder, so the relative file paths work.
3. Open `Final_Analysis.Rmd`.
4. Click **Knit**, or run the chunks one at a time.

Built with R 4.6.1 and tidyverse 2.0.0.
