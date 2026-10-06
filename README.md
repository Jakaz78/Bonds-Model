# Econometric Model of Polish 10-Year Bond Yields

An R Markdown report that builds a linear regression model explaining monthly changes in the yield of 10-year Polish government bonds (`CLOSE`) using market and macroeconomic data (Feb 2000 – Mar 2025, 302 observations).

Rendered report (in Polish): [`Sprawozdanie.pdf`](Sprawozdanie.pdf)

## Methodology

1. Linear interpolation of missing values, chronological 80/20 train/test split.
2. Preliminary variable screening by correlation with `CLOSE` (thresholds 0.3–0.75) and log transformation.
3. Stationarity tests (ADF + KPSS) and differencing.
4. Variable selection with Hellwig's integral information capacity method.
5. OLS estimation and diagnostics: normality, autocorrelation, heteroskedasticity, VIF, parameter stability (Chow, CUSUM), RESET, runs test, catalysis and coincidence checks.
6. Ex post forecast on the test set (MAE, RMSE) compared with a naive forecast.

## Main results

- Selected predictors: changes in log prices of gold (`XAUUSD`), `WIG20` and oil (`OIL`).
- The model is significant overall but weak: R² ≈ 0.14.
- All tested assumptions hold except normality of residuals.
- On the test set the model is only marginally better than the naive forecast.

## Repository structure

```
Sprawozdanie.Rmd     # all code and analysis text
Sprawozdanie.pdf     # rendered report
data/data.xlsx       # monthly data (source: Stooq)
install_packages.R   # installs required R packages
```

## Usage

Requirements: R (≥ 4.1) and a LaTeX distribution with XeLaTeX (e.g. TinyTeX).

```r
source("install_packages.R")
rmarkdown::render("Sprawozdanie.Rmd")
```

Analysis parameters (significance level, split ratio, correlation thresholds, max differencing order) are defined at the top of `Sprawozdanie.Rmd`. All numbers in the report are computed from the data at knit time.

## Data

Data comes from [Stooq](https://stooq.pl). Check the site's terms before redistributing it.
