---
title: "Midterm 1"
author: "Gabriel Rendon"
date: "2022-01-27"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions (including each other), but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

This exam is due by 12:00p on Thursday, January 27.  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
## ✓ readr   2.1.1     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

## Questions  
Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.  
#One major elements that I beleive we have practiced in this class is the way we efficiently organize our data. All the coding seems messy at first, but when we knit our file to .html, everything we have worked trhough RStudio seems neat and pleasing to the eye. Of course it can be a litlle hard to get used to, but when you get it, our work will be great. 
2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice?  
#Echoing to question 1; this may seem simple, but I found that organizing our data to be the most helpful thing that I have learned in this class.This includes comands like data.frame, janitor, or even arrange. When you actually have to work on data in a research lab, I presume, you'll need to be able to have everything organized and as easy to read. We keep practicing organization, and I hope to keep strengthening that skill in the future of this class. 
In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.

```r
elephants <- readr::read_csv("data/ElephantsMF.csv")
```

```
## Rows: 288 Columns: 3
```

```
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
```

```
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
dim(elephants)
```

```
## [1] 288   3
```

```r
str(elephants)
```

```
## spec_tbl_df [288 × 3] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ Age   : num [1:288] 1.4 17.5 12.8 11.2 12.7 ...
##  $ Height: num [1:288] 120 227 235 210 220 ...
##  $ Sex   : chr [1:288] "M" "M" "M" "M" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   Age = col_double(),
##   ..   Height = col_double(),
##   ..   Sex = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
glimpse(elephants)
```

```
## Rows: 288
## Columns: 3
## $ Age    <dbl> 1.40, 17.50, 12.75, 11.17, 12.67, 12.67, 12.25, 12.17, 28.17, 1…
## $ Height <dbl> 120.00, 227.00, 235.00, 210.00, 220.00, 189.00, 225.00, 204.00,…
## $ Sex    <chr> "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M"…
```

```r
summary(elephants)
```

```
##       Age            Height           Sex           
##  Min.   : 0.01   Min.   : 75.46   Length:288        
##  1st Qu.: 4.58   1st Qu.:160.75   Class :character  
##  Median : 9.46   Median :200.00   Mode  :character  
##  Mean   :10.97   Mean   :187.68                     
##  3rd Qu.:16.50   3rd Qu.:221.09                     
##  Max.   :32.17   Max.   :304.06
```

```r
view(elephants)
```

4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.

```r
names(elephants)
```

```
## [1] "Age"    "Height" "Sex"
```

```r
elephants <- janitor::clean_names(elephants)
elephants
```

```
## # A tibble: 288 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # … with 278 more rows
```

```r
elephants%>%
  mutate_at(vars("sex"), factor)
```

```
## # A tibble: 288 × 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # … with 278 more rows
```

5. (2 points) How many male and female elephants are represented in the data?

**Males**

```r
male_elephants<-
  elephants%>%
  filter(sex=="M")
male_elephants
```

```
## # A tibble: 138 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # … with 128 more rows
```
#There are 138 male elephants present in the data. 

**Females**

```r
female_elephants<-
  elephants%>%
  filter(sex=="F")
female_elephants
```

```
## # A tibble: 150 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1 11.1   218.  F    
##  2  2.33  133.  F    
##  3  2.42  145.  F    
##  4 26.5   206.  F    
##  5 11.8   207   F    
##  6  0.33   85.6 F    
##  7 26.8   227.  F    
##  8 13.4   203   F    
##  9 28.4   228.  F    
## 10  2.08  131.  F    
## # … with 140 more rows
```
#There are 150 female elephants present in the data. 

6. (2 points) What is the average age all elephants in the data?

```r
mean(elephants$age)
```

```
## [1] 10.97132
```

7. (2 points) How does the average age and height of elephants compare by sex?

**Males**


```r
mean(male_elephants$age)
```

```
## [1] 8.945145
```
#mean age

```r
avg_heightM<-mean(male_elephants$height)
avg_heightM
```

```
## [1] 185.1312
```
#mean height

**Females**

```r
mean(female_elephants$age)
```

```
## [1] 12.8354
```
#mean age

