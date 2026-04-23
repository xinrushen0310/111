# Manchester United Stock & Match Performance Analysis

## 1. Problem & User
This project investigates whether Manchester United's (NYSE: MANU) on-pitch performance in the Premier League has a measurable impact on its short-term stock price movements. The intended audience includes sports economists, financial analysts, and retail investors interested in the intersection of sports performance and financial markets.

## 2. Data
The analysis integrates two primary datasets covering six Premier League seasons (August 2019 to May 2025):
- **Stock Data:** Monthly stock prices, trading volumes, and returns for MANU, sourced from the Center for Research in Security Prices (CRSP) via the Wharton Research Data Services (WRDS) platform (accessed April 2025).
- **Match Data:** Match-level results (goals, outcomes, and points) sourced from [football-data.org](https://www.football-data.org/) (accessed April 2025).

The merged dataset contains **20 columns** per month, including:

| Category | Columns |
|---|---|
| Stock | Price (USD), Volume, Monthly Return (%), 3-Month Rolling Avg Return |
| Match Counts | Matches, Wins, Draws, Losses |
| Goals | Goals For, Goals Against, Goal Difference |
| Derived Metrics | Win Rate (%), Points Per Match, Avg Goal Diff, Form (Last 5) |
| Rolling Averages | 3M Avg Win Rate, 3M Avg Goal Diff |
| Labels | Season, Dominant Result |

## 3. Methods
The analytical workflow was implemented entirely in Python:
- **Data Acquisition:** Queried WRDS PostgreSQL database using the `wrds` library and fetched CSV files via `requests` and `pandas`.
- **Data Cleaning & Transformation:** Parsed match dates, aggregated results to a monthly frequency, computed derived metrics (win rate, points per match, average goal difference), assigned season labels, and calculated 3-month rolling averages.
- **Analysis & Visualization:** Utilized `matplotlib` and `seaborn` for time-series plots, box plots, scatter plots, dual-axis rolling-average charts, season-level grouped bar charts, and a full correlation heatmap. Conducted statistical testing (independent t-tests and Pearson correlation) using `scipy.stats`.
- **Productization:** Built a seven-page interactive web application using `streamlit` with automated insight generation, dynamic filtering by date range and season, and CSV data export.

## 4. Key Findings
- **Win vs. Loss Returns:** Months dominated by wins show a slightly higher average stock return compared to loss-dominated months, but the difference is not statistically significant at the 5% level.
- **Goal Difference Correlation:** There is a very weak positive relationship (Pearson r ≈ 0.15) between monthly goal difference and stock returns, indicating that large goal differences do not reliably predict positive stock performance.
- **Season-Level Disconnect:** The best on-pitch season (highest win rate) does not correspond to the best stock performance season, reinforcing the weak link between football success and financial returns.
- **Rolling Trends Diverge:** Even after smoothing with 3-month rolling averages, the stock return and win rate lines frequently move in opposite directions.
- **Corporate Events Dominate:** Macro-economic and corporate events overwhelmingly dictate price movements. The sharpest decline occurred in March 2020 (COVID-19), while the most significant surge (+40%) happened in early 2023 amid rumors of a club sale.

## 5. Dashboard Pages

| Page | Description |
|---|---|
| **Overview** | 10 KPI cards + key findings summary |
| **Stock Price Timeline** | Monthly price chart with colour-coded match results + automated insights |
| **Return by Match Result** | Box plot + bar chart + summary statistics + t-test |
| **Correlation Analysis** | Scatter plot + Pearson r metrics + full correlation heatmap |
| **Season Breakdown** | Season summary table + win rate vs return chart + goals chart + insights |
| **Rolling Trends** | 3-month rolling averages (return vs win rate, return vs goal diff) |
| **Data Table** | Full 20-column dataset with quick stats + CSV download |

## 6. How to Run
To run the Streamlit application locally:

1. Clone this repository or download the project files.
2. Ensure you have Python 3.7+ installed.
3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Run the Streamlit app:
   ```bash
   streamlit run app.py
   ```
5. Open the provided local URL (usually `http://localhost:8501`) in your web browser.

## 7. Product Link / Demo
- **Streamlit App:** [Insert your deployed Streamlit Community Cloud link here]
- **Demo Video:** [Insert your 1-3 minute demo video link here]

## 8. Limitations & Next Steps
- **Limitations:** The primary limitation is the mismatch in data frequency. Aggregating weekly match results to a monthly level obscures the immediate market reaction to specific victories or defeats. The analysis also does not control for broader market trends or financial fundamentals.
- **Next Steps:** Future improvements could involve utilizing daily stock data and conducting an event study methodology to measure abnormal returns in the days immediately following a match. Incorporating sentiment analysis from social media or news articles could also provide a more nuanced view of investor reactions.
