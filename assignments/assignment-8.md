# Assignment 8

## Overview

In this assignment, you will analyze the early growth of COVID-19 across different countries using time series data from the first months of the pandemic. You'll create visualizations on both linear and logarithmic scales to understand why log scales are essential for analyzing exponential growth patterns.

## Dataset: Novel Coronavirus 2019 (Early Pandemic Data)
This dataset contains daily cumulative counts of COVID-19 cases across countries and regions from the early months of the 2020 pandemic (retrieved from [Kaggle](https://www.kaggle.com/datasets/sudalairajkumar/novel-corona-virus-2019-dataset/data)).

**Key variables:**
- `ObservationDate`: Date of the observation (in MM/DD/YYYY format as text)
- `Province/State`: Province or state (may be empty for country-level data)
- `Country/Region`: Country of the observation
- `Confirmed`: **Cumulative** number of confirmed cases up to that date
- `Deaths`: **Cumulative** number of deaths up to that date
- `Recovered`: **Cumulative** number of recovered cases up to that date

**Important notes:**
- This is **time series data** with cumulative counts (not daily new cases)
- Multiple rows exist for each country (one per province/state and one for country total)
- Dates are stored as text and need to be converted to proper date format
- The dataset covers the early pandemic period when growth was exponential in many countries. See the Helpful Tips section below. 

## Assignment Task

**You must answer this question with the dataset:** Which countries experienced the fastest COVID-19 ***growth rate*** during the early pandemic, and when did growth rates change? Note that this is not about total number of cases...but about the ***growth rate***. 

**Your visualizations must:**

1. **Select 3-5 countries to compare**
    - Choose countries with substantial case counts (e.g., Italy, US)
    - Make sure the countries you select have interesting patterns to compare. Explore some countries
2. **Show cumulative confirmed cases over time**
    - X-axis: Date
    - Y-axis: Confirmed cases (linear scale)
    - One line per country, colored differently
3. **Use proper time range**
    - Start from the first date with at least 100 cases for any of your selected countries
    - Include enough time to see the growth patterns (recommend at least 60-90 days)
4. **Visualizations should look professional**
    - Clear titles, labels, legend, and text, with a good chart design.
5. **Save as PNG**
    - Filename: `lastname_firstname_linear.png`

## Deliverables
This assignment has THREE deliverables that you must submit on Brightspace:
### 1. Linear-Scale Visualization (PNG file)
- Filename: `lastname_firstname_linear.png`
- Shows cumulative COVID-19 cases over time for your selected countries
- Uses a standard linear y-axis

### 2. Log-Scale Visualization (PNG file)
- Filename: `lastname_firstname_log.png`
- Shows the SAME data as the linear plot but with logarithmic y-axis
- Should use same countries, time period, and styling as teh linear-scale plot for easy comparison
- Clearly mark that this is a logarithmic scale 
### 3. Written Interpretations (in the Brightspace text box)

Write a response that addresses the research question: 
- What patterns do you observe in the linear-scale plot?
- What problems or limitations do you notice with the linear scale for this data?
- What patterns do you observe in the log-scale plot?
- Which countries had the fastest growth rates? (Hint: steeper lines on log scale = faster exponential growth)
- On the log scale, do you see any countries whose growth rate changed suddenly? When and why might this have happened?
- Why is the log scale particularly helpful for this COVID-19 data?

This written response should be about 2 paragraphs in length. 

## Helpful Tips

### Column names with special characters
Column names with special characters (like `Country/Region`) need backticks (\`) around them in R. See the following:

```r
covid$`Country/Region`
```

### Working with Dates
The `ObservationDate` column is stored as text (e.g., "01/22/2020"). R will not automatically process this date into the `Date` data type. You need to convert it to a proper date format before plotting:

```r
covid$ObservationDate <- as.Date(covid$ObservationDate, format = "%m/%d/%Y")
```
The `format` parameter of this function takes a string that details what the date looks like. For example, `"%m/%d/%Y"`tells R that, in this string, the month comes first (%m), followed by a "/" and the day (%d), followed by a "/" and then the year (%Y).

### Handling Multiple Rows Per Country
**Important:** This dataset has multiple rows for each country because it includes province/state-level breakdowns. For example, "US" appears many times (once for each state plus territories).

To get country-level totals, you need to **group by country and date**, then sum the cases:

```r
# Example: Get country-level data
country_totals <- covid %>%
  group_by(`Country/Region`, ObservationDate) %>%
  summarize(
    ... # calculate your new variable here
  )
```

### Filtering to Multiple Countries

Use the `%in%` operator to filter to your selected countries in one statement:

```r
# Example: Filter to 5 specific countries
selected_countries <- country_totals %>%
  filter(`Country/Region` %in% c("Country 1", "Country 2", "Country 3", "County 4", "Country 5"))
```

Replace the country names with your chosen countries. Make sure the names match exactly what appears in the dataset!


### Filtering by Date
You may want to start your analysis from a meaningful point (e.g., when cases reached 100):

```r
# Example: Filter to dates after a certain point
covid_subset <- country_totals %>%
  filter(ObservationDate >= as.Date("2020-02-15"))

# Or: Start from first date any country had 100+ cases
covid_subset <- country_totals %>%
  filter(total_confirmed >= 100)
```

### Creating the Log-Scale Plot

To put the y-axis on a logarithmic scale in ggplot, add `scale_y_log10()`:

```r
# Linear scale (normal)
ggplot(data, aes(...)) +
  geom_line() +
  scale_x_log10() + # to log-scale the x-axis 
  scale_y_log10() # to log-scale the y-axis
```

### Inspect the dataset yourself!
Always be sure to check the dataset manually so you can get an intuitive understanding of it:
```r
# See what countries are in the dataset
unique(covid$`Country/Region`)

# Check how many observations per country
covid %>% count(`Country/Region`, sort = TRUE)

# Look at a specific country's data
covid %>%
  filter(`Country/Region` == "Italy") %>%
  View()
```
