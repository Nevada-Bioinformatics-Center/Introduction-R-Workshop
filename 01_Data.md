---
title: Working with Data in R
author: "Nevada Bioinformatics Center"
date: "2025-06-12"
output: 
  html_document:
    keep_md: true
    toc: true
    toc_depth: 3
    toc_float: 
      collapsed: false
      smooth_scroll: true
    theme: readable
    highlight: tango
---

## Objectives

- Code in R
- Understand R terms
- Create a reproducible workflow
- Work with built-in R datasets

# Coding in R

You can use R as a command line interface (CLI). A *command* is a way of giving the computer some information to perform a task. For example, like a calculator:



``` r
4 + 2
```

```
## [1] 6
```


``` r
9 / 3
```

```
## [1] 3
```


## How R Views Data

R organizes information into different types of **data structures**. Understanding these structures is key to working effectively with R. Let's explore the main types:

### Single Values (Scalars)
The simplest data structure is a single value:


``` r
# Numbers
my_number <- 42
my_number
```

```
## [1] 42
```

``` r
# Text (character strings)
my_name <- "Nevada Bioinformatics"
my_name
```

```
## [1] "Nevada Bioinformatics"
```

``` r
# Logical values (TRUE/FALSE)
my_logical <- TRUE
my_logical
```

```
## [1] TRUE
```

### Vectors
A **vector** is a collection of values of the same type. Vectors are the building blocks of R:


``` r
# Numeric vector
ages <- c(25, 30, 35, 40)
ages
```

```
## [1] 25 30 35 40
```

``` r
# Character vector
names <- c("Alice", "Bob", "Charlie", "Diana")
names
```

```
## [1] "Alice"   "Bob"     "Charlie" "Diana"
```

``` r
# Logical vector
passed_exam <- c(TRUE, FALSE, TRUE, TRUE)
passed_exam
```

```
## [1]  TRUE FALSE  TRUE  TRUE
```

The `c()` function **c**ombines values into a vector. Notice how we use quotes for text but not for numbers or logical values.

### Data Frames
A **data frame** is like a spreadsheet - it has rows and columns where each column can be a different type of data:


``` r
# Create a simple data frame
student_data <- data.frame(
  name = c("Alice", "Bob", "Charlie"),
  age = c(25, 30, 35),
  passed = c(TRUE, FALSE, TRUE)
)
student_data
```

```
##      name age passed
## 1   Alice  25   TRUE
## 2     Bob  30  FALSE
## 3 Charlie  35   TRUE
```

### Lists
A **list** can hold different types of objects, including other lists:


``` r
# Create a list with different types of data
my_list <- list(
  numbers = c(1, 2, 3),
  text = "Hello World",
  data = student_data
)
my_list
```

```
## $numbers
## [1] 1 2 3
## 
## $text
## [1] "Hello World"
## 
## $data
##      name age passed
## 1   Alice  25   TRUE
## 2     Bob  30  FALSE
## 3 Charlie  35   TRUE
```

### Matrices
A **matrix** is like a data frame but all values must be the same type:


``` r
# Create a 3x3 matrix
my_matrix <- matrix(1:9, nrow = 3, ncol = 3)
my_matrix
```

```
##      [,1] [,2] [,3]
## [1,]    1    4    7
## [2,]    2    5    8
## [3,]    3    6    9
```

## Checking Data Types

R provides functions to check what type of data structure you're working with:


``` r
# Check the type of object
class(ages)         
```

```
## [1] "numeric"
```

``` r
class(names)        
```

```
## [1] "character"
```

``` r
class(student_data)  
```

```
## [1] "data.frame"
```

``` r
# Check the structure
str(student_data)    
```

```
## 'data.frame':	3 obs. of  3 variables:
##  $ name  : chr  "Alice" "Bob" "Charlie"
##  $ age   : num  25 30 35
##  $ passed: logi  TRUE FALSE TRUE
```

``` r
# Check if it's a specific type
is.vector(ages)     
```

```
## [1] TRUE
```

``` r
is.data.frame(ages)  
```

```
## [1] FALSE
```


Understanding data structures helps you:

- **Choose the right approach**: Different functions work with different data types
- **Organize your data**: Knowing which structure fits your data best
- **Read error messages**: Many errors relate to data type mismatches

Let's see this in action:


``` r
# This works - adding numbers
numbers <- c(1, 2, 3, 4)
sum(numbers)
```

```
## [1] 10
```



``` r
# This doesn't work - trying to add text
text <- c("a", "b", "c")
sum(text)  # Would give an error!
```


## Creating and Using Variables

One of the most powerful features of R is the ability to store values in **variables** (also called **objects**). This lets you save your work and reuse it later.

### Assignment Operator

We use the assignment operator `<-` to store values in variables:


``` r
# Store a number in a variable
my_age <- 25
my_age
```

```
## [1] 25
```

``` r
# Store text in a variable
my_name <- "Alex"
my_name
```

```
## [1] "Alex"
```

``` r
# Store the result of a calculation
total_score <- 85 + 92 + 78
total_score
```

```
## [1] 255
```

**Tip**: In RStudio, you can type `<-` quickly by pressing <kbd>Alt</kbd> + <kbd>-</kbd> (PC) or <kbd>Option</kbd> + <kbd>-</kbd> (Mac).

### Using Variables in Calculations

Once you've stored values in variables, you can use them in calculations:


``` r
# Store some values
price_per_item <- 15.50
number_of_items <- 4
tax_rate <- 0.08

# Calculate subtotal
subtotal <- price_per_item * number_of_items
subtotal
```

```
## [1] 62
```

``` r
# Calculate tax
tax_amount <- subtotal * tax_rate
tax_amount
```

```
## [1] 4.96
```

``` r
# Calculate final total
final_total <- subtotal + tax_amount
final_total
```

```
## [1] 66.96
```

### Variables Don't Update Automatically

This is one of the most important concepts to understand when working with variables in R. Unlike spreadsheet programs where cells automatically update when their inputs change, R variables are **static** - they only change when you explicitly tell them to.


**Important**: When you change a variable, other variables that depend on it don't automatically update:


``` r
# Initial calculation
base_price <- 100
discount <- 0.10
discounted_price <- base_price * (1 - discount)
discounted_price
```

```
## [1] 90
```

``` r
# Change the base price
base_price <- 200

# discounted_price is still based on the old value!
discounted_price
```

```
## [1] 90
```

``` r
# You need to recalculate it
discounted_price <- base_price * (1 - discount)
discounted_price
```

```
## [1] 180
```



### Variable Naming Rules

Good variable names make your code easier to understand:


``` r
# Good variable names
student_count <- 30
average_grade <- 87.5
experiment_start_date <- "2024-01-15"

# Less clear variable names (but still valid)
x <- 30
avg <- 87.5
d <- "2024-01-15"
```

**Rules for naming variables:**

- Can contain letters, numbers, dots (.), and underscores (_)
- Cannot start with a number
- Cannot contain spaces
- Case-sensitive (`Age` and `age` are different)
- Avoid using names of existing R functions (like `mean`, `sum`, `data`, `T`, `F`)

### Why Use Variables?

Variables make your code:

- **Readable**: Clear names explain what values represent
- **Reusable**: Calculate once, use many times
- **Maintainable**: Change a value in one place, not throughout your code
- **Less error-prone**: No need to retype the same number multiple times

Try this example:


``` r
# Without variables (hard to read and maintain)
final_grade <- (85 + 92 + 78 + 88) / 4 * 0.6 + 95 * 0.4
final_grade
```

```
## [1] 89.45
```

``` r
# With variables (much clearer!)
exam1 <- 85
exam2 <- 92
exam3 <- 78
exam4 <- 88
final_exam <- 95

exam_average <- (exam1 + exam2 + exam3 + exam4) / 4
exam_weight <- 0.6
final_weight <- 0.4

final_grade <- exam_average * exam_weight + final_exam * final_weight
final_grade
```

```
## [1] 89.45
```


## Functions and Their Arguments

Functions are pre-written pieces of code that perform specific tasks. They're like recipes--you give them ingredients (called **arguments**) and they give you back a result.

### Basic Function Structure

Every function in R follows this pattern:
```
function_name(argument1, argument2, ...)
```
One of the simplest functions is `print()`, which displays text or values to the console.


``` r
# Print a message
print("Hello, world!")
```

```
## [1] "Hello, world!"
```

### Simple Functions

Let's start with some basic math functions:


``` r
# Square root function
sqrt(16)
```

```
## [1] 4
```

``` r
sqrt(25)
```

```
## [1] 5
```

``` r
# Absolute value
abs(-5)
```

```
## [1] 5
```

``` r
abs(3.2)
```

```
## [1] 3.2
```

``` r
# Round numbers
round(3.14159)
```

```
## [1] 3
```

``` r
round(2.718)
```

```
## [1] 3
```

### Functions with Multiple Arguments

Many functions take more than one argument:


``` r
# Round to specific decimal places
round(3.14159, digits = 2)
```

```
## [1] 3.14
```

``` r
round(2.718281, digits = 3)
```

```
## [1] 2.718
```

``` r
# Exclude NA's from mean
test_scores <- c(87, 93, 75, NA, 84)
mean(test_scores, na.rm = TRUE)
```

```
## [1] 84.75
```

### Getting Help with Functions

Before using a function, you can learn about it:


``` r
# Get help on the round function
?round

# See what arguments a function takes
args(round)
```

Let's examine what `args(round)` tells us:

- `x`: the number(s) to round
- `digits`: how many decimal places (default is 0)

### Named vs. Positional Arguments

You can provide arguments in two ways:


``` r
# Positional arguments (order matters)
round(3.14159, 2)
```

```
## [1] 3.14
```

``` r
# Named arguments (order doesn't matter)
round(digits = 2, x = 3.14159)
```

```
## [1] 3.14
```

``` r
round(x = 3.14159, digits = 2)
```

```
## [1] 3.14
```

**Best practice**: Use names for optional arguments to make your code clearer.

### Functions with Vectors

Most R functions work with vectors (multiple values):


``` r
# Create a vector of numbers
numbers <- c(1.167, 2.873, 3.994, 4.225, 5.861)
numbers
```

```
## [1] 1.167 2.873 3.994 4.225 5.861
```

``` r
# Apply functions to the entire vector
round(numbers)
```

```
## [1] 1 3 4 4 6
```

``` r
round(numbers, digits = 1)
```

```
## [1] 1.2 2.9 4.0 4.2 5.9
```

``` r
sqrt(numbers)
```

```
## [1] 1.080278 1.694993 1.998499 2.055480 2.420950
```

### Statistical Functions

R has many built-in statistical functions:


``` r
# Create some sample data
grades <- c(85, 92, 78, 88, 95, 82, 90)
grades
```

```
## [1] 85 92 78 88 95 82 90
```

``` r
# Calculate statistics
mean(grades)        # average
```

```
## [1] 87.14286
```

``` r
median(grades)      # middle value
```

```
## [1] 88
```

``` r
max(grades)         # highest value
```

```
## [1] 95
```

``` r
min(grades)         # lowest value
```

```
## [1] 78
```

``` r
length(grades)      # count of values
```

```
## [1] 7
```

``` r
sum(grades)         # total
```

```
## [1] 610
```

### Functions That Create Data

Some functions create new data structures:


``` r
# Create sequences
seq(1, 10)              # numbers from 1 to 10
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

``` r
seq(1, 10, by = 2)      # every 2nd number from 1 to 10
```

```
## [1] 1 3 5 7 9
```

``` r
seq(0, 1, by = 0.1)     # decimals from 0 to 1
```

```
##  [1] 0.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
```

``` r
# Repeat values  
rep(5, times = 3)       # repeat 5 three times
```

```
## [1] 5 5 5
```

``` r
rep(c(1, 2), times = 4) # repeat the vector 1,2 four times
```

```
## [1] 1 2 1 2 1 2 1 2
```



**The colon operator (`:`)** is a handy shortcut for creating sequences of consecutive integers. It's much faster to type `1:5` than `c(1, 2, 3, 4, 5)` or `seq(1, 5)`.


``` r
# These are all equivalent:
1:5
```

```
## [1] 1 2 3 4 5
```

``` r
c(1, 2, 3, 4, 5)
```

```
## [1] 1 2 3 4 5
```

``` r
seq(1, 5)
```

```
## [1] 1 2 3 4 5
```

``` r
# Colon works in reverse too
10:1                    # counts down: 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

