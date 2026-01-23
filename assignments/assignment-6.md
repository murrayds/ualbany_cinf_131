# Assignment 6 - Temporal data and line charts

## Overview

In this assignment, you will practice creating line charts to visualize how song popularity changes over time. You will work with Spotify chart data from 2021, which contains information about song rankings and streaming counts throughout the year.

This assignment will help you learn how to:

- Load CSV files and explore the structure of time-series data
- Extract date components (month) from date fields
- Use `filter()` to select specific observations from a dataset
- Use `group_by()` and `summarize()` to aggregate data over time periods
- Create line charts with multiple lines using `ggplot2`
- Customize line colors and labels to distinguish between different series

## Instructions
First, download the `spotify_charts_2021.csv` file from Brightspace and save it to a location on your computer that you can easily find (such as your Documents folder or a folder specifically for this class).

This data is originally taken from Kaggle. It contains daily chart information for songs on Spotify during 2021, including the song title, artist, rank, and number of streams.

In RStudio, create a new script (File -> New File -> R Script). Below is an assignment template. Copy this assignment template into the new file that you just created.

Many lines of code below are incomplete. These are sections marked in brackets, like `[Your chosen spending category]` and have TODO written in the comments. Where you see this, you will need to replace it with the required information. If you do not do this, then the line of code will not execute. Comments within the file give instructions for what should go into each file. 

The goal of this assignment is to create a line chart showing how song streaming patterns change over the year. The script initially focuses on "A Holly Jolly Christmas - Single Version" (which shows an expected spike in December). For the final deliverable, you will adapt the script to add TWO MORE SONGS of your choosing to the same plot, each with a different colored line.

Your final plot must meet the following criteria:

- It should show THREE different songs (the Christmas song plus two others that you choose)
- Each song should have its own colored line, with an associated legend
- The plot should be clearly labeled with a title, axes titles, and a legend
- The x-axis should show months, NOT days
- The y-axis should show average number of streams
- The output file should be a .png file

```r
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
# You should see "spotify_charts_2021.csv" in the output
list.files()

# TODO: Load the dataset
spotify_data <- read_csv("[your file name here]")

# Explore the dataset
head(spotify_data)
glimpse(spotify_data)

# Let's see what songs are in the dataset
# This will show us unique song titles
unique(spotify_data$title)

# TODO: Use View() to look at the dataset in a spreadsheet-like format
# This will help you choose which songs to analyze
# Uncomment the line below and run it
# View(spotify_data)

# STEP 1: Extract the month from the date field
# The date field contains full dates (YYYY-MM-DD)
# We want to extract just the month number (1-12)
# First, we need to make sure the date column is recognized as a date
spotify_data <- spotify_data %>%
  mutate(
    date = as.Date(date),  # Convert to date format
    month = as.numeric(format(date, "%m"))  # Extract month as a number
  )

# Check that the month column was created
head(spotify_data)

# STEP 2: Let's start by analyzing "A Holly Jolly Christmas - Single Version"
# This song has an interesting pattern!

# Filter to just this one song
christmas_song <- spotify_data %>%
  filter(title == "A Holly Jolly Christmas - Single Version")

# Group by month and calculate average streams
christmas_monthly <- christmas_song %>%
  group_by(month) %>%
  summarize(avg_streams = mean(streams, na.rm = TRUE))

# View the results
christmas_monthly

# TODO: Create a line chart for the Christmas song...fill in the blanks
ggplot(data = christmas_monthly, aes(x = month, y = avg_streams)) +
  geom_line( # add the line
	  color = "[Choose a color]", 
	  size = 1.2
  ) +
  geom_point( # add points too
	  color = "[Choose a color]", 
	  size = 2
  ) + 
  labs(
    title = "Average Monthly Streams: A Holly Jolly Christmas",
    x = "Month",
    y = "Average Streams"
  ) +
  scale_x_continuous(breaks = 1:12)  # Show all 12 months

# Notice the spike in December! This makes sense for a Christmas song.

# Now let's add two more songs to compare
# TODO: Use View(spotify_data) to pick TWO MORE SONGS from the dataset
# Write down the EXACT title of each song (copy and paste to avoid typos)

# TODO: Filter to your first chosen song
# Replace [Song Title 1] with the exact title of your first song choice
song1_data <- spotify_data %>%
  filter(title == "[Song Title 1]")

# TODO: Filter to your second chosen song
# Replace [Song Title 2] with the exact title of your second song choice
song2_data <- spotify_data %>%
  filter(title == "[Song Title 2]")

# Calculate monthly averages for your chosen songs

# First song monthly averages
# TODO: use group_by and summarize to calculate average monthly streams

song1_monthly <- song1_data %>%
	group_by([code goes here]) %>%
	summarize(avg_streams = [code goes here])

# TODO: Second song monthly averages

song2_monthly <- song2_data %>%
	group_by([code goes here]) %>%
	summarize(avg_streams = [code goes here])

# TODO: Combine all three songs into one dataset for plotting
# summarize() will remove the title column, so we need to add the
# name of the song back. Here, though, we can use a shortened name for 
# each song, so choose something that makes sense
christmas_monthly <- christmas_monthly %>%
  mutate(song = "A Holly Jolly Christmas")

# TODO: Add song identifier to your first song's data
# Replace [Song Title 1] with a SHORT name for your first song
song1_monthly <- song1_monthly %>%
  mutate(song = "[Song Title 1]")

# TODO: Add song identifier to your second song's data
# Replace [Song Title 2] with a SHORT name for your second song
song2_monthly <- song2_monthly %>%
  mutate(song = "[Song Title 2]")

# Combine all three datasets
all_songs <- bind_rows(christmas_monthly, song1_monthly, song2_monthly)

# Check the combined data
head(all_songs)

# TODO: Create a multi-line chart
# TODO: Customize the colors, title, and save the plot

ggplot(
	data = all_songs, 
	aes(
		x = month, 
		y = avg_streams, 
		color = song
	)
) +
  geom_line(size = 1.2) +
  geom_point(size = 2) +
  labs(
    title = "[Your descriptive title here]",
    x = "Month (2021)",
    y = "Average Daily Streams",
    color = "Song"
  ) +
  scale_x_continuous(breaks = 1:12) +
  scale_color_manual(values = c(
    "A Holly Jolly Christmas" = "[Choose a color]"
    "[Song Title 1]" = "[Choose a color]",
    "[Song Title 2]" = "[Choose a color]"
  )) +
  theme(
	  # theme(...) allows us to set options about how the plot looks
	  legend.position = "bottom"
  )

# TODO: Save your plot
# Replace [your_output_filename.png] with a descriptive filename
ggsave("[your_output_filename.png]", width = 10, height = 6, dpi = 300)
```

