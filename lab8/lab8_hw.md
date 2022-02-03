---
title: "Lab 8 Homework"
author: "Please Add Your Name Here"
date: "2022-02-02"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
```

## Install `here`
The package `here` is a nice option for keeping directories clear when loading files. I will demonstrate below and let you decide if it is something you want to use.  

```r
#install.packages("here")
```

## Data
For this homework, we will use a data set compiled by the Office of Environment and Heritage in New South Whales, Australia. It contains the enterococci counts in water samples obtained from Sydney beaches as part of the Beachwatch Water Quality Program. Enterococci are bacteria common in the intestines of mammals; they are rarely present in clean water. So, enterococci values are a measurement of pollution. `cfu` stands for colony forming units and measures the number of viable bacteria in a sample [cfu](https://en.wikipedia.org/wiki/Colony-forming_unit).   

This homework loosely follows the tutorial of [R Ladies Sydney](https://rladiessydney.org/). If you get stuck, check it out!  

1. Start by loading the data `sydneybeaches`. Do some exploratory analysis to get an idea of the data structure.

```r
sydneybeaches<-readr::read_csv("data/sydneybeaches.csv")
```

```
## Rows: 3690 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): Region, Council, Site, Date
## dbl (4): BeachId, Longitude, Latitude, Enterococci (cfu/100ml)
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
sydneybeaches
```

```
## # A tibble: 3,690 × 8
##    BeachId Region        Council Site  Longitude Latitude Date  `Enterococci (…`
##      <dbl> <chr>         <chr>   <chr>     <dbl>    <dbl> <chr>            <dbl>
##  1      25 Sydney City … Randwi… Clov…      151.    -33.9 02/0…               19
##  2      25 Sydney City … Randwi… Clov…      151.    -33.9 06/0…                3
##  3      25 Sydney City … Randwi… Clov…      151.    -33.9 12/0…                2
##  4      25 Sydney City … Randwi… Clov…      151.    -33.9 18/0…               13
##  5      25 Sydney City … Randwi… Clov…      151.    -33.9 30/0…                8
##  6      25 Sydney City … Randwi… Clov…      151.    -33.9 05/0…                7
##  7      25 Sydney City … Randwi… Clov…      151.    -33.9 11/0…               11
##  8      25 Sydney City … Randwi… Clov…      151.    -33.9 23/0…               97
##  9      25 Sydney City … Randwi… Clov…      151.    -33.9 07/0…                3
## 10      25 Sydney City … Randwi… Clov…      151.    -33.9 25/0…                0
## # … with 3,680 more rows
```

If you want to try `here`, first notice the output when you load the `here` library. It gives you information on the current working directory. You can then use it to easily and intuitively load files.

```r
library(here)
```

```
## here() starts at /Users/eliasrendonflores/Documents/GitHub/BIS15W2022_grendon
```

The quotes show the folder structure from the root directory.

```r
sydneybeaches <-read_csv(here("lab8", "data", "sydneybeaches.csv")) %>% janitor::clean_names()
```

```
## Rows: 3690 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): Region, Council, Site, Date
## dbl (4): BeachId, Longitude, Latitude, Enterococci (cfu/100ml)
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
sydneybeaches
```

```
## # A tibble: 3,690 × 8
##    beach_id region       council site  longitude latitude date  enterococci_cfu…
##       <dbl> <chr>        <chr>   <chr>     <dbl>    <dbl> <chr>            <dbl>
##  1       25 Sydney City… Randwi… Clov…      151.    -33.9 02/0…               19
##  2       25 Sydney City… Randwi… Clov…      151.    -33.9 06/0…                3
##  3       25 Sydney City… Randwi… Clov…      151.    -33.9 12/0…                2
##  4       25 Sydney City… Randwi… Clov…      151.    -33.9 18/0…               13
##  5       25 Sydney City… Randwi… Clov…      151.    -33.9 30/0…                8
##  6       25 Sydney City… Randwi… Clov…      151.    -33.9 05/0…                7
##  7       25 Sydney City… Randwi… Clov…      151.    -33.9 11/0…               11
##  8       25 Sydney City… Randwi… Clov…      151.    -33.9 23/0…               97
##  9       25 Sydney City… Randwi… Clov…      151.    -33.9 07/0…                3
## 10       25 Sydney City… Randwi… Clov…      151.    -33.9 25/0…                0
## # … with 3,680 more rows
```

2. Are these data "tidy" per the definitions of the tidyverse? How do you know? Are they in wide or long format?
#Yes, the data seems to be in the form of what we call "tidy". This data table follows the three rules, every column is a variable, every row is an observation, and every cell is a single value. This is in long format. 

3. We are only interested in the variables site, date, and enterococci_cfu_100ml. Make a new object focused on these variables only. Name the object `sydneybeaches_long`


```r
sydneybeaches_long<-sydneybeaches%>%
 select(site,date,enterococci_cfu_100ml)
