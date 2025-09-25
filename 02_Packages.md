---
title: "Packages for Data Transformation"
author: "Nevada Bioinformatics Center"
date: "2025-09-25"
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



## Introduction

In this lesson, we'll learn about R packages that make data manipulation easier and more intuitive. While base R is powerful, packages like `dplyr` and `tidyr` provide functions that are specifically designed for common data analysis tasks.

Packages are like toolboxes - base R gives you basic tools, but specialized packages give you power tools that make specific jobs much easier and faster.

## R packages

R packages are collections of functions, data, and documentation that extend R's capabilities. The `tidyverse` is a collection of packages designed to work together seamlessly for data science tasks.

### Installing and loading packages

Before we can use a package, we need to install it (once) and load it (every session):


``` r
# Install the tidyverse (only need to do this once)
install.packages("tidyverse")
```


## What is the tidyverse?

The **tidyverse** is a collection of R packages designed to make data science tasks easier, more consistent, and more readable. These packages are built to work together and share a common philosophy and grammar.

Some of the most important tidyverse packages are:

- **dplyr**: for data manipulation (filtering, selecting, summarizing, etc.)
- **tidyr**: for reshaping and tidying data
- **ggplot2**: for data visualization
- **readr**: for reading data files (like CSVs)
- **tibble**: for modern, user-friendly data frames
- **stringr**: for working with text (strings)
- **forcats**: for working with categorical data (factors)

All tidyverse packages use a similar style:
- They work with **tibbles** (a modern version of data frames)
- They use **verbs** (functions) like `select()`, `filter()`, `mutate()`, and `summarize()` to describe what you want to do with your data
- They use the **pipe operator** (`%>%`) to chain together multiple steps in a readable way

**Why learn the tidyverse?**  
Once you learn the core tidyverse verbs and the pipe operator, you can use them across almost all tidyverse packages. This makes it much easier to learn new packages and work with data in a consistent way.

> **Tip:** The tidyverse is not just for advanced users—it's designed to make R easier and more intuitive for everyone!

---

Now, let's look at some of the most useful tidyverse functions for data manipulation, starting with `dplyr`.


``` r
# Load tidyverse for this session
library(tidyverse)

# Load our practice data
data(mtcars)
data(iris)
```


## Learning `dplyr`

![](fig/dplyr.png)

`dplyr` provides a grammar of data manipulation. It gives us a set of functions that help us solve the most common data manipulation challenges.

The main `dplyr` functions are:

- `select()` - pick columns
- `filter()` - pick rows
- `mutate()` - create new columns
- `arrange()` - reorder rows
- `group_by()` - group data for analysis
- `summarize()` - calculate summary statistics

Let's explore each one with examples.

### `select()` - Choosing columns

When you work with data, you often have tables (data frames) with many columns, but you only need to focus on a few for your analysis. The `select()` function from `dplyr` helps you easily pick out just the columns you want to keep.

**Why use `select()`?**
- To simplify your data and focus only on the variables you care about
- To make your code and results easier to read
- To avoid mistakes by removing unnecessary columns

**How does it work?**
You tell `select()` which columns you want, and it gives you a new data frame with just those columns. You can specify columns by their names or by their positions.

For example, if you have a data frame with 10 columns but only want to look at "mpg" and "hp", you can use `select()` to keep just those two.

Now, let's see some examples:


``` r
# Look at the original mtcars data
head(mtcars)
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
# Select just a few columns
mtcars_simple <- select(mtcars, mpg, hp, wt)
head(mtcars_simple)
```

```
##                    mpg  hp    wt
## Mazda RX4         21.0 110 2.620
## Mazda RX4 Wag     21.0 110 2.875
## Datsun 710        22.8  93 2.320
## Hornet 4 Drive    21.4 110 3.215
## Hornet Sportabout 18.7 175 3.440
## Valiant           18.1 105 3.460
```

``` r
# Select columns by position
select(mtcars, 1:3)
```

```
##                      mpg cyl  disp
## Mazda RX4           21.0   6 160.0
## Mazda RX4 Wag       21.0   6 160.0
## Datsun 710          22.8   4 108.0
## Hornet 4 Drive      21.4   6 258.0
## Hornet Sportabout   18.7   8 360.0
## Valiant             18.1   6 225.0
## Duster 360          14.3   8 360.0
## Merc 240D           24.4   4 146.7
## Merc 230            22.8   4 140.8
## Merc 280            19.2   6 167.6
## Merc 280C           17.8   6 167.6
## Merc 450SE          16.4   8 275.8
## Merc 450SL          17.3   8 275.8
## Merc 450SLC         15.2   8 275.8
## Cadillac Fleetwood  10.4   8 472.0
## Lincoln Continental 10.4   8 460.0
## Chrysler Imperial   14.7   8 440.0
## Fiat 128            32.4   4  78.7
## Honda Civic         30.4   4  75.7
## Toyota Corolla      33.9   4  71.1
## Toyota Corona       21.5   4 120.1
## Dodge Challenger    15.5   8 318.0
## AMC Javelin         15.2   8 304.0
## Camaro Z28          13.3   8 350.0
## Pontiac Firebird    19.2   8 400.0
## Fiat X1-9           27.3   4  79.0
## Porsche 914-2       26.0   4 120.3
## Lotus Europa        30.4   4  95.1
## Ford Pantera L      15.8   8 351.0
## Ferrari Dino        19.7   6 145.0
## Maserati Bora       15.0   8 301.0
## Volvo 142E          21.4   4 121.0
```

