# Assignment 2 - Your first visualization

## Overview
This week you will dive right in and create your own data visualization! 
The `tidyverse` library includes ``ggplot``, which is a system for creating graphs. 
You will be creating and interpreting a scatter plot. 
The data for this assignment is one of the many built-in datasets in R, the `mtcars` dataset. 
This data records the vehicle weight and fuel efficiency of many kinds of cars, and you will be examining the relationship between those two variables.


## Background
The `mtcars` dataset contains information about 32 cars from a 1974 Motor Trend magazine. Key variables you'll use:

- `wt`: Weight (in 1,000 lbs)
- `mpg`: Miles per gallon (fuel efficiency)
- `cyl`: Number of cylinders (4, 6, or 8)
- `hp`: Horsepower

## Instructions

Create a new R script in RStudio. Add the following to the top

```r
# Load the tidyverse package
library(tidyverse)
```

The `mtcars` dataset should already exist. To check, add and execute the following lines. 
The `head(...)` is a function. 
Functions are like pre-packaged and re-usable bits of code that do certain things. 
Functions typically take an input (here, the name of the dataset), and provide an output (here, some rows from the dataset) 

```r
# show the first several rows of the dataset
head(mtcars)
```

Next, create your scatterplot using `ggplot` syntax. From the reading, recall that `ggplot` requires us to map variables in our dataset to "aesthetics". 
Here, we just want to map the `x` and `y` aesthetics, which correpond to the x and y axes, respectivesly. 

For this analysis, we are interested in looking at the relationship between vehicle weight and fuel efficiency. 
Fill in the blanks as follows:
- First blank `(x = ___)`: The variable for the x-axis. Use the `wt` (weight) variable.
- Second blank `(y = ___)`: The variable for the y-axis. Use `mpg` (miles per gallon)

```r

ggplot(data = mtcars, aes(x = ___, y = ___)) +
  geom_point()
```

Next, highlight the two lines of code for the ggplot graph, and click run. You should see the plot in the plots pane!

Now, we will decorate the plot. There are lots of things we can do, such as changing the color of the points, their size, and adding labels. See the below template:

```r
ggplot(data = mtcars, aes(x = ___, y = ___)) +
  geom_point(size = ___, shape = ___, color = "___") +
  labs(
    title = "___",
    x = "___",
    y = "___",
  )
```

In `geom_point(...)` you can fill in values that control the display of the points:
- `size = ___`: this is a number that controls how big the points are. Try using values between 0 and 20 to see what happens.
- `shape = ___`: ggpot supports many shapes for points. These shapes are usually distinguished by numbers. Experiment with the numbers 15, 16, 17, and 18 to see some of these options.
- `color = "___"`: This will be the color the points are shown in. ggplot supports lots of colors, but using color in programming is often complicated. Fortunately, we can also use the name of a few main colors. In the quotation marks, experiment with values like "blue", "red", "orange", and "purple". 

In `labs(...)` you can fill in values that will show up as labels on the plot.
- `title = "___"`: Write a descriptive title (e.g., "Relationship Between Car Weight and Fuel Efficiency")
- `x = "___"`: Label for x-axis (e.g., "Weight (1000 lbs)")
- `y = "___"`: Label for y-axis (e.g., "Miles Per Gallon")


Finally, you must **save your plot** to your local computer.

```r
# Save the plot
ggsave("week2_plot.png", width = 8, height = 6)
```

This will save it to your computer. The string `week2_plot.png` is the filename.

## Assignment response
In your own words, describe the relationship between vehicle weight and fuel efficiency. How exactly did you come to your conclusion from the scatter plot? 

Write a 2-4 sentence repsonse to this, which will be included alongside the other deliverable in the assignment submission box. 

## Deliverable
You will submit the image file created as part of this assignment. 
**You do not have to submit the R Script**. 
The image file should contain the graph you created for this assignment. 
This graph should include labels for title, the x, and the y-axis. The points should also be non-default color.

Upload this image to Brightspace along with the assignment response. 

## Troubleshooting

**`"Error: object 'wt' not found"`**

Make sure you're using the mtcars dataset
Check spelling—R is case-sensitive

**`"Error in ggsave()"`**

Make sure you created the plot first (run the ggplot code before ggsave)

**I can't find my saved image??**

Look in the Files pane (bottom-right).
Click "More" → "Show Folder in New Window" to see where files are saved.
Or check your working directory with getwd().
Or Search for the filename using your computers' search function.

