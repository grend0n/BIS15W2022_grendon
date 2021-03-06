---
title: "Lab 11 Homework"
author: "Gabriel Rendon"
date: "2022-02-20"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

**In this homework, you should make use of the aesthetics you have learned. It's OK to be flashy!**

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```

## Resources
The idea for this assignment came from [Rebecca Barter's](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/) ggplot tutorial so if you get stuck this is a good place to have a look.  

## Gapminder
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use. This is the same data that we will use for midterm 2 so this is good practice.

```r
#install.packages("gapminder")
library("gapminder")
```

## Questions
The questions below are open-ended and have many possible solutions. Your approach should, where appropriate, include numerical summaries and visuals. Be creative; assume you are building an analysis that you would ultimately present to an audience of stakeholders. Feel free to try out different `geoms` if they more clearly present your results.  

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine how NA's are treated in the data.**  


```r
gapminder
```

```
## # A tibble: 1,704 ?? 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       1957    30.3  9240934      821.
##  3 Afghanistan Asia       1962    32.0 10267083      853.
##  4 Afghanistan Asia       1967    34.0 11537966      836.
##  5 Afghanistan Asia       1972    36.1 13079460      740.
##  6 Afghanistan Asia       1977    38.4 14880372      786.
##  7 Afghanistan Asia       1982    39.9 12881816      978.
##  8 Afghanistan Asia       1987    40.8 13867957      852.
##  9 Afghanistan Asia       1992    41.7 16317921      649.
## 10 Afghanistan Asia       1997    41.8 22227415      635.
## # ??? with 1,694 more rows
```


```r
glimpse(gapminder)
```

```
## Rows: 1,704
## Columns: 6
## $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", ???
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, ???
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, ???
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.8???
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12???
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, ???
```


```r
summary(gapminder)
```

```
##         country        continent        year         lifeExp     
##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
##  Australia  :  12                  Max.   :2007   Max.   :82.60  
##  (Other)    :1632                                                
##       pop              gdpPercap       
##  Min.   :6.001e+04   Min.   :   241.2  
##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
##  Median :7.024e+06   Median :  3531.8  
##  Mean   :2.960e+07   Mean   :  7215.3  
##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
##  Max.   :1.319e+09   Max.   :113523.1  
## 
```


```r
naniar::miss_var_summary(gapminder)
```

```
## # A tibble: 6 ?? 3
##   variable  n_miss pct_miss
##   <chr>      <int>    <dbl>
## 1 country        0        0
## 2 continent      0        0
## 3 year           0        0
## 4 lifeExp        0        0
## 5 pop            0        0
## 6 gdpPercap      0        0
```
#Nice! No NA's in the data :D

**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**


```r
gapminder%>%
  group_by(year) %>% 
  summarize(mean_lifeExp=mean(lifeExp))
```

```
## # A tibble: 12 ?? 2
##     year mean_lifeExp
##    <int>        <dbl>
##  1  1952         49.1
##  2  1957         51.5
##  3  1962         53.6
##  4  1967         55.7
##  5  1972         57.6
##  6  1977         59.6
##  7  1982         61.5
##  8  1987         63.2
##  9  1992         64.2
## 10  1997         65.0
## 11  2002         65.7
## 12  2007         67.0
```


```r
gapminder$year <- as.factor(gapminder$year)
```


```r
change_gapminder<-gapminder%>%
  group_by(year) %>% 
  summarize(mean_lifeExp=mean(lifeExp))%>%
  ggplot(aes(x=year, y=mean_lifeExp, fill=mean_lifeExp))+
  geom_col()+
  labs(title = "Life Expectancy Change From 1952 to 2007", x="Year", y= "Mean Life Expectancy")
change_gapminder
```

![](lab11_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

**3. How do the distributions of life expectancy compare for the years 1952 and 2007?**


```r
gapminder%>%
  filter(year=="1952"|year=="2007")%>%
  ggplot(aes(x=lifeExp))+
  geom_histogram(aes(y=..density..))+
  geom_density(color="red")+
  geom_smooth(meathod="lm")%>%
   labs(title = "relationship between per capita GDP and life expectancy", x="lifeExp", y="gdpPercap")