```
##  [1] 10  9  8  7  6  5  4  3  2  1
```


### Combining Functions

You can use the output of one function as input to another:


``` r
# Create data, then calculate
numbers <- c(1, 4, 9, 16, 25)
sqrt_numbers <- sqrt(numbers)
mean_of_sqrt <- mean(sqrt_numbers)
mean_of_sqrt
```

```
## [1] 3
```

``` r
# Or do it all in one line
result <- mean(sqrt(c(1, 4, 9, 16, 25)))
result
```

```
## [1] 3
```

## Exercises

### Exercise 1: Basic Functions
Complete these calculations using R functions:


``` r
# 1. Calculate the square root of 144
# Your code here:

# 2. Round 2.718281828 to 4 decimal places  
# Your code here:

# 3. Find the absolute value of -15.7
# Your code here:
```

### Exercise 2: Working with Vectors
Use this vector for the following exercises:


``` r
test_scores <- c(78, 85, 92, 88, 76, 95, 82, 90, 87, 79)
```


``` r
# 1. Calculate the mean of test_scores
# Your code here:

# 2. Find the highest score
# Your code here:

# 3. Find the lowest score  
# Your code here:

# 4. Count how many scores there are
# Your code here:

# 5. Round the square root of all test scores to 2 digits
# Your code here:
```


### Solutions

<details>
<summary>**Click here to see the solutions**</summary>


``` r
# Exercise 1 Solutions
sqrt(144)                    # 12
round(2.718281828, digits = 4)  # 2.7183
abs(-15.7)                   # 15.7

# Exercise 2 Solutions  
mean(test_scores)            # 85.2
max(test_scores)             # 95
min(test_scores)             # 76
length(test_scores)          # 10
round(sqrt(test_scores), digits = 2)  # rounds the square root of each number 
```

</details>

Now that you understand how functions work, you're ready to start working with real datasets!


# Working with Data

## Built-in R datasets

R comes with many built-in datasets that are perfect for learning and practice. These datasets are already loaded and ready to use - no need to download or import anything!

### Exploring available datasets

To see all available built-in datasets:


``` r
data()  # Shows all available datasets
```

Some popular built-in datasets include:

- **mtcars**: Car performance data (32 cars, 11 variables)
- **iris**: Flower measurements (150 flowers, 5 variables) 
- **airquality**: Air quality measurements in New York
- **PlantGrowth**: Plant growth under different conditions

### Loading and exploring a dataset

Let's work with the **mtcars** dataset:


``` r
# Load the dataset 
# (not necessary for built-in data, but adds it to your Environment in RStudio)
data(mtcars)

# Look at the first few rows
head(mtcars)

# Get basic information about the dataset
str(mtcars)

# Summary statistics
summary(mtcars)

# Get help about the dataset
?mtcars
```

The mtcars dataset contains information about 32 cars from 1974 Motor Trend magazine, including:

- mpg: Miles per gallon
- cyl: Number of cylinders
- hp: Horsepower
- wt: Weight
- And more!

## Exploring our practice dataset

Let's explore the mtcars dataset to get familiar with R:


``` r
# Look at the dataset
mtcars
```

```
##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
```

``` r
# Get dimensions (rows and columns)
dim(mtcars)
```

```
## [1] 32 11
```

``` r
nrow(mtcars)  # number of rows
```

```
## [1] 32
```

``` r
ncol(mtcars)  # number of columns
```

```
## [1] 11
```

``` r
# Get column names
names(mtcars)
```

```
##  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
## [11] "carb"
```

``` r
# Overview of content
head(mtcars) # First few rows
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

``` r
tail(mtcars) # Last few rows
```

```
##                 mpg cyl  disp  hp drat    wt qsec vs am gear carb
## Porsche 914-2  26.0   4 120.3  91 4.43 2.140 16.7  0  1    5    2
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.9  1  1    5    2
## Ford Pantera L 15.8   8 351.0 264 4.22 3.170 14.5  0  1    5    4
## Ferrari Dino   19.7   6 145.0 175 3.62 2.770 15.5  0  1    5    6
## Maserati Bora  15.0   8 301.0 335 3.54 3.570 14.6  0  1    5    8
## Volvo 142E     21.4   4 121.0 109 4.11 2.780 18.6  1  1    4    2
```

``` r
# Summarize
str(mtcars) # Structure
```

```
## 'data.frame':	32 obs. of  11 variables:
##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: num  160 160 108 258 360 ...
##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num  16.5 17 18.6 19.4 17 ...
##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```

``` r
summary(mtcars) # Summary statistics
```

```
##       mpg             cyl             disp             hp       
##  Min.   :10.40   Min.   :4.000   Min.   : 71.1   Min.   : 52.0  
##  1st Qu.:15.43   1st Qu.:4.000   1st Qu.:120.8   1st Qu.: 96.5  
##  Median :19.20   Median :6.000   Median :196.3   Median :123.0  
##  Mean   :20.09   Mean   :6.188   Mean   :230.7   Mean   :146.7  
##  3rd Qu.:22.80   3rd Qu.:8.000   3rd Qu.:326.0   3rd Qu.:180.0  
##  Max.   :33.90   Max.   :8.000   Max.   :472.0   Max.   :335.0  
##       drat             wt             qsec             vs        
##  Min.   :2.760   Min.   :1.513   Min.   :14.50   Min.   :0.0000  
##  1st Qu.:3.080   1st Qu.:2.581   1st Qu.:16.89   1st Qu.:0.0000  
##  Median :3.695   Median :3.325   Median :17.71   Median :0.0000  
##  Mean   :3.597   Mean   :3.217   Mean   :17.85   Mean   :0.4375  
##  3rd Qu.:3.920   3rd Qu.:3.610   3rd Qu.:18.90   3rd Qu.:1.0000  
##  Max.   :4.930   Max.   :5.424   Max.   :22.90   Max.   :1.0000  
##        am              gear            carb      
##  Min.   :0.0000   Min.   :3.000   Min.   :1.000  
##  1st Qu.:0.0000   1st Qu.:3.000   1st Qu.:2.000  
##  Median :0.0000   Median :4.000   Median :2.000  
##  Mean   :0.4062   Mean   :3.688   Mean   :2.812  
##  3rd Qu.:1.0000   3rd Qu.:4.000   3rd Qu.:4.000  
##  Max.   :1.0000   Max.   :5.000   Max.   :8.000
```