``` r
# Select all columns except certain ones
select(mtcars, -cyl, -disp)
```

```
##                      mpg  hp drat    wt  qsec vs am gear carb
## Mazda RX4           21.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag       21.0 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710          22.8  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive      21.4 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout   18.7 175 3.15 3.440 17.02  0  0    3    2
## Valiant             18.1 105 2.76 3.460 20.22  1  0    3    1
## Duster 360          14.3 245 3.21 3.570 15.84  0  0    3    4
## Merc 240D           24.4  62 3.69 3.190 20.00  1  0    4    2
## Merc 230            22.8  95 3.92 3.150 22.90  1  0    4    2
## Merc 280            19.2 123 3.92 3.440 18.30  1  0    4    4
## Merc 280C           17.8 123 3.92 3.440 18.90  1  0    4    4
## Merc 450SE          16.4 180 3.07 4.070 17.40  0  0    3    3
## Merc 450SL          17.3 180 3.07 3.730 17.60  0  0    3    3
## Merc 450SLC         15.2 180 3.07 3.780 18.00  0  0    3    3
## Cadillac Fleetwood  10.4 205 2.93 5.250 17.98  0  0    3    4
## Lincoln Continental 10.4 215 3.00 5.424 17.82  0  0    3    4
## Chrysler Imperial   14.7 230 3.23 5.345 17.42  0  0    3    4
## Fiat 128            32.4  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic         30.4  52 4.93 1.615 18.52  1  1    4    2
## Toyota Corolla      33.9  65 4.22 1.835 19.90  1  1    4    1
## Toyota Corona       21.5  97 3.70 2.465 20.01  1  0    3    1
## Dodge Challenger    15.5 150 2.76 3.520 16.87  0  0    3    2
## AMC Javelin         15.2 150 3.15 3.435 17.30  0  0    3    2
## Camaro Z28          13.3 245 3.73 3.840 15.41  0  0    3    4
## Pontiac Firebird    19.2 175 3.08 3.845 17.05  0  0    3    2
## Fiat X1-9           27.3  66 4.08 1.935 18.90  1  1    4    1
## Porsche 914-2       26.0  91 4.43 2.140 16.70  0  1    5    2
## Lotus Europa        30.4 113 3.77 1.513 16.90  1  1    5    2
## Ford Pantera L      15.8 264 4.22 3.170 14.50  0  1    5    4
## Ferrari Dino        19.7 175 3.62 2.770 15.50  0  1    5    6
## Maserati Bora       15.0 335 3.54 3.570 14.60  0  1    5    8
## Volvo 142E          21.4 109 4.11 2.780 18.60  1  1    4    2
```

``` r
# Select columns that start with a letter
select(mtcars, starts_with("c"))  # cyl and carb
```

```
##                     cyl carb
## Mazda RX4             6    4
## Mazda RX4 Wag         6    4
## Datsun 710            4    1
## Hornet 4 Drive        6    1
## Hornet Sportabout     8    2
## Valiant               6    1
## Duster 360            8    4
## Merc 240D             4    2
## Merc 230              4    2
## Merc 280              6    4
## Merc 280C             6    4
## Merc 450SE            8    3
## Merc 450SL            8    3
## Merc 450SLC           8    3
## Cadillac Fleetwood    8    4
## Lincoln Continental   8    4
## Chrysler Imperial     8    4
## Fiat 128              4    1
## Honda Civic           4    2
## Toyota Corolla        4    1
## Toyota Corona         4    1
## Dodge Challenger      8    2
## AMC Javelin           8    2
## Camaro Z28            8    4
## Pontiac Firebird      8    2
## Fiat X1-9             4    1
## Porsche 914-2         4    2
## Lotus Europa          4    2
## Ford Pantera L        8    4
## Ferrari Dino          6    6
## Maserati Bora         8    8
## Volvo 142E            4    2
```

### `filter()` - Choosing rows

`filter()` lets you keep only rows that meet certain conditions. This is like subsetting but with cleaner syntax.


``` r
# Filter cars with high fuel efficiency
high_mpg <- filter(mtcars, mpg > 25)
high_mpg
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
# Filter with multiple conditions (AND)
efficient_powerful <- filter(mtcars, mpg > 20, hp > 100)
head(efficient_powerful)
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4      21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag  21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
## Hornet 4 Drive 21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
## Volvo 142E     21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
```