sydneybeaches_long
```

```
## # A tibble: 3,690 × 3
##    site           date       enterococci_cfu_100ml
##    <chr>          <chr>                      <dbl>
##  1 Clovelly Beach 02/01/2013                    19
##  2 Clovelly Beach 06/01/2013                     3
##  3 Clovelly Beach 12/01/2013                     2
##  4 Clovelly Beach 18/01/2013                    13
##  5 Clovelly Beach 30/01/2013                     8
##  6 Clovelly Beach 05/02/2013                     7
##  7 Clovelly Beach 11/02/2013                    11
##  8 Clovelly Beach 23/02/2013                    97
##  9 Clovelly Beach 07/03/2013                     3
## 10 Clovelly Beach 25/03/2013                     0
## # … with 3,680 more rows
```
4. Pivot the data such that the dates are column names and each beach only appears once. Name the object `sydneybeaches_wide`


```r
sydneybeaches_wide<-sydneybeaches%>%
  pivot_wider(names_from = date,
              values_from = site)
sydneybeaches_wide
```

```
## # A tibble: 754 × 350
##    beach_id region      council longitude latitude enterococci_cfu… `02/01/2013`
##       <dbl> <chr>       <chr>       <dbl>    <dbl>            <dbl> <chr>       
##  1       25 Sydney Cit… Randwi…      151.    -33.9               19 Clovelly Be…
##  2       25 Sydney Cit… Randwi…      151.    -33.9                3 <NA>        
##  3       25 Sydney Cit… Randwi…      151.    -33.9                2 <NA>        
##  4       25 Sydney Cit… Randwi…      151.    -33.9               13 <NA>        
##  5       25 Sydney Cit… Randwi…      151.    -33.9                8 <NA>        
##  6       25 Sydney Cit… Randwi…      151.    -33.9                7 <NA>        
##  7       25 Sydney Cit… Randwi…      151.    -33.9               11 <NA>        
##  8       25 Sydney Cit… Randwi…      151.    -33.9               97 <NA>        
##  9       25 Sydney Cit… Randwi…      151.    -33.9                0 <NA>        
## 10       25 Sydney Cit… Randwi…      151.    -33.9                6 <NA>        
## # … with 744 more rows, and 343 more variables: `06/01/2013` <chr>,
## #   `12/01/2013` <chr>, `18/01/2013` <chr>, `30/01/2013` <chr>,
## #   `05/02/2013` <chr>, `11/02/2013` <chr>, `23/02/2013` <chr>,
## #   `07/03/2013` <chr>, `25/03/2013` <chr>, `02/04/2013` <chr>,
## #   `12/04/2013` <chr>, `18/04/2013` <chr>, `24/04/2013` <chr>,
## #   `01/05/2013` <chr>, `20/05/2013` <chr>, `31/05/2013` <chr>,
## #   `06/06/2013` <chr>, `12/06/2013` <chr>, `24/06/2013` <chr>, …
```

5. Pivot the data back so that the dates are data and not column names.


```r
sydneybeaches_long2<-sydneybeaches_wide%>%
  pivot_longer(-c(beach_id,region,council,longitude, latitude,enterococci_cfu_100ml),
                  names_to = "date",
               values_to = "beaches",
               values_drop_na = T)
               sydneybeaches_long2
```

```
## # A tibble: 3,690 × 8
##    beach_id region     council longitude latitude enterococci_cfu… date  beaches
##       <dbl> <chr>      <chr>       <dbl>    <dbl>            <dbl> <chr> <chr>  
##  1       25 Sydney Ci… Randwi…      151.    -33.9               19 02/0… Clovel…
##  2       25 Sydney Ci… Randwi…      151.    -33.9               19 19/0… Clovel…
##  3       25 Sydney Ci… Randwi…      151.    -33.9                3 06/0… Clovel…
##  4       25 Sydney Ci… Randwi…      151.    -33.9                3 07/0… Clovel…
##  5       25 Sydney Ci… Randwi…      151.    -33.9                3 01/0… Clovel…
##  6       25 Sydney Ci… Randwi…      151.    -33.9                3 14/0… Clovel…
##  7       25 Sydney Ci… Randwi…      151.    -33.9                3 22/0… Clovel…
##  8       25 Sydney Ci… Randwi…      151.    -33.9                3 20/1… Clovel…
##  9       25 Sydney Ci… Randwi…      151.    -33.9                3 08/1… Clovel…
## 10       25 Sydney Ci… Randwi…      151.    -33.9                3 16/0… Clovel…
## # … with 3,680 more rows
```

6. We haven't dealt much with dates yet, but separate the date into columns day, month, and year. Do this on the `sydneybeaches_long` data.


```r
sydneybeaches_sep<-sydneybeaches_long%>%
   separate(date, into= c("month", "day", "year"), sep = "/")