## Accessing columns in data frames

Before we start exploring datasets, we need to learn how to access specific parts of our data. Data frames are like spreadsheets - they have rows (observations) and columns (variables). To work with the data effectively, we need to know how to extract specific columns.

### The `$` operator

The `$` operator is R's way of saying "give me this specific column from this data frame." Think of it like pointing to a specific column in a spreadsheet.

**Syntax**: `dataframe_name$column_name`

This extracts the entire column as a vector, which you can then use with functions or store in other variables.


``` r
# Look at specific columns
mtcars$mpg        # miles per gallon
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4
## [16] 10.4 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7
## [31] 15.0 21.4
```

``` r
mtcars$cyl        # number of cylinders
```

```
##  [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4
```

``` r
# Basic statistics
mean(mtcars$mpg)  # average miles per gallon
```

```
## [1] 20.09062
```

``` r
max(mtcars$hp)    # maximum horsepower
```

```
## [1] 335
```

``` r
min(mtcars$wt)    # minimum weight
```

```
## [1] 1.513
```


## Subsetting data frames

**Subsetting** means selecting specific parts of your data - whether that's certain rows, certain columns, or both. This is one of the most powerful features in R because it lets you focus on exactly the data you need for your analysis.

Subsetting is like filtering in a spreadsheet program, but much more flexible and powerful.

### Understanding the bracket notation

Data frames use **bracket notation** `[row, column]` to specify exactly which parts you want:

- **Before the comma**: which rows you want
- **After the comma**: which columns you want
- **Leave blank**: means "give me all of them"

For example:

- `[1, ]` = first row, all columns
- `[, 2]` = all rows, second column  
- `[1:5, c(1,3)]` = first 5 rows, columns 1 and 3

### Selecting columns

We've already seen the `$` operator for selecting single columns. Here are other ways:


``` r
# Select single columns
mtcars$mpg                    # Using $
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4
## [16] 10.4 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7
## [31] 15.0 21.4
```

``` r
mtcars[, "mpg"]              # Using brackets with column name
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4
## [16] 10.4 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7
## [31] 15.0 21.4
```

``` r
mtcars[, 1]                  # Using brackets with column position
```

```
##  [1] 21.0 21.0 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 17.8 16.4 17.3 15.2 10.4
## [16] 10.4 14.7 32.4 30.4 33.9 21.5 15.5 15.2 13.3 19.2 27.3 26.0 30.4 15.8 19.7
## [31] 15.0 21.4
```

``` r
# Select multiple columns
mtcars[, c("mpg", "hp")]     # Multiple columns by name
```

```
##                      mpg  hp
## Mazda RX4           21.0 110
## Mazda RX4 Wag       21.0 110
## Datsun 710          22.8  93
## Hornet 4 Drive      21.4 110
## Hornet Sportabout   18.7 175
## Valiant             18.1 105
## Duster 360          14.3 245
## Merc 240D           24.4  62
## Merc 230            22.8  95
## Merc 280            19.2 123
## Merc 280C           17.8 123
## Merc 450SE          16.4 180
## Merc 450SL          17.3 180
## Merc 450SLC         15.2 180
## Cadillac Fleetwood  10.4 205
## Lincoln Continental 10.4 215
## Chrysler Imperial   14.7 230
## Fiat 128            32.4  66
## Honda Civic         30.4  52
## Toyota Corolla      33.9  65
## Toyota Corona       21.5  97
## Dodge Challenger    15.5 150
## AMC Javelin         15.2 150
## Camaro Z28          13.3 245
## Pontiac Firebird    19.2 175
## Fiat X1-9           27.3  66
## Porsche 914-2       26.0  91
## Lotus Europa        30.4 113
## Ford Pantera L      15.8 264
## Ferrari Dino        19.7 175
## Maserati Bora       15.0 335
## Volvo 142E          21.4 109
```

``` r
mtcars[, c(1, 4)]            # Multiple columns by position
```

```
##                      mpg  hp
## Mazda RX4           21.0 110
## Mazda RX4 Wag       21.0 110
## Datsun 710          22.8  93
## Hornet 4 Drive      21.4 110
## Hornet Sportabout   18.7 175
## Valiant             18.1 105
## Duster 360          14.3 245
## Merc 240D           24.4  62
## Merc 230            22.8  95
## Merc 280            19.2 123
## Merc 280C           17.8 123
## Merc 450SE          16.4 180
## Merc 450SL          17.3 180
## Merc 450SLC         15.2 180
## Cadillac Fleetwood  10.4 205
## Lincoln Continental 10.4 215
## Chrysler Imperial   14.7 230
## Fiat 128            32.4  66
## Honda Civic         30.4  52
## Toyota Corolla      33.9  65
## Toyota Corona       21.5  97
## Dodge Challenger    15.5 150
## AMC Javelin         15.2 150
## Camaro Z28          13.3 245
## Pontiac Firebird    19.2 175
## Fiat X1-9           27.3  66
## Porsche 914-2       26.0  91
## Lotus Europa        30.4 113
## Ford Pantera L      15.8 264
## Ferrari Dino        19.7 175
## Maserati Bora       15.0 335
## Volvo 142E          21.4 109
```

### Selecting rows

You can select specific rows using brackets:


``` r
# Select specific rows
mtcars[1, ]                  # First row, all columns
```

```
##           mpg cyl disp  hp drat   wt  qsec vs am gear carb
## Mazda RX4  21   6  160 110  3.9 2.62 16.46  0  1    4    4
```