### Assignment Response

After creating your line chart, write a 2-4 sentence interpretation of what you observe. Your response should address:

1. Which two songs did you choose to add to the chart?
2. How do the streaming patterns of your chosen songs compare to the Christmas song?
3. What trends or patterns do you notice? (e.g., steady throughout the year, peaks at certain times, declining, etc.). How are these patterns different from the Christmas song?

Example response format: "I chose to visualize 'Starboy' by The Weeknd and 'Closer' by the Chainsmokers alongside the Christmas song. While 'A Holly Jolly Christmas' shows a dramatic spike in December and very low streams the rest of the year, both 'Starboy' and "Closer" shows high streams in early 2017 that gradually decline, likely reflecting its initial release popularity. "

## Deliverable

Upload your image file to the corresponding assignment on Brightspace. Include your line chart interpretation (2-4 sentences) in the text box for the submission.

## Troubleshooting

The following are common errors that you might encounter while doing this assignment:

**`"Error: 'spotify_charts_2021.csv' does not exist in current working directory"`**

This means R cannot find your CSV file. Check the following:

1. Did you download the file and save it?
2. Is your working directory set to the folder where you saved the file? Run `getwd()` to check.
3. Does the filename match exactly? Check for typos.

Use `Session > Set Working Directory > Choose Directory` to navigate to the correct folder, then try loading the data again.

**`"Error: unexpected '[' in ..."`**

This means you forgot to replace something in [brackets] with your own value! Check through the code and remove any remaining brackets ("[" and "]").

**`"Error: object of type 'closure' is not subsettable"` when using View()**

Make sure you're using `View()` with a capital V, and that you're passing a dataset to it:

```r
View(spotify_data)
```

**`"Error: Can't subset columns that don't exist"`**

This usually means there's a typo in a column name. Common issues:

- Check that you're using the exact column names from the dataset
- Column names are case-sensitive: `Title` is different from `title`
- Use `glimpse(spotify_data)` to see the exact column names

**Song title not found error**

If you get an error like `"Error: object 'song1_data' is empty"` or your filtered dataset has 0 rows, check:

1. You copied the song title EXACTLY as it appears in the dataset (including capitalization, punctuation, spaces)
2. Use `View(spotify_data)` to find the exact title
3. You can also use `unique(spotify_data$title)` to see all available song titles

**The lines in my plot don't show up or look strange**

Make sure:

1. All three songs have data for multiple months (some songs might only appear briefly in 2021)
2. You've successfully created the `all_songs` dataset by running `bind_rows()`
3. The song names in `scale_color_manual()` match EXACTLY what you put in the `mutate(song = ...)` lines

**`"Error in bind_rows()"`**

This means one of your monthly summary datasets wasn't created properly. Make sure you've run all the filtering and summarizing steps for all three songs before trying to combine them.
