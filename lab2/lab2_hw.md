---
title: "Lab 2 Homework"
author: "Gabriel Rendon"
date: "2022-01-19"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

1. What is a vector in R?  
Vectors are different ways data can be organized. The command for this is the 'c' comand, which stands for concatenate.
2. What is a data matrix in R?  
Data matrix are many stacked vectors instead of a single vector. They're vextors on steriods that require the 'matrix()' command.
3. Below are data collected by three scientists (Jill, Steve, Susan in order) measuring temperatures of eight hot springs. Run this code chunk to create the vectors.  

```r
spring_1 <- c(36.25, 35.40, 35.30)
spring_2 <- c(35.15, 35.35, 33.35)
spring_3 <- c(30.70, 29.65, 29.20)
spring_4 <- c(39.70, 40.05, 38.65)
spring_5 <- c(31.85, 31.40, 29.30)
spring_6 <- c(30.20, 30.65, 29.75)
spring_7 <- c(32.90, 32.50, 32.80)
spring_8 <- c(36.80, 36.45, 33.15)
```

4. Build a data matrix that has the springs as rows and the columns as scientists.  

```r
box_office<-c(spring_1, spring_2, spring_3, spring_4, spring_5, spring_6, spring_7, spring_8)
box_office
```

```
##  [1] 36.25 35.40 35.30 35.15 35.35 33.35 30.70 29.65 29.20 39.70 40.05 38.65
## [13] 31.85 31.40 29.30 30.20 30.65 29.75 32.90 32.50 32.80 36.80 36.45 33.15
```

```r
spring_matrix<-matrix(box_office, nrow=3, byrow = F)
spring_matrix 
```

```
##       [,1]  [,2]  [,3]  [,4]  [,5]  [,6] [,7]  [,8]
## [1,] 36.25 35.15 30.70 39.70 31.85 30.20 32.9 36.80
## [2,] 35.40 35.35 29.65 40.05 31.40 30.65 32.5 36.45
## [3,] 35.30 33.35 29.20 38.65 29.30 29.75 32.8 33.15
```

5. The names of the springs are 1.Bluebell Spring, 2.Opal Spring, 3.Riverside Spring, 4.Too Hot Spring, 5.Mystery Spring, 6.Emerald Spring, 7.Black Spring, 8.Pearl Spring. Name the rows and columns in the data matrix. Start by making two new vectors with the names, then use `colnames()` and `rownames()` to name the columns and rows.

```r
titles<-c("Bluebell Spring", "Opal Spring", "Riverside Springs", "Too Hot Springs", "Mystery Springs", "Emerald Springs", "Black Springs", "Pearl Springs")
titles
```

```
## [1] "Bluebell Spring"   "Opal Spring"       "Riverside Springs"
## [4] "Too Hot Springs"   "Mystery Springs"   "Emerald Springs"  
## [7] "Black Springs"     "Pearl Springs"
```

```r
region<-c("Jill", "Steve", "Susan")
region  
```

```
## [1] "Jill"  "Steve" "Susan"
```

```r
colnames(spring_matrix)<-titles
```

```r
rownames(spring_matrix)<-region
```

```r
spring_matrix
```

```
##       Bluebell Spring Opal Spring Riverside Springs Too Hot Springs
## Jill            36.25       35.15             30.70           39.70
## Steve           35.40       35.35             29.65           40.05
## Susan           35.30       33.35             29.20           38.65
##       Mystery Springs Emerald Springs Black Springs Pearl Springs
## Jill            31.85           30.20          32.9         36.80
## Steve           31.40           30.65          32.5         36.45
## Susan           29.30           29.75          32.8         33.15
```

6. Calculate the mean temperature of all eight springs.

```r
x<-c(spring_matrix)
```

```r
mean(x)
```

```
## [1] 33.60417
```


7. Add this as a new column in the data matrix.  

```r
Mean_Temp<-rowMeans(spring_matrix)
Mean_Temp
```

```
##     Jill    Steve    Susan 
## 34.19375 33.93125 32.68750
```

```r
all_spring_matrix<-cbind(spring_matrix, Mean_Temp)
all_spring_matrix
```

```
##       Bluebell Spring Opal Spring Riverside Springs Too Hot Springs
## Jill            36.25       35.15             30.70           39.70
## Steve           35.40       35.35             29.65           40.05
## Susan           35.30       33.35             29.20           38.65
##       Mystery Springs Emerald Springs Black Springs Pearl Springs Mean_Temp
## Jill            31.85           30.20          32.9         36.80  34.19375
## Steve           31.40           30.65          32.5         36.45  33.93125
## Susan           29.30           29.75          32.8         33.15  32.68750
```

8. Show Susan's value for Opal Spring only.

```r
spring_matrix[3,2]
```

```
## [1] 33.35
```

9. Calculate the mean for Jill's column only.  

```r
Jill_Mean<-all_spring_matrix[1, ]
mean(Jill_Mean)
```

```
## [1] 34.19375
```

10. Use the data matrix to perform one calculation or operation of your interest.

```r
Emerald_Mean<-spring_matrix[ ,6]
```

```r
x<-c(Emerald_Mean)
mean(x)
```

```
## [1] 30.2
```
I calculated the mean for just Emerald Springs 
## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