```r
avg_heightF<-mean(female_elephants$height)
avg_heightF
```

```
## [1] 190.0307
```
#mean height

8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  

**Male**

```r
male_elephants%>%
  group_by(sex)%>%
  filter(age>20)%>%
  summarize(avg_heightM=mean(height, na.rm=T), min_height=min(height), max_height=max(height))
```

```
## # A tibble: 1 × 4
##   sex   avg_heightM min_height max_height
##   <chr>       <dbl>      <dbl>      <dbl>
## 1 M            270.       229.       304.
```
**Female**

```r
female_elephants%>%
  group_by(sex)%>%
  filter(age>20)%>%
  summarize(avg_heightF=mean(height, na.rm=T), min_height=min(height), max_height=max(height))
```

```
## # A tibble: 1 × 4
##   sex   avg_heightF min_height max_height
##   <chr>       <dbl>      <dbl>      <dbl>
## 1 F            232.       193.       278.
```

For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.

```r
gabon<- readr::read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
```

```
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
```

```
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
dim(gabon)
```

```
## [1] 24 26
```

```r
str(gabon)
```

```
## spec_tbl_df [24 × 26] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ TransectID             : num [1:24] 1 2 2 3 4 5 6 7 8 9 ...
##  $ Distance               : num [1:24] 7.14 17.31 18.32 20.85 15.95 ...
##  $ HuntCat                : chr [1:24] "Moderate" "None" "None" "None" ...
##  $ NumHouseholds          : num [1:24] 54 54 29 29 29 29 29 54 25 73 ...
##  $ LandUse                : chr [1:24] "Park" "Park" "Park" "Logging" ...
##  $ Veg_Rich               : num [1:24] 16.7 15.8 16.9 12.4 17.1 ...
##  $ Veg_Stems              : num [1:24] 31.2 37.4 32.3 29.4 36 ...
##  $ Veg_liana              : num [1:24] 5.78 13.25 4.75 9.78 13.25 ...
##  $ Veg_DBH                : num [1:24] 49.6 34.6 42.8 36.6 41.5 ...
##  $ Veg_Canopy             : num [1:24] 3.78 3.75 3.43 3.75 3.88 2.5 4 4 3 3.25 ...
##  $ Veg_Understory         : num [1:24] 2.89 3.88 3 2.75 3.25 3 2.38 2.71 3.25 3.13 ...
##  $ RA_Apes                : num [1:24] 1.87 0 4.49 12.93 0 ...
##  $ RA_Birds               : num [1:24] 52.7 52.2 37.4 59.3 52.6 ...
##  $ RA_Elephant            : num [1:24] 0 0.86 1.33 0.56 1 0 1.11 0.43 2.2 0 ...
##  $ RA_Monkeys             : num [1:24] 38.6 28.5 41.8 19.9 41.3 ...
##  $ RA_Rodent              : num [1:24] 4.22 6.04 1.06 3.66 2.52 1.83 3.1 1.26 4.37 6.31 ...
##  $ RA_Ungulate            : num [1:24] 2.66 12.41 13.86 3.71 2.53 ...
##  $ Rich_AllSpecies        : num [1:24] 22 20 22 19 20 22 23 19 19 19 ...
##  $ Evenness_AllSpecies    : num [1:24] 0.793 0.773 0.74 0.681 0.811 0.786 0.818 0.757 0.773 0.668 ...
##  $ Diversity_AllSpecies   : num [1:24] 2.45 2.31 2.29 2.01 2.43 ...
##  $ Rich_BirdSpecies       : num [1:24] 11 10 11 8 8 10 11 11 11 9 ...
##  $ Evenness_BirdSpecies   : num [1:24] 0.732 0.704 0.688 0.559 0.799 0.771 0.801 0.687 0.784 0.573 ...
##  $ Diversity_BirdSpecies  : num [1:24] 1.76 1.62 1.65 1.16 1.66 ...
##  $ Rich_MammalSpecies     : num [1:24] 11 10 11 11 12 12 12 8 8 10 ...
##  $ Evenness_MammalSpecies : num [1:24] 0.736 0.705 0.65 0.619 0.736 0.694 0.776 0.79 0.821 0.783 ...
##  $ Diversity_MammalSpecies: num [1:24] 1.76 1.62 1.56 1.48 1.83 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   TransectID = col_double(),
##   ..   Distance = col_double(),
##   ..   HuntCat = col_character(),
##   ..   NumHouseholds = col_double(),
##   ..   LandUse = col_character(),
##   ..   Veg_Rich = col_double(),
##   ..   Veg_Stems = col_double(),
##   ..   Veg_liana = col_double(),
##   ..   Veg_DBH = col_double(),
##   ..   Veg_Canopy = col_double(),
##   ..   Veg_Understory = col_double(),
##   ..   RA_Apes = col_double(),
##   ..   RA_Birds = col_double(),
##   ..   RA_Elephant = col_double(),
##   ..   RA_Monkeys = col_double(),
##   ..   RA_Rodent = col_double(),
##   ..   RA_Ungulate = col_double(),
##   ..   Rich_AllSpecies = col_double(),
##   ..   Evenness_AllSpecies = col_double(),
##   ..   Diversity_AllSpecies = col_double(),
##   ..   Rich_BirdSpecies = col_double(),
##   ..   Evenness_BirdSpecies = col_double(),
##   ..   Diversity_BirdSpecies = col_double(),
##   ..   Rich_MammalSpecies = col_double(),
##   ..   Evenness_MammalSpecies = col_double(),
##   ..   Diversity_MammalSpecies = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
glimpse(gabon)
```