sydneybeaches_sep
```

```
## # A tibble: 3,690 × 5
##    site           month day   year  enterococci_cfu_100ml
##    <chr>          <chr> <chr> <chr>                 <dbl>
##  1 Clovelly Beach 02    01    2013                     19
##  2 Clovelly Beach 06    01    2013                      3
##  3 Clovelly Beach 12    01    2013                      2
##  4 Clovelly Beach 18    01    2013                     13
##  5 Clovelly Beach 30    01    2013                      8
##  6 Clovelly Beach 05    02    2013                      7
##  7 Clovelly Beach 11    02    2013                     11
##  8 Clovelly Beach 23    02    2013                     97
##  9 Clovelly Beach 07    03    2013                      3
## 10 Clovelly Beach 25    03    2013                      0
## # … with 3,680 more rows
```

7. What is the average `enterococci_cfu_100ml` by year for each beach. Think about which data you will use- long or wide.


```r
sydneybeaches_means<-sydneybeaches_sep%>%
  group_by(site,year)%>%
  summarize(mean_enterococci_cfu_100ml=mean(enterococci_cfu_100ml, na.rm=T))%>%
  arrange(year)
```

```
## `summarise()` has grouped output by 'site'. You can override using the `.groups`
## argument.
```

```r
sydneybeaches_means
```

```
## # A tibble: 66 × 3
## # Groups:   site [11]
##    site                    year  mean_enterococci_cfu_100ml
##    <chr>                   <chr>                      <dbl>
##  1 Bondi Beach             2013                       32.2 
##  2 Bronte Beach            2013                       26.8 
##  3 Clovelly Beach          2013                        9.28
##  4 Coogee Beach            2013                       39.7 
##  5 Gordons Bay (East)      2013                       24.8 
##  6 Little Bay Beach        2013                      122.  
##  7 Malabar Beach           2013                      101.  
##  8 Maroubra Beach          2013                       47.1 
##  9 South Maroubra Beach    2013                       39.3 
## 10 South Maroubra Rockpool 2013                       96.4 
## # … with 56 more rows
```

8. Make the output from question 7 easier to read by pivoting it to wide format.

```r
sydneybeaches_means%>%
  pivot_wider(names_from = site,
              values_from = mean_enterococci_cfu_100ml)
```

```
## # A tibble: 6 × 12
##   year  `Bondi Beach` `Bronte Beach` `Clovelly Beach` `Coogee Beach`
##   <chr>         <dbl>          <dbl>            <dbl>          <dbl>
## 1 2013           32.2           26.8             9.28           39.7
## 2 2014           11.1           17.5            13.8            52.6
## 3 2015           14.3           23.6             8.82           40.3
## 4 2016           19.4           61.3            11.3            59.5
## 5 2017           13.2           16.8             7.93           20.7
## 6 2018           22.9           43.4            10.6            21.6
## # … with 7 more variables: `Gordons Bay (East)` <dbl>,
## #   `Little Bay Beach` <dbl>, `Malabar Beach` <dbl>, `Maroubra Beach` <dbl>,
## #   `South Maroubra Beach` <dbl>, `South Maroubra Rockpool` <dbl>,
## #   `Tamarama Beach` <dbl>
```

9. What was the most polluted beach in 2018?


```r
sydneybeaches_means%>%
   filter(year==2018) %>% 
  arrange(desc(mean_enterococci_cfu_100ml))
```

```
## # A tibble: 11 × 3
## # Groups:   site [11]
##    site                    year  mean_enterococci_cfu_100ml
##    <chr>                   <chr>                      <dbl>
##  1 South Maroubra Rockpool 2018                      112.  
##  2 Little Bay Beach        2018                       59.1 
##  3 Bronte Beach            2018                       43.4 
##  4 Malabar Beach           2018                       38.0 
##  5 Bondi Beach             2018                       22.9 
##  6 Coogee Beach            2018                       21.6 
##  7 Gordons Bay (East)      2018                       17.6 
##  8 Tamarama Beach          2018                       15.5 
##  9 South Maroubra Beach    2018                       12.5 
## 10 Clovelly Beach          2018                       10.6 
## 11 Maroubra Beach          2018                        9.21
```
#South Maroubra Rockpool had the most enterococci_cfu_100ml in the year of 2018.

10. Please complete the class project survey at: [BIS 15L Group Project](https://forms.gle/H2j69Z3ZtbLH3efW6)

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
