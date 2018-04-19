---
title: "DDS Analkytics"
author: "Daniel Davieau, LAkeitra Webb, Emil Ramos"
date: "April 18, 2018"
output: 
  html_document: 
    keep_md: yes
---


Info

```r
rm(list=ls())
setwd("~/GitHub/DDS-Analytics")
library(knitr)
library(readxl)
library(dygraphs)
library(tidyr)
library(ggplot2)
library(forecast)
library(xtable)
library(kableExtra)
library(readr)
library(reshape2)
```

```
## 
## Attaching package: 'reshape2'
```

```
## The following object is masked from 'package:tidyr':
## 
##     smiths
```

```r
library(wordcloud2)
#sessionInfo()
```
Import the data

```r
CaseStudy2_data <- read_excel("Input/CaseStudy2-data.xlsx")
View(CaseStudy2_data)
```
Preliminary data analysis
Data Structure Analysis, Quality Analysis etc.
Clean the Raw Data
"a	Read the csv into R and take a look at the data set.  Output how many rows and columns the data.frame is."
b	The column names are either too much or not enough.  Change the column names so that they do not have spaces, underscores, slashes, and the like. All column names should be under 12 characters. Make sure you’re updating your codebook with information on the tidied data set as well.


```r
class((CaseStudy2_data))
```

```
## [1] "tbl_df"     "tbl"        "data.frame"
```

```r
str(CaseStudy2_data)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	1470 obs. of  35 variables:
##  $ Age                     : num  41 49 37 33 27 32 59 30 38 36 ...
##  $ Attrition               : chr  "Yes" "No" "Yes" "No" ...
##  $ BusinessTravel          : chr  "Travel_Rarely" "Travel_Frequently" "Travel_Rarely" "Travel_Frequently" ...
##  $ DailyRate               : num  1102 279 1373 1392 591 ...
##  $ Department              : chr  "Sales" "Research & Development" "Research & Development" "Research & Development" ...
##  $ DistanceFromHome        : num  1 8 2 3 2 2 3 24 23 27 ...
##  $ Education               : num  2 1 2 4 1 2 3 1 3 3 ...
##  $ EducationField          : chr  "Life Sciences" "Life Sciences" "Other" "Life Sciences" ...
##  $ EmployeeCount           : num  1 1 1 1 1 1 1 1 1 1 ...
##  $ EmployeeNumber          : num  1 2 4 5 7 8 10 11 12 13 ...
##  $ EnvironmentSatisfaction : num  2 3 4 4 1 4 3 4 4 3 ...
##  $ Gender                  : chr  "Female" "Male" "Male" "Female" ...
##  $ HourlyRate              : num  94 61 92 56 40 79 81 67 44 94 ...
##  $ JobInvolvement          : num  3 2 2 3 3 3 4 3 2 3 ...
##  $ JobLevel                : num  2 2 1 1 1 1 1 1 3 2 ...
##  $ JobRole                 : chr  "Sales Executive" "Research Scientist" "Laboratory Technician" "Research Scientist" ...
##  $ JobSatisfaction         : num  4 2 3 3 2 4 1 3 3 3 ...
##  $ MaritalStatus           : chr  "Single" "Married" "Single" "Married" ...
##  $ MonthlyIncome           : num  5993 5130 2090 2909 3468 ...
##  $ MonthlyRate             : num  19479 24907 2396 23159 16632 ...
##  $ NumCompaniesWorked      : num  8 1 6 1 9 0 4 1 0 6 ...
##  $ Over18                  : chr  "Y" "Y" "Y" "Y" ...
##  $ OverTime                : chr  "Yes" "No" "Yes" "Yes" ...
##  $ PercentSalaryHike       : num  11 23 15 11 12 13 20 22 21 13 ...
##  $ PerformanceRating       : num  3 4 3 3 3 3 4 4 4 3 ...
##  $ RelationshipSatisfaction: num  1 4 2 3 4 3 1 2 2 2 ...
##  $ StandardHours           : num  80 80 80 80 80 80 80 80 80 80 ...
##  $ StockOptionLevel        : num  0 1 0 0 1 0 3 1 0 2 ...
##  $ TotalWorkingYears       : num  8 10 7 8 6 8 12 1 10 17 ...
##  $ TrainingTimesLastYear   : num  0 3 3 3 3 2 3 2 2 3 ...
##  $ WorkLifeBalance         : num  1 3 3 3 3 2 2 3 3 2 ...
##  $ YearsAtCompany          : num  6 10 0 8 2 7 1 1 9 7 ...
##  $ YearsInCurrentRole      : num  4 7 0 7 2 7 0 0 7 7 ...
##  $ YearsSinceLastPromotion : num  0 1 0 3 2 3 0 0 1 7 ...
##  $ YearsWithCurrManager    : num  5 7 0 0 2 6 0 0 8 7 ...
```