``` r
# Filter with OR conditions
filter(mtcars, mpg > 30 | hp > 250)
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
## Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
## Ford Pantera L 15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
## Maserati Bora  15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
```

``` r
# Filter based on categorical data
filter(iris, Species == "setosa")
```

```
##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1           5.1         3.5          1.4         0.2  setosa
## 2           4.9         3.0          1.4         0.2  setosa
## 3           4.7         3.2          1.3         0.2  setosa
## 4           4.6         3.1          1.5         0.2  setosa
## 5           5.0         3.6          1.4         0.2  setosa
## 6           5.4         3.9          1.7         0.4  setosa
## 7           4.6         3.4          1.4         0.3  setosa
## 8           5.0         3.4          1.5         0.2  setosa
## 9           4.4         2.9          1.4         0.2  setosa
## 10          4.9         3.1          1.5         0.1  setosa
## 11          5.4         3.7          1.5         0.2  setosa
## 12          4.8         3.4          1.6         0.2  setosa
## 13          4.8         3.0          1.4         0.1  setosa
## 14          4.3         3.0          1.1         0.1  setosa
## 15          5.8         4.0          1.2         0.2  setosa
## 16          5.7         4.4          1.5         0.4  setosa
## 17          5.4         3.9          1.3         0.4  setosa
## 18          5.1         3.5          1.4         0.3  setosa
## 19          5.7         3.8          1.7         0.3  setosa
## 20          5.1         3.8          1.5         0.3  setosa
## 21          5.4         3.4          1.7         0.2  setosa
## 22          5.1         3.7          1.5         0.4  setosa
## 23          4.6         3.6          1.0         0.2  setosa
## 24          5.1         3.3          1.7         0.5  setosa
## 25          4.8         3.4          1.9         0.2  setosa
## 26          5.0         3.0          1.6         0.2  setosa
## 27          5.0         3.4          1.6         0.4  setosa
## 28          5.2         3.5          1.5         0.2  setosa
## 29          5.2         3.4          1.4         0.2  setosa
## 30          4.7         3.2          1.6         0.2  setosa
## 31          4.8         3.1          1.6         0.2  setosa
## 32          5.4         3.4          1.5         0.4  setosa
## 33          5.2         4.1          1.5         0.1  setosa
## 34          5.5         4.2          1.4         0.2  setosa
## 35          4.9         3.1          1.5         0.2  setosa
## 36          5.0         3.2          1.2         0.2  setosa
## 37          5.5         3.5          1.3         0.2  setosa
## 38          4.9         3.6          1.4         0.1  setosa
## 39          4.4         3.0          1.3         0.2  setosa
## 40          5.1         3.4          1.5         0.2  setosa
## 41          5.0         3.5          1.3         0.3  setosa
## 42          4.5         2.3          1.3         0.3  setosa
## 43          4.4         3.2          1.3         0.2  setosa
## 44          5.0         3.5          1.6         0.6  setosa
## 45          5.1         3.8          1.9         0.4  setosa
## 46          4.8         3.0          1.4         0.3  setosa
## 47          5.1         3.8          1.6         0.2  setosa
## 48          4.6         3.2          1.4         0.2  setosa
## 49          5.3         3.7          1.5         0.2  setosa
## 50          5.0         3.3          1.4         0.2  setosa
```

### `mutate()` - Creating new columns

`mutate()` adds new columns to your data frame, often based on existing columns. This is perfect for calculating new variables.


``` r
# Create a new column for horsepower per weight
mtcars_new <- mutate(mtcars, hp_per_weight = hp / wt)
head(select(mtcars_new, hp, wt, hp_per_weight))
```

```
##                    hp    wt hp_per_weight
## Mazda RX4         110 2.620      41.98473
## Mazda RX4 Wag     110 2.875      38.26087
## Datsun 710         93 2.320      40.08621
## Hornet 4 Drive    110 3.215      34.21462
## Hornet Sportabout 175 3.440      50.87209
## Valiant           105 3.460      30.34682
```

``` r
# Create multiple new columns at once
mtcars_enhanced <- mutate(mtcars,
                         hp_per_weight = hp / wt,
                         is_efficient = mpg > 20,
                         weight_kg = wt * 453.592)  # convert to kg

head(select(mtcars_enhanced, mpg, hp, wt, hp_per_weight, is_efficient, weight_kg))
```

```
##                    mpg  hp    wt hp_per_weight is_efficient weight_kg
## Mazda RX4         21.0 110 2.620      41.98473         TRUE  1188.411
## Mazda RX4 Wag     21.0 110 2.875      38.26087         TRUE  1304.077
## Datsun 710        22.8  93 2.320      40.08621         TRUE  1052.333
## Hornet 4 Drive    21.4 110 3.215      34.21462         TRUE  1458.298
## Hornet Sportabout 18.7 175 3.440      50.87209        FALSE  1560.356
## Valiant           18.1 105 3.460      30.34682        FALSE  1569.428
```

