# Assignment 4 - Loading data

## Overview

In this assignment, you will practice loading an external dataset from your local computer into RStudio and creating a properly labeled histogram to visualize the distribution of a numeric variable. You will work with the Red Wine Quality dataset, which contains physicochemical properties of Portuguese red wine samples.

This assignment will help you learn how to:

- View and set the working directory in RStudio
- Download a dataset and load it using `read_csv()` in RStudio
- Generate and label a histogram, experimenting with different numbers of bins
- Interpret the shape of a distribution

## Instructions

First, download the `red_wine_quality.csv` file from Brightspace and save it to a location on your computer that you can easily find (such as your Documents folder or a folder specifically for this class). This dataset contains a variety of metrics about quality of a particular variety of Vinho Verde - a kind of Portuguese wine, including things like the content of different types of chemicals. This is a somewhat famous dataset for education and testing because it has so many differnet metrics with different shapes. 

In RStudio, create a new script (File -> New File -> R Script). Below is an assignment template. Copy this assignment template into the new file that you just created. You will fill in the lines containing brackets (\[...\]) in the code, and modify the script in order to produce the assignment deliverable. 

The deliverable for this assignment will be an image file (.png) for a graph. The graph you create will meet the following criteria:
- It must be a histogram (example code is provided)
- It must present one of the numeric variables in the provided dataset
- You must select a sensible number of bins from the data to ensure that is not too wide nor too narrow
- You must fill in all axis labels
- You must provide a custom color for the bars. This is specified by the `fill` parameter.

```r
# Load required libraries
library(tidyverse)

# TODO: Set your working directory
# Option 1: Use the menu (Session > Set Working Directory > Choose Directory)
# Option 2: Uncomment ONE of the lines below and update the path to match where you saved the CSV file

# setwd("C:/Users/YourName/Documents/CINF131")  # Windows example
# setwd("/Users/YourName/Documents/CINF131")    # Mac example

# Check your working directory
getwd()

# List files in your working directory to confirm the CSV is there
# You should see "red_wine_quality.csv" in the output
list.files()

# TODO: Load the data
# This file should be in your working directory
wine_data <- read_csv("[type file name here].csv")

# This shows a general overview
glimpse(wine_data)

# This shows the first few rows
head(wine_data)

# TODO: Create a histogram
ggplot(data = wine_data, aes(x = [Your chosen variable])) +
  geom_histogram(
	  bins = [Number of bins], 
	  fill = [your color], 
	  color = "black"
  ) +
  labs(
    title = "[Your descriptive title here]",
    x = "[Your x-axis label here]",
    y = "Frequency"
  )

# TODO: save the output
ggsave("[your_file_name_here].png")
```

### Assignment Response

After creating your histogram, write a 2-3 sentence interpretation of what you observe. Your response should address:

1. What is the central tendecy of the distribution for this variable? 
2. Describe the variability/spread of this distribution. Is it wide? or narrow?
3. What is the shape of the distribution? (Is it normal/symmetric, right-skewed, left-skewed, uniform, or bimodal?)
4. Do you observe any other notable features such as outliers or gaps?

Example response format: "The distribution of alcohol content in red wines is approximately normal with a slight right skew. Most wines have alcohol content between 9% and 12%, with a few outliers extending to 14%. There are no obvious gaps in the data, suggesting a continuous range of alcohol levels in the sample."

## Deliverable

Upload the file containing your image (.png format) to the corresponding assignment on Brightspace. Include your histogram interpretation (2-3 sentences) in the text box for the submission.

## Troubleshooting

The following are common errors that you might encounter while doing this assignment:

**`"Error: unexpected '[' in ..."`**

This means you forgot to replace something in \[brackets\] with your own value! Check through the code and remove any remaining brackets ("\[" and "\]").

**`"Error: 'red_wine_quality.csv' does not exist in current working directory"`**

This means R cannot find your CSV file. Check the following:

1. Did you download the file and save it?
2. Is your working directory set to the folder where you saved the file? Run `getwd()` to check.
3. Does the filename match exactly? Check for typos and ensure it ends in `.csv`

Use `Session > Set Working Directory > Choose Directory` to navigate to the correct folder, then try loading the data again.