```
## Rows: 24
## Columns: 26
## $ TransectID              <dbl> 1, 2, 2, 3, 4, 5, 6, 7, 8, 9, 13, 14, 15, 16, …
## $ Distance                <dbl> 7.14, 17.31, 18.32, 20.85, 15.95, 17.47, 24.06…
## $ HuntCat                 <chr> "Moderate", "None", "None", "None", "None", "N…
## $ NumHouseholds           <dbl> 54, 54, 29, 29, 29, 29, 29, 54, 25, 73, 46, 56…
## $ LandUse                 <chr> "Park", "Park", "Park", "Logging", "Park", "Pa…
## $ Veg_Rich                <dbl> 16.67, 15.75, 16.88, 12.44, 17.13, 16.50, 14.7…
## $ Veg_Stems               <dbl> 31.20, 37.44, 32.33, 29.39, 36.00, 29.22, 31.2…
## $ Veg_liana               <dbl> 5.78, 13.25, 4.75, 9.78, 13.25, 12.88, 8.38, 8…
## $ Veg_DBH                 <dbl> 49.57, 34.59, 42.82, 36.62, 41.52, 44.07, 51.2…
## $ Veg_Canopy              <dbl> 3.78, 3.75, 3.43, 3.75, 3.88, 2.50, 4.00, 4.00…
## $ Veg_Understory          <dbl> 2.89, 3.88, 3.00, 2.75, 3.25, 3.00, 2.38, 2.71…
## $ RA_Apes                 <dbl> 1.87, 0.00, 4.49, 12.93, 0.00, 2.48, 3.78, 6.1…
## $ RA_Birds                <dbl> 52.66, 52.17, 37.44, 59.29, 52.62, 38.64, 42.6…
## $ RA_Elephant             <dbl> 0.00, 0.86, 1.33, 0.56, 1.00, 0.00, 1.11, 0.43…
## $ RA_Monkeys              <dbl> 38.59, 28.53, 41.82, 19.85, 41.34, 43.29, 46.2…
## $ RA_Rodent               <dbl> 4.22, 6.04, 1.06, 3.66, 2.52, 1.83, 3.10, 1.26…
## $ RA_Ungulate             <dbl> 2.66, 12.41, 13.86, 3.71, 2.53, 13.75, 3.10, 8…
## $ Rich_AllSpecies         <dbl> 22, 20, 22, 19, 20, 22, 23, 19, 19, 19, 21, 22…
## $ Evenness_AllSpecies     <dbl> 0.793, 0.773, 0.740, 0.681, 0.811, 0.786, 0.81…
## $ Diversity_AllSpecies    <dbl> 2.452, 2.314, 2.288, 2.006, 2.431, 2.429, 2.56…
## $ Rich_BirdSpecies        <dbl> 11, 10, 11, 8, 8, 10, 11, 11, 11, 9, 11, 11, 1…
## $ Evenness_BirdSpecies    <dbl> 0.732, 0.704, 0.688, 0.559, 0.799, 0.771, 0.80…
## $ Diversity_BirdSpecies   <dbl> 1.756, 1.620, 1.649, 1.162, 1.660, 1.775, 1.92…
## $ Rich_MammalSpecies      <dbl> 11, 10, 11, 11, 12, 12, 12, 8, 8, 10, 10, 11, …
## $ Evenness_MammalSpecies  <dbl> 0.736, 0.705, 0.650, 0.619, 0.736, 0.694, 0.77…
## $ Diversity_MammalSpecies <dbl> 1.764, 1.624, 1.558, 1.484, 1.829, 1.725, 1.92…
```