``` r
# Mutate can use columns you just created
mtcars_mutated <- mutate(mtcars, 
                        weight_tons = wt / 2,
                        hp_per_ton = hp / (wt / 2))
head(select(mtcars_mutated, hp, wt, weight_tons, hp_per_ton))
```

```
##                    hp    wt weight_tons hp_per_ton
## Mazda RX4         110 2.620      1.3100   83.96947
## Mazda RX4 Wag     110 2.875      1.4375   76.52174
## Datsun 710         93 2.320      1.1600   80.17241
## Hornet 4 Drive    110 3.215      1.6075   68.42924
## Hornet Sportabout 175 3.440      1.7200  101.74419
## Valiant           105 3.460      1.7300   60.69364
```


### `arrange()` - Sorting rows

`arrange()` sorts your data based on one or more columns. By default, it sorts in ascending order.


``` r
# Sort by miles per gallon (lowest to highest)
head(arrange(mtcars, mpg))
```

```
##                      mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Cadillac Fleetwood  10.4   8  472 205 2.93 5.250 17.98  0  0    3    4
## Lincoln Continental 10.4   8  460 215 3.00 5.424 17.82  0  0    3    4
## Camaro Z28          13.3   8  350 245 3.73 3.840 15.41  0  0    3    4
## Duster 360          14.3   8  360 245 3.21 3.570 15.84  0  0    3    4
## Chrysler Imperial   14.7   8  440 230 3.23 5.345 17.42  0  0    3    4
## Maserati Bora       15.0   8  301 335 3.54 3.570 14.60  0  1    5    8
```

``` r
# Sort by miles per gallon (highest to lowest)
head(arrange(mtcars, desc(mpg)))
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
## Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
## Fiat X1-9      27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
## Porsche 914-2  26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
```

``` r
# Sort by multiple columns
head(arrange(mtcars, cyl, desc(mpg)))
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
## Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
## Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
## Fiat X1-9      27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
## Porsche 914-2  26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
```

### `count()` - Counting occurrences

`count()` is a quick way to count how many times each value appears in a column.


``` r
# Count cars by number of cylinders
count(mtcars, cyl)
```

```
##   cyl  n
## 1   4 11
## 2   6  7
## 3   8 14
```

``` r
# Count by multiple variables
count(mtcars, cyl, gear)
```

```
##   cyl gear  n
## 1   4    3  1
## 2   4    4  8
## 3   4    5  2
## 4   6    3  2
## 5   6    4  4
## 6   6    5  1
## 7   8    3 12
## 8   8    5  2
```

``` r
# Count and sort
count(mtcars, cyl, sort = TRUE)
```

```
##   cyl  n
## 1   8 14
## 2   4 11
## 3   6  7
```

``` r
# With iris data
count(iris, Species)
```

```
##      Species  n
## 1     setosa 50
## 2 versicolor 50
## 3  virginica 50
```

### Pipes (`%>%`) - Chaining operations

The pipe operator `%>%` lets you chain multiple operations together. Read it as "then do". This makes your code more readable and easier to follow.

**What is a pipe?**  
The pipe takes the result from the left side and passes it as the first argument to the function on the right side. This allows you to write a sequence of data steps in the order you would describe them. This makes your code:

- Easier to read and write
- Avoids lots of nested parentheses
- Lets you build up your analysis step by step

**How to read a pipe chain:**  
`mtcars %>% select(mpg, hp) %>% filter(mpg > 20)`  
means:  
“Take mtcars, then select mpg and hp, then keep only rows where mpg > 20.”

**Tip:**  
You can break a long pipe chain into multiple lines for clarity.  
RStudio will automatically indent the next line after a pipe.

**Common mistake:**  
Don’t forget to load the `tidyverse` or `dplyr` package, or `%>%` won’t work!


**Without pipes** (hard to read):

``` r
# Hard to read - working from inside out
result <- arrange(
  filter(
    select(mtcars, mpg, hp, wt), 
    mpg > 20
  ), 
  desc(hp)
)
head(result)
```

```
##                 mpg  hp    wt
## Lotus Europa   30.4 113 1.513
## Mazda RX4      21.0 110 2.620
## Mazda RX4 Wag  21.0 110 2.875
## Hornet 4 Drive 21.4 110 3.215
## Volvo 142E     21.4 109 2.780
## Toyota Corona  21.5  97 2.465
```

**With pipes** (much clearer):

``` r
# Easy to read - working from left to right
mtcars %>%
  select(mpg, hp, wt) %>%
  filter(mpg > 20) %>%
  arrange(desc(hp)) %>%
  head()
```

```
##                 mpg  hp    wt
## Lotus Europa   30.4 113 1.513
## Mazda RX4      21.0 110 2.620
## Mazda RX4 Wag  21.0 110 2.875
## Hornet 4 Drive 21.4 110 3.215
## Volvo 142E     21.4 109 2.780
## Toyota Corona  21.5  97 2.465
```

