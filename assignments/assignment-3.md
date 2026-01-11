# Assignment 3 - Inspecting a dataset

## Overview
This week you'll practice exploring a dataset before visualizing it. 
Understanding your data's structure, size, and variable types is the essential first step in any analysis. 
You'll use the `penguins` dataset to practice data frame exploration, then create a visualization that shows what you discovered.

## Data background
The `penguins` dataset contains measurements of 344 penguins from three species observed on islands in Antarctica. 
This is a real dataset collected by scientists studying penguins.
It contains measurements collected from three different species of penguin: Adelelie, Chinstrap, and Gentoo. 

This dataset is not default in R. It is part of another library. So, you will need to install this new package. In the RStudio console, type the following:

```r
install.packages("palmerpenguins")
```

## Instructions
In RStudio, create a new scrit (File -> New File -> R Script). Follow along with the instructions below,

```r
# Load required packages
library(tidyverse)

# use `install.packages("palmerpenguins")` to install the palmerpenguins package
library(palmerpenguins) 

# Load the penguins dataset
data(penguins)
```

Run each of the following commans, line-by-line. Each line uses a different function. 
Each of these functions takes as input the dataset (here, `penguins`), and outputs some information about the dataset.
- `view`: Opens a new window to show the dataset, a little like a spreadsheet. This will open a new tab in RStudio. You will need to close it to return to the script.
- `glimpse`: This will print out a copmact view of the dataset structure to the console
- `head`: This will show the first few rows of the dataset
- `nrow`: This will plot the number of observations (rows)
- `ncol`: This will print out the number of variables (columns)

```r
# View the entire dataset in a spreadsheet-like format
View(penguins)

# Get a compact view of the structure
glimpse(penguins)

# See the first few rows
head(penguins)

# Determine the size of the dataset
nrow(penguins)  # Number of observations (rows)
ncol(penguins)  # Number of variables (columns)
```


Next, you will practice accessing specific variables. In R, after you type the name of the dataset, you use the "$" character to access specific variables. 
For example, the code `penguins$species` will access the `species` variable (column) of the `penguins` data frame, printing out all the values in that column.

```r
# Access the species variable
penguins$species

# Access the bill_length_mm variable
penguins$bill_length_mm
```

You will also use some basic commans for calculating basic information summary statistics for variables in the dataset. 
The first of these is `mean(...)`. This is a function that takes as input a set of numbers, and returns the mean (average) of those numbers. 
If we call `mean(penguins$bill_length_mm, na.rm = TRUE)`, then we will calculate the the average of all the values included in the `bill_length_mm` column. 
The second part of this function's input, `na.rm = TRUE` is irrelevant at the moment; just know that you need to include it. Below are the commans you will run:

- `mean`: calculates the mean (average) of a set of numbers
- `max`: returns the maximum value in a list of numbers
- `min`: returns the minimum value in a list of numbers

```r
# Calculate statistics on bill length
mean(penguins$bill_length_mm, na.rm = TRUE)
max(penguins$bill_length_mm, na.rm = TRUE)
min(penguins$bill_length_mm, na.rm = TRUE)
```

Next, calculate statistics for another variable, `body_mass_g` (body mass in grams)
```r
mean(penguins$___, na.rm = TRUE)
max(penguins$___, na.rm = TRUE)
```

Finally, lets make a graph that will be submitted for this assignment. This graph is a boxplot showing the distribution of one of the variables in the `penguins` dataframe. 
You must fill in ALL the blanks, including the caption.

What to fill in for `ggplot(...)

- `x = ___`: The categorical variable (species)
- `y = ___`: The numeric variable (bill_length_mm)

What to fill in for `labs(...)`
- `title = "___"`: A descriptive title (e.g., "Bill Length Across Penguin Species")
- `x = "___"`: Label for x-axis (e.g., "Species")
- `y = "___"`: Label for y-axis (e.g., "Bill Length (mm)")

For the caption, 

- First ___: Number from nrow(penguins) (total observations)
- Second ___: Number from ncol(penguins) (total variables)
- Third ___: Mean from mean(penguins$bill_length_mm, na.rm = TRUE), rounded to 1 decimal place

```r
# Create boxplot comparing bill length by species
ggplot(data = penguins, aes(x = ___, y = ___)) +
  geom_boxplot(fill = "skyblue") +
  labs(
    title = "___",
    x = "___",
    y = "___",
    caption = "Data includes ___ observations and ___ variables. Mean bill length = ___ mm."
  )
```

For example, the following is an example caption (the values however, are not correct)
```r
caption = "Data includes 500 observations and 20 variables. Mean bill length = 42.9 mm."
```

You will need to fill in the caption using values obtained from `nrow`, `ncol`, and by calculating the average bill length. 

Finally, you will need to save your plot:

```r
# Save the plot
ggsave("week3_plot.png", width = 8, height = 6)
```

## Assignment Response
What is one pattern or difference you notice between the three penguin species in your boxplot?
Justify your response using specific information from your plot. 
Write 2-4 sentences describing what you observe. 



## Deliverable
You must submit the image file created with this assignment, with all labels included. Points will be deducted for any missing labels. 

Include the assignment repsonse alongside in the textbox alongside the Brightspace submission.
