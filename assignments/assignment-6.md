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
First, download the `spotify_US_2021.csv` file from Brightspace and save it to a location on your computer that you can easily find (such as your Documents folder or a folder specifically for this class).

This data is originally taken from Kaggle. It contains daily chart information for songs on Spotify in the US during 2021, including the song title, artist, rank, and number of streams.

In RStudio, create a new script (File -> New File -> R Script). Below is an assignment template. Copy this assignment template into the new file that you just created.

Many lines of code below are incomplete. These are sections marked in brackets, like `[Pick a color]` and have TODO written in the comments. Where you see this, you will need to replace it with the required information. If you do not do this, then the line of code will not execute. Comments within the file give instructions for what should go into each file. 

The goal of this assignment is to create a line chart showing how song streaming patterns change over the year. The script initially focuses on "All I Want for Christmas is You" (which shows an expected spike in December). For the final deliverable, you will adapt the script to add TWO MORE SONGS of your choosing to the same plot, each with a different colored line. You will also have to answer several questions included in the comments and include your response in the caption. 

Your final plot must meet the following criteria:

- It should show THREE different songs (the Christmas song plus two others that you choose)
- Each song should have its own colored line, with an associated legend
- The plot should be clearly labeled with a title, axes titles, and a legend
- The x-axis should show days
- The y-axis should show number of streams
- The caption should include answers to basic questions about each song. The questions are detailed within the code comments below.
- The output file should be a .png file
- 

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
# You should see "spotify_us_2021.csv" in the output
list.files()

# TODO: Load the dataset
spotify_data <- read_csv("[path to dataset]")

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


# Let's start by analyzing "All I Want for Christmas Is You"
# Filter to just this one song
christmas_song <- spotify_data %>%
  filter(title == "All I Want for Christmas Is You")

# TODO: Create a line chart for the Christmas song...fill in the blanks
ggplot(data = christmas_song, aes(x = date, y = streams, group = title)) +
  geom_line( # add the line
    color = "[pick a color]", 
    size = 1.2
  ) +
  labs(
    title = "Daily Streams: All I Want for Christmas is You",
    x = "[Your x-axis title]",
    y = "[Your y-axis title]"
  ) +
  scale_x_date(limits = c(as.Date("2021-01-01"), as.Date("2021-12-31"))) # show all 12 months


# Now let's add two more songs to compare
# TODO: Use View(spotify_data) to pick TWO MORE SONGS from the dataset
# Write down the EXACT title of each song (copy and paste to avoid typos)

# TODO: Filter to your first chosen song
# Replace [Song Title 1] with the exact title of your first song choice
song1_data <- spotify_data %>%
  filter(title == "[Pick a song]")

# TODO: Filter to your second chosen song
# Replace [Song Title 2] with the exact title of your second song choice
song2_data <- spotify_data %>%
  filter(title == "[Pick a song]")

# Combine all three datasets
all_songs <- bind_rows(christmas_song, song1_data, song2_data)

# Check the combined data
head(all_songs)



# Now, lets make a table showing the average number of months that each song
# was in the top charts in 2021
# First, extract the "month" from the date
all_songs_with_month <- all_songs %>%
  mutate(month = month(date)) %>%
  select(title, rank, streams, month)

# TODO: Now, write a code that answers the following questions: 
  # (1) In how many months does each song appear in the data?
  # (2) What is the highest rank that the song achieved in the Spotify charts?
  # (3) In what month did each song "peak" at its highest number of streams?
# You can approach these questions however you want. You will need to include 
# the answers in the caption of the below chart. 


# TODO: Create a multi-line chart. Customize the colors, title, and save the plot
ggplot(
  data = all_songs, 
  aes(
    x = date, 
    y = streams, 
    color = title
  )
) +
  geom_line(size = 1.1) +
  labs(
    title = "[Your descriptive title here]",
    x = "[Your x-axis title here]",
    y = "[Your y-axis title here]",
    caption = "[Insert your caption, including answering questions (1), (2), and (3) above]"
    color = "Song"
  ) +
  scale_x_continuous(breaks = 1:12) +
  scale_color_manual(values = c(
    "All I Want for Christmas Is You" = "[Pick a color]",
    "[Song 1 Title]" = "[Pick a color]",
    "[Song 2 Title]" = "[Pick a color]"
  )) +
  theme(
    # theme(...) allows us to set options about how the plot looks
    legend.position = "bottom"
  ) +
  scale_x_date(limits = c(as.Date("2021-01-01"), as.Date("2021-12-31"))) # show all 12 months

# TODO: Save your plot
# Replace [your_output_filename.png] with a descriptive filename
ggsave("[your_output_filename.png]", width = 10, height = 6, dpi = 300)

```

### Assignment Response

After creating your multi-line line chart, write a 2-4 sentence interpretation of what you observe. Your response should address:

1. Which two songs did you choose to add to the chart?
2. How do the streaming patterns of your chosen songs compare to the Christmas song?
3. What trends or patterns do you notice? (e.g., steady throughout the year, peaks at certain times, declining, etc.). How are these patterns different from the Christmas song?

## Deliverable

Upload your image file to the corresponding assignment on Brightspace. Include your line chart interpretation (2-4 sentences) in the text box for the submission. Remember to answer the questions in the code comments and include those answers in the caption of your image. 

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
