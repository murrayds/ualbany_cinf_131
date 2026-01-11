# Assignment 1 - Hello, World!

## Overview
This assignment is meant as a check to ensure that you have R, RStudio, and Tidyverse up and running on your local computer, and that you can run basic calculations. 
This is a “Hello, World!” assignment. When learning a new programming language, it is tradition that the first thing you learn is how to make the language output “Hello, World!”. 

## Instructions
In RStudio, create a new scrit (File -> New File -> R Script). Below is an assignment template. Copy this assignment template into the new file that you just created. 

You will run each line of this code one-at-a-time. To do so, highlight the line of code, and click "Run" in the upper-right-hand corner of the RStudio script pane. 
Multiple lines can be executed at once by highlighting them all together, and clicking "Run". 

Many lines of code below are incomplete. These are sections marked in brackets, like  "[Your name]". 
Where you see this, you will need to replace it with the required information. 
If you do not do this, then the line of code will not execute - you will receive an error from RStudio.
For example, consdier the following example line:

```
name <- "[Your name]"
`

I would replace this with the following:

```r
name <- "Dakota Murray"
```

Note that the brackeet characters ("[" and "]") must be removed, but that the quotation marks must stay. 

After you have succesfully ran avery line individually, run the entire script at once. 
To do so, select all lines of code in the file (using the keys "ctrl + a" or "cmd + a") and then click run. 

Save the file and give it an identifiable name. It should be called something like `cinf131_assignment1.R`. 

```r
# Week 1 Assignment: Getting Started with R

# Load tidyverse (this confirms it's installed)
# If you receive an error, see the `troubleshooting` section in the assignment description.
library(tidyverse)

# Basic calculations
[Your age] * 12

# Add any two numbers you like

# Addition
[Number 1] + [Number 2]

# Subtraction
[Number 1] - [Number 2]

# Multiplication
[Number 1] * [Number 2]

# Division
[Number 1] / [Number 2]

# Create a variable, variables store values that we can use later
# Be sure to check the "environment" pane in RStudio after you create the variable!
my_favorite_number <- [any number]
my_favorite_number

# Multiply your favorite number by 10
# Once created, we can reference the variable using its name
my_favorite_number * 10

# Vectors
# R uses "vectors" allowing us to make lists of numbers or other data.
# A vector is created by using the character "c(...,...,...)", where values in the parentheses are separated by commas. 
my_numbers <- c([Number], [Number], [Number], [Number], [Number])

# Hello, World!
print("Hello! My name is [Your Name] and R is working!")
```

### Assignment response
Describe any past experience you have had with programming. It could be anything at all, such as learning `scratch` in elementary school to past courses at the university. 
If you have experience programming, is there anything different you notice about R compared to other programming languages?
If you don't have experience programming, then what is your first impression of it from this script? Is it what you expected?

Write a 2-4 sentence response to this prompt. This will be submitted along with the script. 


## Deliverable
Upload the file containing this script to the correponding assignment on Brightspace. Include the assignment response in the text box for the submission. 


## Troubleshooting
The following are common errors that you might encounter while doing this assignment

**`"Error in library(tidyverse): there is no package called 'tidyverse'"`**

You need to install tidyverse first. In the Console (bottom-left), type:

```r
install.packages("tidyverse")
```

Press Enter and wait for it to finish (may take a few minutes). Then try running your script again.

**`"Error: unexpected '['"`**

This means you forgot to replace something in [brackets] with your own value! Check through the code and remove any remaining brackets ("[" and "])

**`Error: object 'my_favorite_number' not found`**

This means that you are trying to reference a variable but the variable was never created. You likely ran the code in the wrong order. Run the preceeding line that creates the variable:

```r
my_favorite_number <- [your number]
```

Then, run the following line. The variable should be successfully created. 