``` r
mtcars[1:5, ]                # First 5 rows, all columns
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
```

``` r
mtcars[c(1, 3, 5), ]         # Rows 1, 3, and 5, all columns
```

```
##                    mpg cyl disp  hp drat   wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.62 16.46  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.32 18.61  1  1    4    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.44 17.02  0  0    3    2
```

### Selecting rows and columns together


``` r
# Select specific rows and columns
mtcars[1:5, c("mpg", "hp")]  # First 5 rows, mpg and hp columns
```

```
##                    mpg  hp
## Mazda RX4         21.0 110
## Mazda RX4 Wag     21.0 110
## Datsun 710        22.8  93
## Hornet 4 Drive    21.4 110
## Hornet Sportabout 18.7 175
```

``` r
mtcars[1:3, 1:3]             # First 3 rows and first 3 columns
```

```
##                mpg cyl disp
## Mazda RX4     21.0   6  160
## Mazda RX4 Wag 21.0   6  160
## Datsun 710    22.8   4  108
```

### Conditional subsetting

This is where data frames get really powerful - you can select rows based on conditions:


**How it works**: You create a logical test that returns `TRUE` or `FALSE` for each row, then R keeps only the rows where the test is `TRUE`.

#### Comparison operators

First, let's understand the comparison operators you can use:


``` r
# Basic comparison operators:
# ==  equal to (note: two equals signs!)
# !=  not equal to  
# >   greater than
# <   less than
# >=  greater than or equal to
# <=  less than or equal to

# Let's see these in action with a simple example
test_values <- c(5, 10, 15, 20)
test_values
```

```
## [1]  5 10 15 20
```

``` r
# Which values are greater than 10?
test_values > 10  # Returns TRUE/FALSE for each value
```

```
## [1] FALSE FALSE  TRUE  TRUE
```

``` r
# Which values equal exactly 15?
test_values == 15  # Returns TRUE/FALSE for each value
```

```
## [1] FALSE FALSE  TRUE FALSE
```

**Important**: Use `==` (two equals) for comparison, not `=` (one equals). Single `=` is for assignment, like `<-`.

#### Basic conditional subsetting

Now let's apply this to data frames:


``` r
# Cars with more than 20 miles per gallon
# First, let's see the logical test
mtcars$mpg > 20  # TRUE/FALSE for each car
```

```
##  [1]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE
## [13] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
## [25] FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
```

``` r
# Now use it to subset
high_mpg_cars <- mtcars[mtcars$mpg > 20, ]
head(high_mpg_cars)
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4      21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag  21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710     22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive 21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
## Merc 240D      24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
## Merc 230       22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
```

``` r
# Cars with exactly 4 cylinders
four_cyl_cars <- mtcars[mtcars$cyl == 4, ]
nrow(four_cyl_cars)  # How many 4-cylinder cars?
```

```
## [1] 11
```

#### Logical operators for multiple conditions

You can combine multiple conditions using logical operators:

- **`&`** means "AND" - both conditions must be true
- **`|`** means "OR" - at least one condition must be true  
- **`!`** means "NOT" - reverses TRUE/FALSE


``` r
# AND operator (&): Both conditions must be true
# Cars with high mpg AND low weight
efficient_cars <- mtcars[mtcars$mpg > 25 & mtcars$wt < 3, ]
efficient_cars
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
## Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
## Fiat X1-9      27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
## Porsche 914-2  26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
```

``` r
nrow(efficient_cars)  # How many cars meet both criteria?
```

```
## [1] 6
```

``` r
# OR operator (|): At least one condition must be true
# Cars that are either very powerful OR very efficient
powerful_or_efficient <- mtcars[mtcars$hp > 200 | mtcars$mpg > 25, ]
nrow(powerful_or_efficient)
```

```
## [1] 13
```

``` r
# Let's see what each condition captures separately:
sum(mtcars$hp > 200)   # Cars with >200 hp
```

```
## [1] 7
```

``` r
sum(mtcars$mpg > 25)   # Cars with >25 mpg
```

```
## [1] 6
```

``` r
# The OR condition captures cars that meet either criterion

# NOT operator (!): Reverse the condition
# Cars that are NOT 4-cylinder
not_four_cyl <- mtcars[!(mtcars$cyl == 4), ]
# This is the same as:
not_four_cyl_alt <- mtcars[mtcars$cyl != 4, ]
```

#### Complex conditions

You can create more complex conditions by combining multiple operators:


``` r
# Cars with good fuel economy (>20 mpg) that are either lightweight (<3000 lbs) 
# OR have low horsepower (<100 hp)
complex_condition <- mtcars[mtcars$mpg > 20 & (mtcars$wt < 3 | mtcars$hp < 100), ]
head(complex_condition)
```

```
##                mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4     21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag 21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710    22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
## Merc 240D     24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
## Merc 230      22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
## Fiat 128      32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
```

``` r
# Note the parentheses! They control the order of operations
# Without parentheses: mpg > 20 & wt < 3 | hp < 100
# Would mean: (mpg > 20 & wt < 3) OR hp < 100

# With parentheses: mpg > 20 & (wt < 3 | hp < 100)  
# Means: mpg > 20 AND (wt < 3 OR hp < 100)
```

#### Working with text/factor conditions

You can also use conditions with text or factor data:


``` r
# Using the iris dataset
data(iris)

# Flowers of a specific species
setosa_flowers <- iris[iris$Species == "setosa", ]
head(setosa_flowers)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

``` r
# Flowers that are NOT setosa
not_setosa <- iris[iris$Species != "setosa", ]
head(not_setosa)
```

```
##    Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
## 51          7.0         3.2          4.7         1.4 versicolor
## 52          6.4         3.2          4.5         1.5 versicolor
## 53          6.9         3.1          4.9         1.5 versicolor
## 54          5.5         2.3          4.0         1.3 versicolor
## 55          6.5         2.8          4.6         1.5 versicolor
## 56          5.7         2.8          4.5         1.3 versicolor
```

``` r
# Multiple species using OR
setosa_or_versicolor <- iris[iris$Species == "setosa" | iris$Species == "versicolor", ]
head(setosa_or_versicolor)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

