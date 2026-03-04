# Assignment 7 - The Deadliest Storms

## Overview

In this assignment, you will conduct an exploratory data analysis of severe weather events in the United States using the 2019 NOAA Storms database. Your goal is to investigate which types of severe weather pose the greatest danger to human life and which states are most affected by the deadliest weather events.

## Dataset: NOAA Storms (2019)

The NOAA Storms database (retreived from [Kaggle](https://www.kaggle.com/datasets/atinakarim/noaa-severe-storm-database?select=Storms_2019.csv)) contains records of severe weather incidents across the United States for the year 2019. Each row represents a single severe weather event.

**Key variables:**

- `event_type`: The type of severe weather (e.g., "Tornado", "Flood", "Thunderstorm Wind", "Flash Flood", "Hail", etc.)
- `state`: The state where the event occurred
- `deaths_direct`: Number of deaths directly caused by the event
- `deaths_indirect`: Number of deaths indirectly caused by the event
- `injuries_direct`: Number of injuries directly caused by the event
- `injuries_indirect`: Number of injuries indirectly caused by the event

The dataset contains many different event types. Some are very common (thousands of events), while others are quite rare (fewer than 10 events).

**Assignment Task**: 
You will answer the following question: Which types of severe weather events are most dangerous in terms of casualties (deaths and injuries combined)?

**Your analysis must:**

1. **Select 4 event types to compare**
    - Choose event types that have a reasonable number of events in the dataset (at least 50 events each)
    - The choice of which event types is up to you—pick ones you find interesting or want to learn more about
    - You MUST filter to only these selected event types (don't try to analyze all 50+ event types at once)
    - Use what you have learned working with R to explore the data and select event types
2. **Calculate total casualties**
    - Create a new variable that combines deaths and injuries (both direct and indirect)
    - Group by event type and calculate the total casualties for each type
    - Note that there are likely missing values
3. **Create a professional visualization**
    - Use an appropriate chart type for comparing categories (think: what did we learn about comparing categorical data?)
4. **Save your visualization**
    - Export as a PNG file
    - Name it: `lastname_firstname_part1.png`

## Deliverables

Submit to the relevant assignment on Brightspace. There are two submission components.
### 1. Visualization (PNG file)
- Filename: `lastname_firstname_part1.png`
- Shows comparison of casualties across your selected event types
### 2. Written Interpretations (in the Brightspace text box)

Write one paragraph addressing the research question: 
- Which event types are most dangerous in terms of total casualties?
- Were there any surprising findings? 

## Helpful Tips

### Getting Acquainted with the Data

**Before you start your analysis, explore the dataset!** This is a new dataset you haven't worked with before. Use these functions to get familiar with it:

```r
# Load the data first
library(tidyverse)
storms <- read_csv("noaa_storms_2019.csv")

# Get a quick overview of the structure
glimpse(storms)

# Look at the first few rows
head(storms)

# Open the data viewer (in RStudio)
View(storms)

# See what event types exist
unique(storms$event_type)

# Count how many of each event type
storms %>% count(event_type, sort = TRUE)
```

**Important:** Use the `count()` function shown above to see how many events of each type exist. This will help you choose event types that have at least 50 events.

### Filtering to Multiple Values

You'll need to filter to only your selected event types. Here's how to filter to multiple values in a single `filter()` statement:
```r
# Example: Filter to only three event types
my_events <- storms %>%
  filter(event_type %in% c("event1", "event2", "event3"))

# The %in% operator checks if event_type matches ANY value in the vector
# This is much better than: filter(event_type == "Tornado" | event_type == "Flood" | ...)
```

### Calculating Total Casualties

You'll need to create a new variable that combines all four casualty columns. Use `mutate` to create such a variable.