```

```
## Warning: Ignoring unknown parameters: meathod
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](lab11_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**


```r
gapminder%>%
  select(continent, lifeExp)%>%
  summarize(min_lifeExp=min(lifeExp),
            max_lifeExp=max(lifeExp),
            median_lifeExp=median(lifeExp))
```

```
## # A tibble: 1 ?? 3
##   min_lifeExp max_lifeExp median_lifeExp
##         <dbl>       <dbl>          <dbl>
## 1        23.6        82.6           60.7
```

**5. How has life expectancy changed between 1952-2007 for each continent?**

```r
gapminder%>%
  group_by(continent, year)%>%
  summarize(mean_lifeExp=mean(lifeExp))%>%
  ggplot(aes(x=year, y=mean_lifeExp, group=continent, color=continent))+
  geom_line()+
  labs(title = "Life Expectancy Change From 1952 to 2007 By Continent")
```

```
## `summarise()` has grouped output by 'continent'. You can override using the
## `.groups` argument.
```

![](lab11_hw_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**

```r
gapminder%>%
  select(lifeExp, gdpPercap)%>%
  ggplot(aes(x=lifeExp, y=gdpPercap))+
  geom_point(size=1, color="deeppink", alpha=1)+
  geom_smooth(meathod="lm")
```

```
## Warning: Ignoring unknown parameters: meathod
```

```
## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
```

![](lab11_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

```r
 labs(title = "relationship between per capita GDP and life expectancy", x="lifeExp", y="gdpPercap")
```

```
## $x
## [1] "lifeExp"
## 
## $y
## [1] "gdpPercap"
## 
## $title
## [1] "relationship between per capita GDP and life expectancy"
## 
## attr(,"class")
## [1] "labels"
```

**7. Which countries have had the largest population growth since 1952?**

```r
pop_growth<-gapminder%>%
  select(country,year,pop)%>%
  filter(year=="1952"|year=="2007")%>%
  pivot_wider(names_from = year, names_prefix = "year_", values_from = pop)%>%
  mutate(growth=year_2007-year_1952)%>%
  arrange(desc(growth))
pop_growth
```

```
## # A tibble: 142 ?? 4
##    country       year_1952  year_2007    growth
##    <fct>             <int>      <int>     <int>
##  1 China         556263527 1318683096 762419569
##  2 India         372000000 1110396331 738396331
##  3 United States 157553000  301139947 143586947
##  4 Indonesia      82052000  223547000 141495000
##  5 Brazil         56602560  190010647 133408087
##  6 Pakistan       41346560  169270617 127924057
##  7 Bangladesh     46886859  150448339 103561480
##  8 Nigeria        33119096  135031164 101912068
##  9 Mexico         30144317  108700891  78556574
## 10 Philippines    22438691   91077287  68638596
## # ??? with 132 more rows
```

**8. Use your results from the question above to plot population growth for the top five countries since 1952.**

```r
pop_growth%>%
  filter(country==c("China", "India", "United States", "Indonesia", "Brazil"))%>%
ggplot(aes(x=reorder(country, growth), y=growth, fill=country))+
  geom_col()+
  labs(title = "population growth for the top five countries since 1952", x="country", y="population growth")
```

```
## Warning in `==.default`(country, c("China", "India", "United States",
## "Indonesia", : longer object length is not a multiple of shorter object length
```

```
## Warning in is.na(e1) | is.na(e2): longer object length is not a multiple of
## shorter object length
```

![](lab11_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

**9. How does per-capita GDP growth compare between these same five countries?**

```r
gapminder%>%
   filter(country==c("China", "India", "United States", "Indonesia", "Brazil"))%>%
  select(country,year, gdpPercap)%>%
  ggplot(aes(x=year, y=gdpPercap, group=country, color=country))+
  geom_line()
```

```
## Warning in `==.default`(country, c("China", "India", "United States",
## "Indonesia", : longer object length is not a multiple of shorter object length
```

```
## Warning in is.na(e1) | is.na(e2): longer object length is not a multiple of
## shorter object length
```

![](lab11_hw_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

**10. Make one plot of your choice that uses faceting!**


```r
gapminder %>% 
  ggplot(aes(x=lifeExp))+
  geom_density()+
  facet_wrap(.~continent)+ 
  theme(plot.title = element_text(size = rel(1.5), hjust = 0.5))+
  labs(title = "Life Expectancy Rise per Continent",
       x = "continent",
       y = "lifeExp",
       fill = "lifeExp")
```

![](lab11_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