```r
unique(CaseStudy2_data$Gender)
```

```
## [1] "Female" "Male"
```

```r
unique(CaseStudy2_data$YearsAtCompany)
```

```
##  [1]  6 10  0  8  2  7  1  9  5  4 25  3 12 14 22 15 27 21 17 11 13 37 16
## [24] 20 40 24 33 19 36 18 29 31 32 34 26 30 23
```

```r
unique(CaseStudy2_data$Attrition)
```

```
## [1] "Yes" "No"
```
a	Remove all observations where the participant is under age 18.  No further analysis of underage individuals is permitted by your client.  Remove any other age outliers as you see fit, but be sure to tell what you’re doing and why.

```r
unique(CaseStudy2_data$Age)
```

```
##  [1] 41 49 37 33 27 32 59 30 38 36 35 29 31 34 28 22 53 24 21 42 44 46 39
## [24] 43 50 26 48 55 45 56 23 51 40 54 58 20 25 19 57 52 47 18 60
```

```r
unique(CaseStudy2_data$Over18)
```

```
## [1] "Y"
```
b	Please provide (in pretty-fied table format or similar), descriptive statistics on at least 7 variables (age, Income, etc.).  Create a simple histogram for two of them.  Comment on the shape of the distribution in your markdown.

```r
# Interesting variables
# daily rate, education,  job satisfaction,number of companies worked, performance rating,years at company, years with current manager
x <- summary(CaseStudy2_data$DailyRate)
DailyRateSummary<-data.frame(x=matrix(x),row.names=names(x))
names(DailyRateSummary)<-paste("", "Value")

# x<-summary(CaseStudy2_data$NumCompaniesWorked)

kable(DailyRateSummary, "html") %>%
  kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;">  Value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Min. </td>
   <td style="text-align:right;"> 102.0000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1st Qu. </td>
   <td style="text-align:right;"> 465.0000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Median </td>
   <td style="text-align:right;"> 802.0000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mean </td>
   <td style="text-align:right;"> 802.4857 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 3rd Qu. </td>
   <td style="text-align:right;"> 1157.0000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Max. </td>
   <td style="text-align:right;"> 1499.0000 </td>
  </tr>
</tbody>
</table>

```r
#total working years(Use caution)
# Variables to avoid
# Age, Gender, marital status, relationship statisfaction, total working years(Use caution)
```



c	Give the frequencies (in table format or similar) for Gender, Education, and Occupation.  They can be separate tables, if that’s your choice.
d	Give the counts (again, pretty table) of management positions.







c	Give the frequencies (in table format or similar) for Gender, Education, and Occupation.  They can be separate tables, if that’s your choice.
d	Give the counts (again, pretty table) of management positions.

a	Note: You should make all of these appealing looking.  Remember to include things like a clean, informative title, axis labels that are in plain English, and readable axis values that do not overlap.
b	Create barcharts in ggplot or similar  The bars should be in descending order, Use any color palette of your choice other than the default.
c	Is there a relationship between Age and Income?  Create a scatterplot and make an assessment of whether there is a relationship.  Color each point based on the Gender of the participant.  You’re welcome to use lm() or similar functions to back up your claims.

d	What about Life Satisfaction?  Create another scatterplot.  Is there a discernible relationship there to what?   



The executive leadership has identified predicting employee turnover as its first application of data science for talent management. Before the business green lights the project, they have tasked your data science team to conduct an analysis of existing employee data.

determine factors that lead to attrition
identify (at least) the top three factors that contribute to turnover
The business is also interested in learning about any job role specific trends that may exist in the data set (e.g., “Data Scientists have the highest job satisfaction”

•	Title
•	Authors all listed
•	Presentation Outline
•	Business Objectives
•	Data Sourced
•	Methodology
•	Evaluation/Results
•	Summary
•	Business Objectives
•	Data Source	
•	Where you got it 
•	Basic Statistics 
•	Methodology	
•	Steps 
•	Workflow
•	Evaluation/Results
•	Tell me the percentages
•	Show me graphs with explanations
•	The top three factors that contribute to turnover
•	Tell me about any job role specific trends that may exist in the data set
•	Provide any other interesting trends and observations from your analysis
•	Other things to consider?
•	Summary 
•	Insights
•	Recommendations
•	Improvements
•	Questions
Have your presentation as a PDF ready to present on April 24. 

c	Some columns are, due to Qualtrics, malfunctioning.  
d	Make sure your columns are the proper data types (i.e., numeric, character, etc.).  If they are incorrect, convert them.
