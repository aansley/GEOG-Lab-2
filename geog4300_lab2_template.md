Lab 2: Text mining and sentiment analysis
================

## Text mining

In the second half of this lab, you’ll do some basic text mining and
sentiment analysis using data from the [Yelp data
challenge](https://www.yelp.com/dataset/challenge). Specifically, you’ll
be looking at reviews for businesses in Charlotte, NC. This file is
available in the data folder of this lab repo.

**IMPORTANT**: Yelp has some restrictions on these data, primarily that
it cannot be shared publicly or used for publication/analysis. You are
free to use it for this lab or for personal research, but you cannot
reuse it for other public facing
    projects.

``` r
library(tidyverse)
```

    ## -- Attaching packages ----------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.2.0     v purrr   0.3.2
    ## v tibble  2.1.3     v dplyr   0.8.3
    ## v tidyr   0.8.3     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.4.0

    ## -- Conflicts -------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(tidytext)
library(knitr)

yelp_data<-read_csv("data/charlotte_restaurants.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_double(),
    ##   business_id = col_character(),
    ##   date = col_datetime(format = ""),
    ##   name = col_character(),
    ##   address = col_character(),
    ##   text = col_character()
    ## )

    ## See spec(...) for full column specifications.

These data include multiple variables about businesses listed in Yelp.
In this case, only restaurants are included, and there are dummy
variables (0/1) for the 10 most common restaurant categories. Here’s a
list of them and the count of reviews in each:

``` r
rest_table<-yelp_data %>%
  gather(`American (New)`:Sandwiches,key="type",value="pres") %>%
  group_by(type) %>%
  summarise(count=sum(pres)) %>%
  arrange(-count)

kable(rest_table)
```

| type                   | count |
| :--------------------- | ----: |
| Restaurants            | 99661 |
| Food                   | 34689 |
| Nightlife              | 30239 |
| Bars                   | 29092 |
| American (New)         | 21564 |
| American (Traditional) | 19791 |
| Breakfast & Brunch     | 17933 |
| Sandwiches             | 12865 |
| Pizza                  |  9940 |
| Burgers                |  9037 |
| Mexican                |  8836 |

**Question 1 (3 points)**: Identify the 20 most common words in these
reviews, first filtering out the stopwords using an anti\_join as shown
in the class script for text mining. You can use the top\_n function to
select the 20 most common words. Use the reorder function as shown in
the class script on text mining to arrange your results from highest to
lowest. Use kable to call the table with your results when done.

``` r
#Code goes here.
```

**Question 2 (2 points)**: Using ggplot, create a bar plot showing the
frequency of these most common words. The class script on text mining
has an example of how to do this using geom\_col.

``` r
#Code goes here
```

**Question 3 (4 points)**: Now let’s compare two types of restaurants.
Filter the dataset so you just have restaurants with *one* or *five*
stars based on reviews (see the “stars” variable). Using the same
process of question 1, identify the 20 most common words (not counting
stop words) in each review. Use kable to call the table with your
results when done.

``` r
#Code goes here
```

**Question 4 (2 points)**: Using the ggwordcloud package, create two
word clouds that show the 20 most common words for each of the two
categories used in question 3, one and five star restaurants.

``` r
#Code goes here
```

**Question 5 (1 point)**: Looking at your results in questions 3 and 4,
identify *one* notable difference in the words used for one star and
five star reviewed restaurants.

{Your response goes here}

**Question 6 (4 points)**: Which burger restaurants had the most
positive reviews? Filter the dataset so you only have restaurants
classified as Burger (meaning they have a 1 in that column). Tokenize
the words used in reviews and join sentiments from the Bing sentiment
dictionary. Use group\_by and summarise to count the number of positive
and negative words by restaurant name. Lastly, create a new variable
that scores each restaurant by subtracting the number of negative words
from the number of positive words. \*

``` r
#Code goes here
```

**Question 7 (2 points)**: Which two restaurants had the highest scores?
How many *positive* and *negative* words did each one have?

{Two restaurant names and their number of positive and negative words go
here.}

**Question 7 (2 points)**: In your own words, explain the purpose of
each function you used to answer question 6.

{Your response goes here.}