```r
summary(gabon)
```

```
##    TransectID       Distance        HuntCat          NumHouseholds  
##  Min.   : 1.00   Min.   : 2.700   Length:24          Min.   :13.00  
##  1st Qu.: 5.75   1st Qu.: 5.668   Class :character   1st Qu.:24.75  
##  Median :14.50   Median : 9.720   Mode  :character   Median :29.00  
##  Mean   :13.50   Mean   :11.879                      Mean   :37.88  
##  3rd Qu.:20.25   3rd Qu.:17.683                      3rd Qu.:54.00  
##  Max.   :27.00   Max.   :26.760                      Max.   :73.00  
##    LandUse             Veg_Rich       Veg_Stems       Veg_liana     
##  Length:24          Min.   :10.88   Min.   :23.44   Min.   : 4.750  
##  Class :character   1st Qu.:13.10   1st Qu.:28.69   1st Qu.: 9.033  
##  Mode  :character   Median :14.94   Median :32.45   Median :11.940  
##                     Mean   :14.83   Mean   :32.80   Mean   :11.040  
##                     3rd Qu.:16.54   3rd Qu.:37.08   3rd Qu.:13.250  
##                     Max.   :18.75   Max.   :47.56   Max.   :16.380  
##     Veg_DBH        Veg_Canopy    Veg_Understory     RA_Apes      
##  Min.   :28.45   Min.   :2.500   Min.   :2.380   Min.   : 0.000  
##  1st Qu.:40.65   1st Qu.:3.250   1st Qu.:2.875   1st Qu.: 0.000  
##  Median :43.90   Median :3.430   Median :3.000   Median : 0.485  
##  Mean   :46.09   Mean   :3.469   Mean   :3.020   Mean   : 2.045  
##  3rd Qu.:50.58   3rd Qu.:3.750   3rd Qu.:3.167   3rd Qu.: 3.815  
##  Max.   :76.48   Max.   :4.000   Max.   :3.880   Max.   :12.930  
##     RA_Birds      RA_Elephant       RA_Monkeys      RA_Rodent    
##  Min.   :31.56   Min.   :0.0000   Min.   : 5.84   Min.   :1.060  
##  1st Qu.:52.51   1st Qu.:0.0000   1st Qu.:22.70   1st Qu.:2.047  
##  Median :57.90   Median :0.3600   Median :31.74   Median :3.230  
##  Mean   :58.64   Mean   :0.5450   Mean   :31.30   Mean   :3.278  
##  3rd Qu.:68.17   3rd Qu.:0.8925   3rd Qu.:39.88   3rd Qu.:4.093  
##  Max.   :85.03   Max.   :2.3000   Max.   :54.12   Max.   :6.310  
##   RA_Ungulate     Rich_AllSpecies Evenness_AllSpecies Diversity_AllSpecies
##  Min.   : 0.000   Min.   :15.00   Min.   :0.6680      Min.   :1.966       
##  1st Qu.: 1.232   1st Qu.:19.00   1st Qu.:0.7542      1st Qu.:2.248       
##  Median : 2.545   Median :20.00   Median :0.7760      Median :2.317       
##  Mean   : 4.166   Mean   :20.21   Mean   :0.7699      Mean   :2.310       
##  3rd Qu.: 5.157   3rd Qu.:22.00   3rd Qu.:0.8083      3rd Qu.:2.429       
##  Max.   :13.860   Max.   :24.00   Max.   :0.8330      Max.   :2.566       
##  Rich_BirdSpecies Evenness_BirdSpecies Diversity_BirdSpecies Rich_MammalSpecies
##  Min.   : 8.00    Min.   :0.5590       Min.   :1.162         Min.   : 6.000    
##  1st Qu.:10.00    1st Qu.:0.6825       1st Qu.:1.603         1st Qu.: 9.000    
##  Median :11.00    Median :0.7220       Median :1.680         Median :10.000    
##  Mean   :10.33    Mean   :0.7137       Mean   :1.661         Mean   : 9.875    
##  3rd Qu.:11.00    3rd Qu.:0.7722       3rd Qu.:1.784         3rd Qu.:11.000    
##  Max.   :13.00    Max.   :0.8240       Max.   :2.008         Max.   :12.000    
##  Evenness_MammalSpecies Diversity_MammalSpecies
##  Min.   :0.6190         Min.   :1.378          
##  1st Qu.:0.7073         1st Qu.:1.567          
##  Median :0.7390         Median :1.699          
##  Mean   :0.7477         Mean   :1.698          
##  3rd Qu.:0.7847         3rd Qu.:1.815          
##  Max.   :0.8610         Max.   :2.065
```