The pipe takes the result from the left side and passes it as the first argument to the function on the right side.

### `group_by()` and `summarize()` - Grouped analysis

These functions work together to perform calculations on groups within your data. This is incredibly powerful for analysis.

`group_by()` divides your data into groups, and `summarize()` calculates statistics for each group.


``` r
# Calculate average mpg by number of cylinders
mtcars %>%
  group_by(cyl) %>%
  summarize(avg_mpg = mean(mpg))
```

```
## # A tibble: 3 × 2
##     cyl avg_mpg
##   <dbl>   <dbl>
## 1     4    26.7
## 2     6    19.7
## 3     8    15.1
```

``` r
# Multiple summary statistics
mtcars %>%
  group_by(cyl) %>%
  summarize(
    count = n(),              # count of cars
    avg_mpg = mean(mpg),      # average mpg
    max_hp = max(hp),         # maximum horsepower
    avg_weight = mean(wt)     # average weight
  )
```

```
## # A tibble: 3 × 5
##     cyl count avg_mpg max_hp avg_weight
##   <dbl> <int>   <dbl>  <dbl>      <dbl>
## 1     4    11    26.7    113       2.29
## 2     6     7    19.7    175       3.12
## 3     8    14    15.1    335       4.00
```

``` r
# Group by multiple variables
mtcars %>%
  group_by(cyl, gear) %>%
  summarize(
    count = n(),
    avg_mpg = mean(mpg))
```

```
## # A tibble: 8 × 4
## # Groups:   cyl [3]
##     cyl  gear count avg_mpg
##   <dbl> <dbl> <int>   <dbl>
## 1     4     3     1    21.5
## 2     4     4     8    26.9
## 3     4     5     2    28.2
## 4     6     3     2    19.8
## 5     6     4     4    19.8
## 6     6     5     1    19.7
## 7     8     3    12    15.0
## 8     8     5     2    15.4
```

### Putting it all together

Here's a more complex example that combines multiple `dplyr` functions:


``` r
# Analyze efficient cars (>20 mpg) by cylinder count
efficient_car_analysis <- mtcars %>%
  filter(mpg > 20) %>%                    # only efficient cars
  mutate(hp_per_weight = hp / wt) %>%     # create efficiency ratio
  group_by(cyl) %>%                       # group by cylinders
  summarize(
    car_count = n(),
    avg_mpg = round(mean(mpg), 1),
    avg_hp = round(mean(hp), 1),
    avg_efficiency = round(mean(hp_per_weight), 2)
  ) %>%
  arrange(desc(avg_mpg))                  # sort by mpg

efficient_car_analysis
```

```
## # A tibble: 2 × 5
##     cyl car_count avg_mpg avg_hp avg_efficiency
##   <dbl>     <int>   <dbl>  <dbl>          <dbl>
## 1     4        11    26.7   82.6           37.9
## 2     6         3    21.1  110             38.2
```

## Data Wrangling with `tidyr`

![](fig/tidyr.png)

`tidyr` helps you reshape your data. Most analysis and visualization functions expect data in a specific format, so knowing how to reshape data is crucial.

### Long vs wide data

Data can be organized in two main ways:

**Wide data**: Each variable has its own column
```
Country   2018   2019   2020
USA       100    110    105
Canada     90     95     92
```

**Long data**: Each observation is a separate row
```
Country   Year   Value
USA       2018   100
USA       2019   110
USA       2020   105
Canada    2018    90
Canada    2019    95
Canada    2020    92
```

Different analyses and plots require different formats:

- **Wide format** is easier for humans to read and for some statistical tests
- **Long format** is better for plotting with `ggplot2` and for many statistical analyses

### Pivot functions

`tidyr` provides two main functions for reshaping data:

- `pivot_longer()` - converts wide data to long data
- `pivot_wider()` - converts long data to wide data

Many tidyverse functions, like `pivot_longer()` and `pivot_wider()`, result in a **tibble** instead of a regular data frame.

**What is a tibble?**  
A tibble is a modern version of a data frame. It looks and behaves almost the same, but:

- It prints more nicely in the console (shows only the first 10 rows and columns that fit your screen)
- It never changes the type of your data (no automatic conversion of strings to factors)
- It’s often more consistent and user-friendly for data analysis

Most tidyverse functions work best with tibbles, and you can use tibbles almost everywhere you’d use a data frame.

You can check if your data is a tibble by using the `class()` function. If you see something like `<tbl_df>`, `<tibble>`, or `[tibble]` when you print your data, you’re working with a tibble.

If you ever need a classic data frame (for example, for a function that doesn’t accept tibbles), you can convert it easily:


``` r
# Convert a tibble to a data frame
grades_long_df <- as.data.frame(grades_long)
```