#### The `%in%` operator

When you want to check if values match any item in a list, use `%in%`:


``` r
# Instead of writing long OR statements:
# iris[iris$Species == "setosa" | iris$Species == "versicolor", ]

# Use %in% for cleaner code:
selected_species <- iris[iris$Species %in% c("setosa", "versicolor"), ]
head(selected_species)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

``` r
# This is especially useful with numbers too:
# Cars with 4 or 8 cylinders
common_cylinders <- mtcars[mtcars$cyl %in% c(4, 8), ]
table(common_cylinders$cyl)
```

```
## 
##  4  8 
## 11 14
```

### Useful functions for subsetting

While bracket notation is powerful, R provides some specialized functions that make certain tasks easier.

#### `which()` - Finding positions

The `which()` function tells you the **positions** (row numbers) where conditions are true, rather than returning `TRUE`/`FALSE` values.


``` r
# Compare logical indexing vs which()
mtcars$cyl > 6           # Returns TRUE/FALSE for each car
```

```
##  [1] FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE
## [13]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
## [25]  TRUE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE
```

``` r
which(mtcars$cyl > 6)    # Returns the row numbers where it's TRUE
```

```
##  [1]  5  7 12 13 14 15 16 17 22 23 24 25 29 31
```

``` r
# Use the positions to get specific rows
high_cyl_positions <- which(mtcars$cyl > 6)
mtcars[high_cyl_positions, c("mpg", "cyl", "hp")]
```

```
##                      mpg cyl  hp
## Hornet Sportabout   18.7   8 175
## Duster 360          14.3   8 245
## Merc 450SE          16.4   8 180
## Merc 450SL          17.3   8 180
## Merc 450SLC         15.2   8 180
## Cadillac Fleetwood  10.4   8 205
## Lincoln Continental 10.4   8 215
## Chrysler Imperial   14.7   8 230
## Dodge Challenger    15.5   8 150
## AMC Javelin         15.2   8 150
## Camaro Z28          13.3   8 245
## Pontiac Firebird    19.2   8 175
## Ford Pantera L      15.8   8 264
## Maserati Bora       15.0   8 335
```

#### `which.max()` and `which.min()` - Finding extremes

These find the position of the maximum or minimum value - useful for finding "record holders."


``` r
# Find the car with highest mpg
which.max(mtcars$mpg)                # Position number
```

```
## [1] 20
```

``` r
mtcars[which.max(mtcars$mpg), ]      # The actual car data
```

```
##                 mpg cyl disp hp drat    wt qsec vs am gear carb
## Toyota Corolla 33.9   4 71.1 65 4.22 1.835 19.9  1  1    4    1
```

``` r
rownames(mtcars)[which.max(mtcars$mpg)]  # Just the car name
```

```
## [1] "Toyota Corolla"
```

``` r
# Find the heaviest car
mtcars[which.max(mtcars$wt), c("wt", "mpg", "hp")]
```

```
##                        wt  mpg  hp
## Lincoln Continental 5.424 10.4 215
```

**When to use each:**

- Use regular subsetting when you want all rows meeting a condition
- Use `which()` when you need specific row positions  
- Use `which.max()`/`which.min()` when you want the single best/worst case

## Factors and levels

**Factors** are R's way of handling categorical data (like categories or groups). They look like text but are stored differently, which makes them useful for analysis and plotting.

**Factors** might seem confusing at first, but they're incredibly useful for working with categorical data. In real-world data analysis, you often have variables that represent categories rather than numbers - things like:

- Survey responses (agree/disagree/neutral)
- Treatment groups (control/treatment)
- Geographic regions (north/south/east/west)
- Product ratings (poor/fair/good/excellent)

### What makes factors special?

Regular text (character) data in R is just text. But factors are **categorical variables** - they represent a limited set of possible values (called **levels**). This distinction is important because:

1. **Factors have a specific order** - you can control how categories appear in plots and tables
2. **Statistical functions expect factors** - most analysis functions work better with proper categorical data
3. **Factors save memory** - R stores each unique category name only once

Let's see this in action:


``` r
# Create a simple factor
car_sizes <- factor(c("small", "medium", "large", "small", "large", "medium"))
car_sizes
```

```
## [1] small  medium large  small  large  medium
## Levels: large medium small
```

``` r
# Look at the levels (categories)
levels(car_sizes)
```

```
## [1] "large"  "medium" "small"
```

``` r
# See the structure
str(car_sizes)
```

```
##  Factor w/ 3 levels "large","medium",..: 3 2 1 3 1 2
```

Notice how R shows the levels and stores the data as numbers behind the scenes!

### Working with the iris dataset

Let's use the iris dataset which has a factor column:


``` r
# Load and examine iris
data(iris)
head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

``` r
str(iris)
```

```
## 'data.frame':	150 obs. of  5 variables:
##  $ Sepal.Length: num  5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
##  $ Sepal.Width : num  3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
##  $ Petal.Length: num  1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
##  $ Petal.Width : num  0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
##  $ Species     : Factor w/ 3 levels "setosa","versicolor",..: 1 1 1 1 1 1 1 1 1 1 ...
```

``` r
# The Species column is a factor
iris$Species
```