```r
view(gabon)
```

```r
gabon <- janitor::clean_names(gabon)
gabon
```

```
## # A tibble: 24 × 26
##    transect_id distance hunt_cat num_households land_use veg_rich veg_stems
##          <dbl>    <dbl> <chr>             <dbl> <chr>       <dbl>     <dbl>
##  1           1     7.14 Moderate             54 Park         16.7      31.2
##  2           2    17.3  None                 54 Park         15.8      37.4
##  3           2    18.3  None                 29 Park         16.9      32.3
##  4           3    20.8  None                 29 Logging      12.4      29.4
##  5           4    16.0  None                 29 Park         17.1      36  
##  6           5    17.5  None                 29 Park         16.5      29.2
##  7           6    24.1  None                 29 Park         14.8      31.2
##  8           7    19.8  None                 54 Logging      13.2      32.6
##  9           8     5.78 High                 25 Neither      12.6      23.7
## 10           9     5.13 High                 73 Logging      16        27.1
## # … with 14 more rows, and 19 more variables: veg_liana <dbl>, veg_dbh <dbl>,
## #   veg_canopy <dbl>, veg_understory <dbl>, ra_apes <dbl>, ra_birds <dbl>,
## #   ra_elephant <dbl>, ra_monkeys <dbl>, ra_rodent <dbl>, ra_ungulate <dbl>,
## #   rich_all_species <dbl>, evenness_all_species <dbl>,
## #   diversity_all_species <dbl>, rich_bird_species <dbl>,
## #   evenness_bird_species <dbl>, diversity_bird_species <dbl>,
## #   rich_mammal_species <dbl>, evenness_mammal_species <dbl>, …
```

```r
colnames(gabon)
```

```
##  [1] "transect_id"              "distance"                
##  [3] "hunt_cat"                 "num_households"          
##  [5] "land_use"                 "veg_rich"                
##  [7] "veg_stems"                "veg_liana"               
##  [9] "veg_dbh"                  "veg_canopy"              
## [11] "veg_understory"           "ra_apes"                 
## [13] "ra_birds"                 "ra_elephant"             
## [15] "ra_monkeys"               "ra_rodent"               
## [17] "ra_ungulate"              "rich_all_species"        
## [19] "evenness_all_species"     "diversity_all_species"   
## [21] "rich_bird_species"        "evenness_bird_species"   
## [23] "diversity_bird_species"   "rich_mammal_species"     
## [25] "evenness_mammal_species"  "diversity_mammal_species"
```


```r
gabon%>%
  mutate_at(vars("land_use", "hunt_cat"), factor)
```