Now, let’s look at how to reshape data using `pivot_longer()` and `pivot_wider()`.

Let's create some example data to practice with:


``` r
# Create sample wide data (grades for different subjects)
grades_wide <- data.frame(
  student = c("Alice", "Bob", "Charlie", "Diana"),
  math = c(85, 78, 92, 88),
  science = c(90, 82, 89, 94),
  english = c(88, 85, 78, 91)
)
grades_wide
```

```
##   student math science english
## 1   Alice   85      90      88
## 2     Bob   78      82      85
## 3 Charlie   92      89      78
## 4   Diana   88      94      91
```

### Pivoting Longer

`pivot_longer()` takes multiple columns and combines them into two columns: one for the variable names and one for the values.


``` r
# Convert wide to long
grades_long <- grades_wide %>%
  pivot_longer(
    cols = c(math, science, english),    # columns to pivot
    names_to = "subject",                # name for the new "names" column
    values_to = "grade"                  # name for the new "values" column
  )
grades_long
```

```
## # A tibble: 12 × 3
##    student subject grade
##    <chr>   <chr>   <dbl>
##  1 Alice   math       85
##  2 Alice   science    90
##  3 Alice   english    88
##  4 Bob     math       78
##  5 Bob     science    82
##  6 Bob     english    85
##  7 Charlie math       92
##  8 Charlie science    89
##  9 Charlie english    78
## 10 Diana   math       88
## 11 Diana   science    94
## 12 Diana   english    91
```

``` r
# Alternative syntax - select columns by position or pattern
grades_wide %>%
  pivot_longer(
    cols = -student,           # all columns except student
    names_to = "subject",
    values_to = "grade"
  )
```

```
## # A tibble: 12 × 3
##    student subject grade
##    <chr>   <chr>   <dbl>
##  1 Alice   math       85
##  2 Alice   science    90
##  3 Alice   english    88
##  4 Bob     math       78
##  5 Bob     science    82
##  6 Bob     english    85
##  7 Charlie math       92
##  8 Charlie science    89
##  9 Charlie english    78
## 10 Diana   math       88
## 11 Diana   science    94
## 12 Diana   english    91
```

``` r
# Or use column positions
grades_wide %>%
  pivot_longer(
    cols = 2:4,               # columns 2 through 4
    names_to = "subject", 
    values_to = "grade"
  )
```

```
## # A tibble: 12 × 3
##    student subject grade
##    <chr>   <chr>   <dbl>
##  1 Alice   math       85
##  2 Alice   science    90
##  3 Alice   english    88
##  4 Bob     math       78
##  5 Bob     science    82
##  6 Bob     english    85
##  7 Charlie math       92
##  8 Charlie science    89
##  9 Charlie english    78
## 10 Diana   math       88
## 11 Diana   science    94
## 12 Diana   english    91
```

Now we can do some statistics. 


``` r
# We can easily calculate average grades by subject
grades_long %>%
  group_by(subject) %>%
  summarize(avg_grade = mean(grade))
```

```
## # A tibble: 3 × 2
##   subject avg_grade
##   <chr>       <dbl>
## 1 english      85.5
## 2 math         85.8
## 3 science      88.8
```

``` r
# Or find the best student in each subject
grades_long %>%
  group_by(subject) %>%
  slice_max(grade, n = 1)  # get the top grade in each subject
```

```
## # A tibble: 3 × 3
## # Groups:   subject [3]
##   student subject grade
##   <chr>   <chr>   <dbl>
## 1 Diana   english    91
## 2 Charlie math       92
## 3 Diana   science    94
```

### Pivoting Wider

`pivot_wider()` does the opposite--it takes two columns and spreads them into multiple columns.


``` r
# Convert back to wide format
grades_back_to_wide <- grades_long %>%
  pivot_wider(
    names_from = subject,     # column containing new column names
    values_from = grade       # column containing values
  )
grades_back_to_wide
```

```
## # A tibble: 4 × 4
##   student  math science english
##   <chr>   <dbl>   <dbl>   <dbl>
## 1 Alice      85      90      88
## 2 Bob        78      82      85
## 3 Charlie    92      89      78
## 4 Diana      88      94      91
```

``` r
# Let's create a more complex example
# Student performance over time
performance <- data.frame(
  student = rep(c("Alice", "Bob"), each = 3),
  quarter = rep(c("Q1", "Q2", "Q3"), times = 2),
  grade = c(85, 87, 90, 78, 80, 83)
)
performance
```

```
##   student quarter grade
## 1   Alice      Q1    85
## 2   Alice      Q2    87
## 3   Alice      Q3    90
## 4     Bob      Q1    78
## 5     Bob      Q2    80
## 6     Bob      Q3    83
```

``` r
# Pivot wider to see each quarter as a column
performance_wide <- performance %>%
  pivot_wider(
    names_from = quarter,
    values_from = grade
  )
performance_wide
```

