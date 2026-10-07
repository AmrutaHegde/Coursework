# Does It Rain More in Seattle than in San Francisco? A Precipitation Comparison, 2018 to 2022

## Project Overview

Seattle is known as a rainy city, but San Francisco is also a wet Pacific Coast city. This project asks a simple question: **does it rain more in Seattle than in San Francisco?** It compares the two cities in three ways: how much precipitation falls on an average day, how often any precipitation occurs, and whether the difference holds in every month and every year.

The analysis uses NOAA daily precipitation records for one weather station in each city, covering January 1, 2018 to December 31, 2022.

**Key finding:** Yes. Seattle averaged about 0.113 inches of precipitation per day versus 0.044 in San Francisco (about 2.6 times as much), and precipitation was recorded on about 55% of days in Seattle versus 15% in San Francisco. Seattle was wetter in every year and in every month of the year.

**Key techniques:** data inspection and cleaning, date alignment, missing-value analysis and imputation, tidy data reshaping, exploratory visualization, and hypothesis testing.

---

## Project Structure

```
├── code/
│   └── seattle_vs_sf_rain_analysis.ipynb   # Data cleaning and analysis notebook
├── data/
│   ├── seattle_rain.csv                    # Raw Seattle data
│   ├── sf_rain.csv                         # Raw San Francisco data
│   └── clean_seattle_sf_weather.csv        # Clean, tidy data used for the analysis
├── reports/                                # Written report and figures
├── requirements.txt                        # Python dependencies
├── LICENSE                                 # MIT License
└── README.md                               # Project documentation
```

---

## Data

- **Source:** NOAA National Centers for Environmental Information (NCEI) Climate Data Online, Global Historical Climatology Network daily (GHCN-Daily). Search portal: https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND
- **Stations:**

  | File | Station | Station ID |
  |---|---|---|
  | `data/seattle_rain.csv` | SEATTLE 2.1 ESE, WA US | US1WAKG0225 |
  | `data/sf_rain.csv` | SAN FRANCISCO INTERNATIONAL AIRPORT, CA US | USW00023234 |

- **Format and size:** two CSV files with daily records. The Seattle file has 1,658 rows and 10 columns, and the San Francisco file has 1,826 rows and 4 columns. The analysis uses the `DATE` and `PRCP` (daily precipitation, in inches) columns. Five years of daily data is 1,826 days.
- **Missing data:** San Francisco is complete. Seattle is missing 190 of 1,826 days (168 dates absent from the file and 22 blank values), including a 62-day gap in early 2018.
- **Clean data:** `data/clean_seattle_sf_weather.csv` has one row per city per day, with the columns `date`, `city` (`SEA` or `SF`), `precipitation`, `was_imputed`, `year`, `month`, `day`, and `any_precipitation`.
- **License:** NOAA NCEI data are publicly available. See the NCEI website for its terms of use.

---

## Analysis

All of the analysis is in [`code/seattle_vs_sf_rain_analysis.ipynb`](code/seattle_vs_sf_rain_analysis.ipynb). Each code section in the notebook is preceded by a description of its purpose and followed by an interpretation of its output.

**Steps taken**
1. Inspected both NOAA daily precipitation files.
2. Converted the date columns, which use different formats in each file, to datetime.
3. Kept only the date and precipitation columns, restricted both files to 2018 to 2022, and checked for duplicates.
4. Identified missing values by comparing each file to a complete calendar.
5. Joined the two cities on date with an outer join, reshaped to tidy (long) format, and renamed columns to lowercase names.
6. Imputed each missing Seattle value with Seattle's mean precipitation for that same calendar day across the other years, and flagged imputed values.
7. Created derived variables (year, month, day, and a flag for any precipitation) and saved the clean data.
8. Explored the data with summary statistics and graphs, then tested differences between the cities for each month (Welch's t-test for mean daily precipitation, two-sample z-test for the proportion of days with precipitation), with a robustness check that excludes imputed days.

**Analysis file:** `code/seattle_vs_sf_rain_analysis.ipynb`

**Clean data file:** `data/clean_seattle_sf_weather.csv`

**To run it**
1. Install the packages with `pip install -r requirements.txt`.
2. Make sure `seattle_rain.csv` and `sf_rain.csv` are in the `data/` folder.
3. Open the notebook in Jupyter and run the cells from top to bottom. The notebook finds the `data/` folder from the project root or from the `code/` folder, and it writes the clean data file to the same folder.

---

## Results

- **Amount:** Seattle averaged about 0.113 inches per day versus 0.044 in San Francisco. Over the five years that is about 207 inches in Seattle versus 80 in San Francisco, which includes imputed days.
- **Frequency:** Precipitation was recorded on about 55% of days in Seattle versus about 15% in San Francisco.
- **Consistency:** Seattle had higher average daily precipitation in each of the five years and in every month of the year. The difference in the share of rainy days is statistically significant in all 12 months. The difference in average amount is significant in 10 months, with March and December the exceptions.
- **Robustness:** Using only days with real observations, with no imputed values, gives nearly the same result: about 0.112 versus 0.044 inches per day, and rain on about 51% versus 15% of days.

**Limitations:** each city is represented by a single station, and the two are different types (a station in Seattle and an airport station in San Francisco), so the results describe these locations rather than the whole cities. Seattle's missing days were estimated, not measured. Five years is a short period for drawing climate conclusions, and 2020 was unusually dry in San Francisco.

---

## Authors

- Amruta Hegde - [@AmrutaHegde](https://github.com/AmrutaHegde)

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- Daily precipitation data from NOAA NCEI Climate Data Online: https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND
- Python libraries: pandas, NumPy, Matplotlib, Seaborn, SciPy, and statsmodels.