```
## # A tibble: 24 × 26
##    transect_id distance hunt_cat num_households land_use veg_rich veg_stems
##          <dbl>    <dbl> <fct>             <dbl> <fct>       <dbl>     <dbl>
##  1           1     7.14 Moderate             54 Park         16.7      31.2
##  2           2    17.3  None                 54 Park         15.8      37.4
##  3           2    18.3  None                 29 Park         16.9      32.3
##  4           3    20.8  None                 29 Logging      12.4      29.4
##  5           4    16.0  None                 29 Park         17.1      36  
##  6           5    17.5  None                 29 Park         16.5      29.2
##  7           6    24.1  None                 29 Park         14.8      31.2
##  8           7    19.8  None                 54 Logging      13.2      32.6
##  9           8     5.78 High                 25 Neither      12.6      23.7
## 10           9     5.13 High                 73 Logging      16        27.1
## # … with 14 more rows, and 19 more variables: veg_liana <dbl>, veg_dbh <dbl>,
## #   veg_canopy <dbl>, veg_understory <dbl>, ra_apes <dbl>, ra_birds <dbl>,
## #   ra_elephant <dbl>, ra_monkeys <dbl>, ra_rodent <dbl>, ra_ungulate <dbl>,
## #   rich_all_species <dbl>, evenness_all_species <dbl>,
## #   diversity_all_species <dbl>, rich_bird_species <dbl>,
## #   evenness_bird_species <dbl>, diversity_bird_species <dbl>,
## #   rich_mammal_species <dbl>, evenness_mammal_species <dbl>, …
```

10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?

**Birds**

```r
avg_bio_birds<-mean(gabon$diversity_bird_species)
avg_bio_birds
```

```
## [1] 1.66125
```


```r
bio_birds<-gabon%>%
  group_by(hunt_cat)%>%
  filter(hunt_cat=="Moderate"|hunt_cat=="High")%>%
  summarize(bio_birds=mean(diversity_bird_species, na.rm=T))
bio_birds
```

```
## # A tibble: 2 × 2
##   hunt_cat bio_birds
##   <chr>        <dbl>
## 1 High          1.66
## 2 Moderate      1.62
```

**Mammals**

```r
avg_bio_mammals<-mean(gabon$diversity_mammal_species)
avg_bio_mammals
```

```
## [1] 1.697875
```

```r
bio_mammals<-gabon%>%
  group_by(hunt_cat)%>%
  filter(hunt_cat=="Moderate"|hunt_cat=="High")%>%
  summarize(bio_mammals=mean(diversity_mammal_species, na.rm=T))
bio_mammals
```

```
## # A tibble: 2 × 2
##   hunt_cat bio_mammals
##   <chr>          <dbl>
## 1 High            1.74
## 2 Moderate        1.68
```

11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  


```r
gabon%>%
  filter(distance<3)%>%
  select("distance", "ra_apes", "ra_birds", "ra_elephant", "ra_monkeys", "ra_rodent", "ra_ungulate")%>%
  summarize(across(c("ra_apes", "ra_birds", "ra_elephant", "ra_monkeys", "ra_rodent", "ra_ungulate"), mean))
```

```
## # A tibble: 1 × 6
##   ra_apes ra_birds ra_elephant ra_monkeys ra_rodent ra_ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    0.12     76.6       0.145       17.3      3.90        1.87
```

```r
gabon%>%
  filter(distance>25)%>%
  select("ra_apes", "ra_birds", "ra_elephant", "ra_monkeys", "ra_rodent", "ra_ungulate")%>%
  summarize(across(c("ra_apes", "ra_birds", "ra_elephant", "ra_monkeys", "ra_rodent", "ra_ungulate"), mean))
```

```
## # A tibble: 1 × 6
##   ra_apes ra_birds ra_elephant ra_monkeys ra_rodent ra_ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    4.91     31.6           0       54.1      1.29        8.12
```
12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`

```r
gabon%>%
  select(transect_id, num_households, land_use)%>%
filter(land_use=="Logging")%>%
arrange(desc(num_households))%>%
  summarize(avg_households=(mean(num_households, na.rm=T)), min_household=min(num_households), max(num_households))
```

```
## # A tibble: 1 × 3
##   avg_households min_household `max(num_households)`
##            <dbl>         <dbl>                 <dbl>
## 1           41.7            13                    73
```
