# Seattle and San Francisco Precipitation Comparison

This project explores daily precipitation records for Seattle and San Francisco from 2018 through 2022.

---

## Project Overview

- **Objective:** Compare precipitation totals in Seattle and San Francisco over the same five-year period.
- **Domain:** Weather and climate data analysis.
- **Key techniques:** Data inspection and cleaning, date alignment, missing-value analysis, grouping by month and year, and time-series visualization.


---

## Project Structure

```
├── data/                 # Raw and processed data
├── code/                 # Jupyter notebooks and Python scripts
├── reports/              # Generated reports and visualizations
├── requirements.txt      # Dependencies
└── README.md             # Project documentation
```

---

## Data

- **Source:** (https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND)
- **Description:** Brief overview of the dataset features, size, and format
- **License:** (if applicable)

---

## Analysis

The primary analysis is [`code/Seattle_San_Francisco_weather_comparison.ipynb`](code/Seattle_San_Francisco_weather_comparison.ipynb). It inspects the two input datasets, joins observations by date, reviews missing values, and plots yearly and monthly precipitation totals.

To run it:

1. Install the listed packages with `pip install -r requirements.txt`.
2. Open the notebook in Jupyter from this project folder (or a child folder); its path setup searches for the `data` directory.
3. Run the notebook cells from top to bottom.

The chart cells currently read `data/clean_seattle_sf_weather.csv`. The cell that writes this file is commented out, so the charts use the existing cleaned CSV unless that export step is enabled and run first.

---

## Results

The notebook's current yearly chart suggests that the Seattle station recorded more total precipitation than the San Francisco airport station over 2018–2022. The monthly chart shows substantial variation, so the overall result does not mean Seattle was wetter in every month. These charts compare precipitation amounts; they do not compare the number of rainy days.

Seattle has missing observations, and the current imputation steps calculate seasonal averages from Seattle and can apply those values to missing records from either location. This may affect the comparison. The data also represent individual stations, not all parts of either city.

---

## Authors

- Your Name - [@yourhandle](https://github.com/AmrutaHegde)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

- Python libraries: pandas, NumPy, Matplotlib, and Seaborn.
- The project uses the weather CSV exports from https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND
