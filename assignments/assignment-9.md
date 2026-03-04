# Assignment 9 - Making avocados look bad

## Overview

In this assignment, you'll practice both good and bad data visualization by creating two charts that answer the same question: one that follows all the best practices you've learned, and one that deliberately violates them in creative ways.

This is a kind of "red-teaming" exercise that I hope will let you take some visualization lessons to heart. 

You'll be working with a dataset on avocado sales across US cities to answer a simple question: **Which cities love avocados the most?**

## Dataset: Avocado Prices and Sales (2018)

This dataset contains weekly retail sales data for Hass avocados across different US cities and regions from 2015 through 2018. I got this from [Kaggle](https://www.kaggle.com/datasets/neuromusic/avocado-prices), though the dataset comes from the Hass Avocado Board.

**Key variables:**
- `Date`: The date of the observation (weekly)
- `AveragePrice`: Average price per single avocado (in dollars)
- `type`: Either "conventional" or "organic"
- `year`: The year (2015-2018 for all observations)
- `Region`: The city or region of observation
- `Total Volume`: Total number of avocados sold that week
- `4046`, `4225`, `4770`: Sales counts for specific avocado PLU codes (size varieties)

**Dataset notes:**
- Data comes from actual retail cash register scans
- Prices reflect per-unit cost even when sold in bags
- Includes multiple retail channels: grocery, mass retailers, drug stores, etc.
- All avocados are Hass variety
- Each region has multiple observations (one per week)

## Assignment Task

**Research Question:** Which US cities/regions love avocados the most? 

You will create **TWO visualizations** answering this question:

1. **A GOOD visualization** that follows all the best practices from class
2. **A BAD visualization** that creatively violates as many best practices as possible. Better yet, if the chart is intentionally misleading about the findings.

Both visualizations must show the same underlying data and answer the same question—but one should make it easy to understand, while the other should make it difficult (or misleading). You have complete freedom in *how* you make the bad chart look bad. 

### Preparing the data:
1. Calculate the **total volume of avocados sold** for each region across the entire year
    - You'll need to sum up all the weekly `Total Volume` values by region
    - Consider whether to include both conventional AND organic, or focus on one type
2. Select the **top 5-10 regions** to display
    - There are many regions in the dataset; showing all would be cluttered
    - Focus on the cities with highest total sales

## Deliverable

You must submit **THREE items** to Brightspace:
### 1. Good Visualization (PNG file)

- Filename: `lastname_firstname_good.png`
- Professional, clear visualization following all best practices
- Shows top 5-10 regions by total avocado sales

### 2. Bad Visualization (PNG file)
- Filename: `lastname_firstname_bad.png`
- Deliberately terrible visualization of the SAME data
- Creatively violates at least 5-6 best practices

### 3. Written Reflection (in the Brightspace text box)

Write a response (about 2 paragraphs) that addresses the following points:

**The Good Visualization**
- What chart type did you choose and why?
- What best practices did you follow?
- What does your chart reveal about which regions love avocados most?

**The Bad Visualization**
- What violations did you include? (List at least 5-6 specific bad practices)
- How do these violations make the chart harder to read or potentially misleading?
- Despite being terrible, does it still technically show the same data?

**Lessons Learned**
- Which violations had the biggest negative impact on the visualization?
- How will this affect how you create (or evaluate) visualizations in the future?

## Helpful tips

### Calculating Total Sales by Region

You'll need to sum up all weekly sales for each region:

```r
# Example: Get total avocado sales by region
regional_totals <- avocado %>%
  group_by(Region) %>%
  summarize(total_sold = sum(`Total Volume`, na.rm = TRUE)) %>%
  arrange(desc(total_sold))  # Sort from highest to lowest

# Look at the top regions
head(regional_totals, 15)
```

**Note:** The `Total Volume` column name has a space, so you might need to use backticks: `Total Volume`

### Handling Conventional vs. Organic
The dataset distinguishes between "conventional" and "organic" avocados when reporting sales. You have multiple choices here:

- Combine both types (total avocado sales regardless of type)
- Show only conventional (the majority of sales)
- Compare both types with grouped/stacked bars

Its up to you which you do, but you will have do choose something!

**For making a BAD visualization:**
Be creative! This is your chance to have fun. Think about charts you've seen that made you frustrated. Don't just make it ugly—make it genuinely hard to read or misleading. Consider what would make you angriest if you encountered this in a report, or what would make me angriest if I saw it as a normal submission. 