```
##   [1] setosa     setosa     setosa     setosa     setosa     setosa    
##   [7] setosa     setosa     setosa     setosa     setosa     setosa    
##  [13] setosa     setosa     setosa     setosa     setosa     setosa    
##  [19] setosa     setosa     setosa     setosa     setosa     setosa    
##  [25] setosa     setosa     setosa     setosa     setosa     setosa    
##  [31] setosa     setosa     setosa     setosa     setosa     setosa    
##  [37] setosa     setosa     setosa     setosa     setosa     setosa    
##  [43] setosa     setosa     setosa     setosa     setosa     setosa    
##  [49] setosa     setosa     versicolor versicolor versicolor versicolor
##  [55] versicolor versicolor versicolor versicolor versicolor versicolor
##  [61] versicolor versicolor versicolor versicolor versicolor versicolor
##  [67] versicolor versicolor versicolor versicolor versicolor versicolor
##  [73] versicolor versicolor versicolor versicolor versicolor versicolor
##  [79] versicolor versicolor versicolor versicolor versicolor versicolor
##  [85] versicolor versicolor versicolor versicolor versicolor versicolor
##  [91] versicolor versicolor versicolor versicolor versicolor versicolor
##  [97] versicolor versicolor versicolor versicolor virginica  virginica 
## [103] virginica  virginica  virginica  virginica  virginica  virginica 
## [109] virginica  virginica  virginica  virginica  virginica  virginica 
## [115] virginica  virginica  virginica  virginica  virginica  virginica 
## [121] virginica  virginica  virginica  virginica  virginica  virginica 
## [127] virginica  virginica  virginica  virginica  virginica  virginica 
## [133] virginica  virginica  virginica  virginica  virginica  virginica 
## [139] virginica  virginica  virginica  virginica  virginica  virginica 
## [145] virginica  virginica  virginica  virginica  virginica  virginica 
## Levels: setosa versicolor virginica
```

``` r
levels(iris$Species)
```

```
## [1] "setosa"     "versicolor" "virginica"
```


Factors can ensure consistent categories (no typos like "setosa" vs "Setosa").


``` r
# Count occurrences of each species
table(iris$Species)
```

```
## 
##     setosa versicolor  virginica 
##         50         50         50
```

``` r
# Create a simple bar plot
barplot(table(iris$Species))
```

![](01_Data_files/figure-html/unnamed-chunk-47-1.png)<!-- -->


Let's create a factor:


``` r
# Create character data
colors <- c("red", "blue", "green", "red", "blue")
colors
```

```
## [1] "red"   "blue"  "green" "red"   "blue"
```

``` r
# Convert to factor
colors_factor <- as.factor(colors)
colors_factor
```

```
## [1] red   blue  green red   blue 
## Levels: blue green red
```

``` r
levels(colors_factor)  # Notice alphabetical order
```

```
## [1] "blue"  "green" "red"
```

### Handling missing data with factors

Let's create an example with missing data:


``` r
# Create data with missing values
survey_responses <- c("agree", "disagree", "neutral", NA, "agree", NA, "disagree")
survey_responses
```

```
## [1] "agree"    "disagree" "neutral"  NA         "agree"    NA         "disagree"
```

``` r
# Convert to factor
survey_factor <- as.factor(survey_responses)
survey_factor
```

```
## [1] agree    disagree neutral  <NA>     agree    <NA>     disagree
## Levels: agree disagree neutral
```

``` r
levels(survey_factor)  # NA is not a level
```

```
## [1] "agree"    "disagree" "neutral"
```

``` r
# Count responses
table(survey_factor)
```

```
## survey_factor
##    agree disagree  neutral 
##        2        2        1
```

``` r
table(survey_factor, useNA = "ifany")  # Include NAs in count
```

```
## survey_factor
##    agree disagree  neutral     <NA> 
##        2        2        1        2
```

Or we can replace NA's with `is.na()`: 


``` r
# Replace NAs with "unknown"
survey_responses[is.na(survey_responses)] <- "unknown"
survey_responses
```

```
## [1] "agree"    "disagree" "neutral"  "unknown"  "agree"    "unknown"  "disagree"
```

``` r
# Convert to factor
survey_clean <- as.factor(survey_responses)
survey_clean
```

```
## [1] agree    disagree neutral  unknown  agree    unknown  disagree
## Levels: agree disagree neutral unknown
```

``` r
levels(survey_clean)
```

```
## [1] "agree"    "disagree" "neutral"  "unknown"
```

### Reordering factor levels

Factors are automatically leveled in alphabetical order. But we can change that by specifying the order:



``` r
# Create a factor with logical order
sizes <- factor(c("small", "large", "medium", "small", "medium", "large"))
levels(sizes)  # Alphabetical order by default
```

```
## [1] "large"  "medium" "small"
```

``` r
# Reorder levels logically
sizes_ordered <- factor(sizes, levels = c("small", "medium", "large"))
levels(sizes_ordered)
```

```
## [1] "small"  "medium" "large"
```


### Working with Data Sets

Here's an example of categorizing your data set:


``` r
# Check data structure
str(mtcars)
```

```
## 'data.frame':	32 obs. of  11 variables:
##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: num  160 160 108 258 360 ...
##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num  16.5 17 18.6 19.4 17 ...
##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```

``` r
# We want our transmission type (am) to be a factor with manual first
# First, let's see what the am variable looks like
table(mtcars$am)  # 0 = automatic, 1 = manual
```

```
## 
##  0  1 
## 19 13
```

``` r
# Convert to factor with descriptive labels and manual first
mtcars$am <- factor(mtcars$am, 
                   levels = c(1, 0),  # manual first, then automatic
                   labels = c("manual", "automatic"))

# Check the result
str(mtcars$am)
```

```
##  Factor w/ 2 levels "manual","automatic": 1 1 1 2 2 2 2 2 2 2 ...
```

``` r
levels(mtcars$am)
```

```
## [1] "manual"    "automatic"
```

``` r
table(mtcars$am)
```

```
## 
##    manual automatic 
##        13        19
```

``` r
# Simple plot
barplot(table(mtcars$am))
```

![](01_Data_files/figure-html/unnamed-chunk-52-1.png)<!-- -->


## Basic plotting in R

R has built-in functions for creating simple plots. 

### Scatter plots with `plot()`

The `plot()` function creates scatter plots to show relationships between two variables. You can customize the plot with titles and axis labels too.


``` r
# Basic scatter plot
plot(mtcars$hp, mtcars$mpg)
```

![](01_Data_files/figure-html/unnamed-chunk-53-1.png)<!-- -->

``` r
# Add labels
plot(mtcars$hp, mtcars$mpg,
     main = "Fuel Efficiency vs Horsepower", # Main title
     xlab = "Horsepower",                    # X-axis label
     ylab = "Miles per Gallon")              # Y-axis label
```

![](01_Data_files/figure-html/unnamed-chunk-53-2.png)<!-- -->