```
## # A tibble: 2 × 4
##   student    Q1    Q2    Q3
##   <chr>   <dbl> <dbl> <dbl>
## 1 Alice      85    87    90
## 2 Bob        78    80    83
```



### Questions that warrant different data structures

**Use wide format when you want to:**

- Compare values across categories side by side
- Calculate correlations between variables
- Create certain types of tables for reports
- Use functions that expect each variable in its own column

**Use long format when you want to:**

- Create plots with `ggplot2` (especially when you want to color/group by category)
- Calculate statistics by group
- Use functions that work with grouping variables
- Perform operations on multiple columns at once


``` r
# Example: When would you use each format?

# Wide format is good for correlation analysis
cor(grades_wide[, -1])  # correlation between subjects (excluding student names)
```

```
##               math   science    english
## math     1.0000000 0.7317406 -0.3292796
## science  0.7317406 1.0000000  0.4017887
## english -0.3292796 0.4017887  1.0000000
```

``` r
# Long format is good for grouped analysis
grades_long %>%
  group_by(subject) %>%
  summarize(
    avg_grade = mean(grade),
    min_grade = min(grade),
    max_grade = max(grade),
    grade_range = max_grade - min_grade
  )
```

```
## # A tibble: 3 × 5
##   subject avg_grade min_grade max_grade grade_range
##   <chr>       <dbl>     <dbl>     <dbl>       <dbl>
## 1 english      85.5        78        91          13
## 2 math         85.8        78        92          14
## 3 science      88.8        82        94          12
```


## Saving Your Results and Outputs

Now that you’ve learned how to manipulate and reshape data, it’s important to know how to **save your results** for future use or sharing. This is why we set up folders like `output/` and `figures/` at the start.

### Saving and loading a dataset

Often, you’ll want to save a cleaned or summarized dataset so you (or others) can use it later, or open it in another program like Excel.  

- **`write.csv()`** saves a data frame to a CSV (comma-separated values) file on your computer.
- **`read.csv()`** loads a CSV file back into R as a data frame.

**Example:**


``` r
# Save a data frame to a CSV file
write.csv(my_data, file = "output/my_data.csv", row.names = FALSE)

# Later, or in a new R session, you can load it back:
my_loaded_data <- read.csv("output/my_data.csv")
```

- The `file` argument is the path and file name where you want to save or load your data.
- `row.names = FALSE` is often used to avoid saving row numbers as an extra column.

### Saving plots as image files

You can also save your plots as image files (like PNG or JPEG) so you can use them in reports, presentations, or share them with others.

To save a plot you will need to open a **graphics device**. This is a way to tell R to create an image file instead of displaying the plot in the RStudio Plots pane.

This is a three-step process:

1. **Open a graphics device** (like `png()` or `jpeg()`) and give it a file name.

   - This tells R: "Get ready to save a plot as an image file"
   - You specify the filename and image type (PNG, JPEG, etc.)

2. **Create your plot as usual** with functions like `plot()` or `barplot()`

   - Your plot won't appear in RStudio's Plots pane
   - Instead, it's being "drawn" into the image file

3. **Close the device** with `dev.off()` to finish saving the file

   - This tells R: "I'm done drawing, please save and close the image file"
   - **Important:** Don't forget this step or your file won't be saved properly!

R needs to know when you start and stop creating the image file. It's like telling R "start recording" → do your work → "stop recording and save."

**Example:**


``` r
# Save a plot as a PNG image
png("figures/my_plot.png", width = 600, height = 400)
plot(mtcars$hp, mtcars$mpg)
dev.off()
```

- The plot will be saved in your `figures/` folder as `my_plot.png`.
- You won’t see the plot in your RStudio Plots pane when saving this way, but you can open the image file to view it.


Let’s create a new dataset from `mtcars` that only includes cars with high fuel efficiency, and save it as a CSV file in your `output/` folder.


``` r
# Create a new dataset: cars with mpg > 25
efficient_cars <- filter(mtcars, mpg > 25)

# Save to CSV in the output folder
write.csv(efficient_cars, file = "output/efficient_cars.csv", row.names = TRUE)
```

Now you’ll find a file called `efficient_cars.csv` in your `output/` folder!


### Saving a basic plot

Let’s make a simple plot and save it to your `figures/` folder. (We’ll cover plotting in depth in another workshop.)


``` r
# Create a basic scatter plot and save it as a PNG
png("figures/mpg_vs_hp.png", width = 600, height = 400)
plot(mtcars$hp, mtcars$mpg,
     main = "Fuel Efficiency vs Horsepower",
     xlab = "Horsepower",
     ylab = "Miles per Gallon",
     col = "blue", pch = 19)
dev.off()
```

```
## png 
##   2
```

This creates a file called `mpg_vs_hp.png` in your `figures/` folder.



### Saving a summary table

You can also save summary statistics or tables:


``` r
# Create a summary table: average mpg by number of cylinders
mpg_by_cyl <- mtcars %>%
  group_by(cyl) %>%
  summarize(avg_mpg = mean(mpg))

# Save the summary table as a CSV
write.csv(mpg_by_cyl, file = "output/mpg_by_cyl.csv", row.names = FALSE)
```


**Tip:**  
Always check your `output/` and `figures/` folders after running your code to make sure your files were saved as expected!


## Exercises

Let's practice what we've learned with some exercises. Be sure to create a script for your code and save your results!

### Exercise 1: Basic dplyr operations

Using the `mtcars` dataset create varibles to answer the following questions:


``` r
# 1. Select only the columns: mpg, cyl, hp, and wt
# Your code here:

# 2. Filter cars that have more than 6 cylinders AND more than 200 horsepower  
# Your code here:

# 3. Create a new column called "power_to_weight" (hp divided by wt)
# Your code here:

# 4. Arrange cars by mpg from highest to lowest
# Your code here:

# 5. Count how many cars have each number of cylinders
# Your code here:

# 6. Save your power_to_weight dataset as a CSV file in your output folder
# Your code here:
```

### Exercise 2: Pipes and grouped analysis

Using the `mtcars` dataset, create a new dateset with the following parameters using pipes:


``` r
# Using the mtcars dataset, use pipes to:
# 1. Filter cars with mpg > 15
# 2. Create a new column hp_per_weight = hp/wt  
# 3. Group by number of cylinders
# 4. Summarize to get: count of cars, average mpg, average hp_per_weight
# 5. Arrange by average mpg
# 6. Save this summary table as "cylinder_analysis.csv" in your output folder

# Your code here:
```

### Exercise 3: Pivoting practice and plotting

Create this dataset and practice pivoting:


``` r
# Temperature data for different cities
temp_data <- data.frame(
  city = c("Las Vegas", "Reno", "Carson City"),
  jan = c(45, 32, 35),
  apr = c(65, 55, 58),
  jul = c(95, 85, 88),
  oct = c(70, 60, 63)
)
temp_data
```

```
##          city jan apr jul oct
## 1   Las Vegas  45  65  95  70
## 2        Reno  32  55  85  60
## 3 Carson City  35  58  88  63
```


``` r
# 1. Convert this wide data to long format
# Call the new columns "month" and "temperature"
# Your code here:

# 2. From your long format data, calculate the average temperature for each month
# Your code here:

# 3. Save your long format temperature data as "temp_long.csv"
# Your code here:
```

### Solutions

<details>
<summary>**Click here to see the solutions**</summary>


``` r
# Exercise 1 Solutions
# 1. Select columns
selected_cars <- select(mtcars, mpg, cyl, hp, wt)

# 2. Filter cars
powerful_cars <- filter(mtcars, cyl > 6, hp > 200)

# 3. Create new column
cars_with_ratio <- mutate(mtcars, power_to_weight = hp / wt)

# 4. Arrange by mpg
cars_by_mpg <- arrange(mtcars, desc(mpg))

# 5. Count cylinders
cyl_counts <- count(mtcars, cyl)

# 6. Save the power_to_weight dataset
write.csv(cars_with_ratio, file = "output/cars_with_power_ratio.csv", row.names = TRUE)

# Exercise 2 Solution
cylinder_analysis <- mtcars %>%
  filter(mpg > 15) %>%
  mutate(hp_per_weight = hp / wt) %>%
  group_by(cyl) %>%
  summarize(
    car_count = n(),
    avg_mpg = mean(mpg),
    avg_hp_per_weight = mean(hp_per_weight)
  ) %>%
  arrange(avg_mpg)

# Save the analysis
write.csv(cylinder_analysis, file = "output/cylinder_analysis.csv", row.names = FALSE)

# Exercise 3 Solutions
# 1. Wide to long
temp_long <- temp_data %>%
  pivot_longer(
    cols = -city,
    names_to = "month", 
    values_to = "temperature"
  )

# 2. Average temperature by month
avg_temp_by_month <- temp_long %>%
  group_by(month) %>%
  summarize(avg_temp = mean(temperature))


# 3. Save long format data
write.csv(temp_long, file = "output/temp_long.csv", row.names = FALSE)
```

</details>

## Key takeaways

- **`dplyr` provides intuitive functions** for data manipulation: `select()`, `filter()`, `mutate()`, `arrange()`, `group_by()`, `summarize()`
- **Pipes (`%>%`) make code readable** by chaining operations from left to right
- **`tidyr` helps reshape data** between wide and long formats using `pivot_longer()` and `pivot_wider()`
- **Long format is better for plotting and grouped analysis**; **wide format is better for human readability and some statistical tests**
- **Group operations are powerful** --use `group_by()` with `summarize()` to calculate statistics for different groups
- **These packages work seamlessly together** and with other tidyverse packages for data science workflows

Now you have the tools to efficiently manipulate and reshape data for analysis and visualization!

