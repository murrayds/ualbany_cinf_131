# Assignment 5 - Data wrangling and bar charts

## Overview
In this assignment, you will practice essential data wrangling operations in R and create a bar chart to visualize patterns in customer spending data. You will work with the Customer Personality Analysis dataset, which contains information about customers' demographics and purchasing behavior.

This assignment will help you learn how to:

- Load an excel spreadsheet into RStudio
- Use `select()` to choose specific columns from a dataset
- Use `mutate()` to create new variables based on existing ones
- Use `filter()` to subset data based on conditions
- Use `group_by()` and `summarize()` to calculate statistics for different groups
- Create and label a bar chart using `ggplot2`

## Instructions

First, download the `customers.xlsx` file from Brightspace and save it to a location on your computer that you can easily find (such as your Documents folder or a folder specifically for this class).

This data is originally taken from Kaggle. It contains detailed information about a company's "ideal customers", including information about customer demographics, income, and amount spent in different spending categories. 

In RStudio, create a new script (File -> New File -> R Script). Below is an assignment template. Copy this assignment template into the new file that you just created.

Many lines of code below are incomplete. These are sections marked in brackets, like `[Your chosen spending category]`. Where you see this, you will need to replace it with the required information. If you do not do this, then the line of code will not execute. Comments within the file give instructions for what should go into each file. 

The goal of this assignment is to calculate the amount spent on a spending category by marital status. At the moment, the script is set to calculate the amount spent on wine. For the final deliverable, the student will adapt the script below to choose A DIFFERENT COLUMN in the dataset, and produce a bar plot showing the average. This bar plot must meet the following criteria:
- It should be represent the average amount spent in one of the noted spending categories in the dataset. A list of potential fields is provided below
- It should be a bar chart showing the average by marital status
- It should filter customers by age, for any value of age above 25 years old. 
- The plot should be clearly labeled with a title, axes titles, and a caption that details the column chosen and the filter age
- It should include a choice of bar fill and bar outline color
- The output file should be a .png file

> Other fields include the following:
> 	- MntFruits: Amount spent on fruits in last 2 years
> 	- MntMeatProducts: Amount spent on meat in last 2 years
> 	- MntFishProducts: Amount spent on fish in last 2 years
> 	- MntSweetProducts: Amount spent on sweets in last 2 years
> 	- MntGoldProds: Amount spent on gold in last 2 years

```r
# Week 3 Assignment: Data Wrangling and Bar Charts

# Load required libraries
library(tidyverse)

# TODO: Set your working directory
# Option 1: Use the menu (Session > Set Working Directory > Choose Directory)
# Option 2: Uncomment ONE of the lines below and update the path to match where you saved the file
# setwd("C:/Users/YourName/Documents/CINF131")  # Windows example
# setwd("/Users/YourName/Documents/CINF131")     # Mac example

# Check your working directory
getwd()

# List files in your working directory to confirm the file is there
# You should see "customers.xlsx" in the output
list.files()

# TODO - load the readxl library
# Be sure that the readxl library is installed.
# If the following line gives an error, then run install.packages("readxl") in the console
library(readxl)

# TODO: Load the dataset
# The file is in a .xlsx spreadsheet

customer_data <- read_excel("[your file name here]", sheet = 1)

# Explore the dataset
head(customer_data)

# TODO: Select relevant columns
# Use the `select(...)` command to narrow down to the following columns:
	# Year_Birth, Marital_Status, MntWines, MntFruits, 
	# MntMeatProducts, MntFishProducts, MntSweetProducts, and MntGoldProds

customer_data <- customer_data %>%
	select([insert column names here])

# Check the result
head(customer_data)

# TODO: Create an Age variable
# The data only has the birth year, not the age. 
# Use `mutate` to derive an age variable. The data was collected in 
# 2024, so calculate the age based on the data collection date 
# and each customers' birth year. Use the `Year_Birth` column.

customer_data <- customer_data %>%
	mutate(
		Age = [insert your code here]
	)

# Check that Age was created correctly
head(customer_data)

# TODO: Filter to adults of at least 25 years of age
# use the `filter(...)` command. 
customer_data <- customer_data %>%
  filter([insert code here])

# Check how many rows remain after filtering
nrow(customer_data)

# TODO: Calculate average spending by the marital status. 
# In `group_by(...)`, below, lets group by the marital status variable. 
# Use `head()` or `glimpse()` to get the correct variable name. 
spending_by_marital <- customer_data %>%
  group_by([insert code here]) %>%
  summarize(
    avg_wines = mean(MntWines, na.rm = TRUE)
  )

# View the summary table
spending_by_marital

# TODO: Create a bar chart
ggplot(data = spending_by_marital, 
       aes(x = Marital_Status, y = avg_wines)) +
  geom_col(
	  fill = "[Choose a fill color]", 
	  color = "[Choose a bar outline color]",
	  width = [choose a width] # good options are 0.2, 0.5, 1.0
  ) +
  labs(
    title = "[Your title]",
    x = "Marital Status",
    y = "[Your y-axis label]"
  ) +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# The last line rotates the x-axis labels so they don't overlap
ggsave("[insert your output file name here]")
```

### Assignment Response

After creating your bar chart, write a 2-4 sentence interpretation of what you observe. Your response should address:

1. Which spending category did you choose to visualize?
2. Which marital status group has the highest average spending in your chosen category?
3. Are there any notable differences between groups?

Example response format: "I chose to visualize average spending on wines by marital status. The data shows that married customers spend the most on wine with an average of approximately $300 over two years, while single customers spend considerably less at around $180. The 'Together' category (couples living together but not married) shows spending levels between these two groups, suggesting that household structure may influence wine purchasing behavior."

## Deliverable

Upload your image file to the corresponding assignment on Brightspace. Include your bar chart interpretation (2-4 sentences) in the text box for the submission.

## Troubleshooting

The following are common errors that you might encounter while doing this assignment:

**`"Error in library(tidyverse): there is no package called 'tidyverse'"`**

You should have installed tidyverse in Assignment 1. If you're on a different computer, install it again:

```r
install.packages("tidyverse")
```

**`"Error: 'customers.xlsx' does not exist in current working directory"`**

This means R cannot find your file. Check the following:

1. Did you download the file and save it?
2. Is your working directory set to the folder where you saved the file? Run `getwd()` to check.
3. Does the filename match exactly? Excel files end in `.xlsx`, not `.csv`

Use `Session > Set Working Directory > Choose Directory` to navigate to the correct folder, then try loading the data again.

**`"Error: unexpected '[' in ..."`**

This means you forgot to replace something in [brackets] with your own value! Check through the code and remove any remaining brackets ("[" and "]").

**`"Error: object 'MntWines' not found"` (or similar)**

This error can occur if you're trying to reference a column that doesn't exist. Make sure you:

1. Have run the `select()` command to keep the spending columns
2. Are using the correct column name from the summarized data (use `avg_wines` not `MntWines` in the ggplot code)
3. Haven't made any typos in the variable name

**`"Error: could not find function '%>%'"`**

The pipe operator `%>%` comes from tidyverse. Make sure you've run `library(tidyverse)` at the beginning of your script.

**`"Warning: Removed X rows containing missing values"`**

This is usually okay! Some customers may have missing income or spending data. The `na.rm = TRUE` argument in the `mean()` function tells R to ignore these missing values when calculating averages.

**My bar chart shows too many categories or looks strange**

Check your data! Run `table(customer_data$Marital_Status)` to see what categories exist. Some categories might have very few observations. This is expected in real-world data.