### Bar plots with `barplot()`

The `barplot()` function creates bar charts, often used with `table()` to show counts:


``` r
# Count how many cars have each number of cylinders
table(mtcars$cyl)
```

```
## 
##  4  6  8 
## 11  7 14
```

``` r
# Create a bar plot of the counts
barplot(table(mtcars$cyl))
```

![](01_Data_files/figure-html/unnamed-chunk-54-1.png)<!-- -->

``` r
# Add a title
barplot(table(mtcars$cyl),
        main = "Number of Cars by Cylinder Count",
        xlab = "Cylinders",
        ylab = "Count")
```

![](01_Data_files/figure-html/unnamed-chunk-54-2.png)<!-- -->

These basic plots are great for quick data exploration. 


## Exercise

**How to approach these exercises**:

- Try each one on your own first
- Don't worry about making mistakes - that's how you learn!
- If you get stuck, re-read the relevant section above
- Check your answers against the solutions, but try not to peek too early
- Remember: there's often more than one correct way to solve a problem in R

**Tip**: Type out the code rather than copy-pasting. This helps you remember the syntax better.

### Data Analysis Practice

Let's practice what we've learned by doing a mini data analysis:

1. **Create a new R script** called "mtcars_analysis.R" in your scripts folder
2. **Write a comment** at the top describing what the script does
3. **Load and explore the mtcars dataset**:
   - Load the data with `data(mtcars)`
   - Look at the first 6 rows
   - Check the structure of the data
   - Get summary statistics

4. **Answer these specific questions using R code**:
   - How many cars have more than 6 cylinders?
   - What is the average horsepower of cars with automatic transmission? (Hint: `am == 0` means automatic)
   - Which car has the best fuel efficiency (highest mpg)?
   - Create a subset of cars that have both high fuel efficiency (>25 mpg) AND are lightweight (<3 weight units)

5. **Work with factors**:
   - Convert the `gear` variable to a factor
   - Count how many cars have each number of gears
   - Create a simple bar plot showing the gear distribution

6. **Save your script** and make sure it runs from top to bottom without errors

<details>
<summary>**Click here to see the solutions**</summary>


``` r
# mtcars_analysis.R
# Analysis of car performance data from the mtcars dataset
# Author: [Your name]
# Date: [Today's date]

# Load and explore the dataset
data(mtcars)
head(mtcars)
str(mtcars)
summary(mtcars)

# Question 1: How many cars have more than 6 cylinders?
cars_over_6_cyl <- mtcars[mtcars$cyl > 6, ]
nrow(cars_over_6_cyl)
# Alternative: sum(mtcars$cyl > 6)

# Question 2: Average horsepower of automatic cars
automatic_cars <- mtcars[mtcars$am == 0, ]
mean(automatic_cars$hp)
# Alternative: mean(mtcars$hp[mtcars$am == 0])

# Question 3: Car with best fuel efficiency
best_mpg_car <- mtcars[which.max(mtcars$mpg), ]
rownames(best_mpg_car)
best_mpg_car$mpg

# Question 4: Efficient and lightweight cars
efficient_light <- mtcars[mtcars$mpg > 25 & mtcars$wt < 3, ]
nrow(efficient_light)
rownames(efficient_light)

# Question 5: Work with factors
# Convert gear to factor
mtcars$gear <- as.factor(mtcars$gear)

# Count cars by gear
table(mtcars$gear)

# Create bar plot
barplot(table(mtcars$gear),
        main = "Number of Cars by Gear Count",
        xlab = "Number of Gears",
        ylab = "Count")
```

</details>

### Bonus Challenge (Optional)

If you finish early, try this additional challenge:

- Find the car with the highest horsepower-to-weight ratio
- Create a new variable called `efficiency_category` that labels cars as "High" (>25 mpg), "Medium" (15-25 mpg), or "Low" (<15 mpg)
- Count how many cars fall into each efficiency category

<details>
<summary>**Bonus solutions**</summary>


``` r
# Bonus Challenge Solutions

# 1. Highest horsepower-to-weight ratio
mtcars$hp_to_weight <- mtcars$hp / mtcars$wt
best_ratio_car <- mtcars[which.max(mtcars$hp_to_weight), ]
rownames(best_ratio_car)
best_ratio_car$hp_to_weight

# 2. Create efficiency categories using logical indexing
# First create the variable with a default value
mtcars$efficiency_category <- "Low"  # Start with all cars as "Low"

# Then update specific cars based on conditions
mtcars$efficiency_category[mtcars$mpg >= 15 & mtcars$mpg <= 25] <- "Medium"
mtcars$efficiency_category[mtcars$mpg > 25] <- "High"

# Convert to factor with logical order
mtcars$efficiency_category <- factor(mtcars$efficiency_category, 
                                   levels = c("Low", "Medium", "High"))


# 3. Count cars in each category
table(mtcars$efficiency_category)
```

</details>


## Getting help

- **In R**: Use `?function_name` to get help on any function
- **RStudio**: Press F1 while cursor is on a function name
- **Online**: Stack Overflow, RStudio Community, R documentation
- **Error messages**: Read them carefully - they often tell you exactly what's wrong!
- **For datasets**: Use `?dataset_name` (e.g., `?mtcars`) to learn about built-in datasets

## Key takeaways

- **R fundamentals**: Use R as a calculator, store values with `<-`, understand data structures (vectors, data frames, lists, matrices)
- **Functions and arguments**: Use built-in functions like `mean()`, `sum()`, `sqrt()` with named/positional arguments, get help with `?function_name`
- **Data exploration**: Access built-in datasets with `data()`, explore with `head()`, `str()`, `summary()`, extract columns with `$`
- **Data subsetting**: Select rows/columns with bracket notation `[row, column]`, filter with conditions using `==`, `>`, `&`, `|`, find extremes with `which.max()`
- **Factors for categories**: Convert text to factors with `as.factor()`, control level order, handle missing data, essential for plotting and analysis
- **Best practices**: Write code in scripts with comments `#`, use descriptive variable names, organize projects, read error messages carefully

$~$
