---
title: "DDS Analytics"
author: "Authors: Daniel Davieau, Lakeitra Webb, Emil Ramos"
date: "April 24, 2018"
output: 
  html_document: 
    keep_md: yes
---




```
## 
## Attaching package: 'olsrr'
```

```
## The following object is masked from 'package:datasets':
## 
##     rivers
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
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

```
## 
## Attaching package: 'MASS'
```

```
## The following object is masked from 'package:dplyr':
## 
##     select
```

```
## The following object is masked from 'package:olsrr':
## 
##     cement
```

```
## R version 3.4.4 (2018-03-15)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## Running under: Windows 10 x64 (build 16299)
## 
## Matrix products: default
## 
## locale:
## [1] LC_COLLATE=English_United States.1252 
## [2] LC_CTYPE=English_United States.1252   
## [3] LC_MONETARY=English_United States.1252
## [4] LC_NUMERIC=C                          
## [5] LC_TIME=English_United States.1252    
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
##  [1] MASS_7.3-49      investr_1.4.0    wordcloud2_0.2.1 reshape2_1.4.3  
##  [5] readr_1.1.1      kableExtra_0.8.0 xtable_1.8-2     forecast_8.3    
##  [9] ggplot2_2.2.1    dplyr_0.7.4      tidyr_0.8.0      dygraphs_1.1.1.4
## [13] readxl_1.0.0     knitr_1.20       olsrr_0.5.0     
## 
## loaded via a namespace (and not attached):
##  [1] nlme_3.1-131.1     xts_0.10-2         lubridate_1.7.4   
##  [4] dimRed_0.1.0       httr_1.3.1         rprojroot_1.3-2   
##  [7] gh_1.0.1           tools_3.4.4        backports_1.1.2   
## [10] R6_2.2.2           rpart_4.1-13       nortest_1.0-4     
## [13] lazyeval_0.2.1     colorspace_1.3-2   nnet_7.3-12       
## [16] tidyselect_0.2.4   gridExtra_2.3      mnormt_1.5-5      
## [19] curl_3.2           compiler_3.4.4     rvest_0.3.2       
## [22] xml2_1.2.0         tseries_0.10-44    scales_0.5.0      
## [25] sfsmisc_1.1-2      DEoptimR_1.0-8     lmtest_0.9-36     
## [28] fracdiff_1.4-2     psych_1.8.3.3      robustbase_0.92-8 
## [31] quadprog_1.5-5     goftest_1.1-1      stringr_1.3.0     
## [34] digest_0.6.15      foreign_0.8-69     rmarkdown_1.9     
## [37] pkgconfig_2.0.1    htmltools_0.3.6    htmlwidgets_1.0   
## [40] rlang_0.2.0        TTR_0.23-3         ddalpha_1.3.2     
## [43] rstudioapi_0.7     quantmod_0.4-13    shiny_1.0.5       
## [46] bindr_0.1.1        zoo_1.8-1          jsonlite_1.5      
## [49] magrittr_1.5       Matrix_1.2-12      Rcpp_0.12.16      
## [52] munsell_0.4.3      abind_1.4-5        stringi_1.1.7     
## [55] yaml_2.1.18        plyr_1.8.4         recipes_0.1.2     
## [58] grid_3.4.4         parallel_3.4.4     lattice_0.20-35   
## [61] splines_3.4.4      hms_0.4.2          pillar_1.2.1      
## [64] CVST_0.2-1         magic_1.5-8        urca_1.3-0        
## [67] glue_1.2.0         evaluate_0.10.1    httpuv_1.3.6.2    
## [70] cellranger_1.1.0   gtable_0.2.0       purrr_0.2.4       
## [73] kernlab_0.9-25     assertthat_0.2.0   DRR_0.0.3         
## [76] gower_0.1.2        mime_0.5           prodlim_2018.04.18
## [79] broom_0.4.4        uroot_2.0-9        viridisLite_0.3.0 
## [82] class_7.3-14       survival_2.41-3    geometry_0.3-6    
## [85] timeDate_3043.102  RcppRoll_0.2.2     tibble_1.4.2      
## [88] bindrcpp_0.2.2     lava_1.6.1         ipred_0.9-6
```
## Business Objective
The leadership has identified predicting employee turnover as its first application of data science for talent management. Before investing in the project they would like an analysis of existing employee data.  

## Data
Data was provided by the client in form of a .csv file "CaseStudy2-data.xlsx".

####Basic Statistics
The data includes a total of 1470 current and terminated employee records with 35 variables. 

```
##   "Observations" dim(CaseStudy2_data)
## 1   Observations                 1470
## 2   Observations                   35
```
<table class="table table-striped" style="width: auto !important; ">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Data Records </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Observations </td>
   <td style="text-align:right;"> 1470 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Variables </td>
   <td style="text-align:right;"> 35 </td>
  </tr>
</tbody>
</table>
Summary of measures included in the data:
<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> DailyRate </th>
   <th style="text-align:right;"> Number of Companies Worked </th>
   <th style="text-align:right;"> Years at Company </th>
   <th style="text-align:right;"> Years with Manager </th>
   <th style="text-align:right;"> Distance From Home </th>
   <th style="text-align:right;"> Percent Salary Hike </th>
   <th style="text-align:right;"> Years in Current Role </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Min. </td>
   <td style="text-align:right;"> 102.0000 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 1.000000 </td>
   <td style="text-align:right;"> 11.00000 </td>
   <td style="text-align:right;"> 0.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1st Qu. </td>
   <td style="text-align:right;"> 465.0000 </td>
   <td style="text-align:right;"> 1.000000 </td>
   <td style="text-align:right;"> 3.000000 </td>
   <td style="text-align:right;"> 2.000000 </td>
   <td style="text-align:right;"> 2.000000 </td>
   <td style="text-align:right;"> 12.00000 </td>
   <td style="text-align:right;"> 2.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Median </td>
   <td style="text-align:right;"> 802.0000 </td>
   <td style="text-align:right;"> 2.000000 </td>
   <td style="text-align:right;"> 5.000000 </td>
   <td style="text-align:right;"> 3.000000 </td>
   <td style="text-align:right;"> 7.000000 </td>
   <td style="text-align:right;"> 14.00000 </td>
   <td style="text-align:right;"> 3.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Mean </td>
   <td style="text-align:right;"> 802.4857 </td>
   <td style="text-align:right;"> 2.693197 </td>
   <td style="text-align:right;"> 7.008163 </td>
   <td style="text-align:right;"> 4.123129 </td>
   <td style="text-align:right;"> 9.192517 </td>
   <td style="text-align:right;"> 15.20952 </td>
   <td style="text-align:right;"> 4.229252 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 3rd Qu. </td>
   <td style="text-align:right;"> 1157.0000 </td>
   <td style="text-align:right;"> 4.000000 </td>
   <td style="text-align:right;"> 9.000000 </td>
   <td style="text-align:right;"> 7.000000 </td>
   <td style="text-align:right;"> 14.000000 </td>
   <td style="text-align:right;"> 18.00000 </td>
   <td style="text-align:right;"> 7.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Max. </td>
   <td style="text-align:right;"> 1499.0000 </td>
   <td style="text-align:right;"> 9.000000 </td>
   <td style="text-align:right;"> 40.000000 </td>
   <td style="text-align:right;"> 17.000000 </td>
   <td style="text-align:right;"> 29.000000 </td>
   <td style="text-align:right;"> 25.00000 </td>
   <td style="text-align:right;"> 18.000000 </td>
  </tr>
</tbody>
</table>
##Methodology
Attrition is the central theme of this analysis. We interpreted the value "Yes" in the data provided under attrition as an indicator that the employee is terminated.

We categorized each record as "Current" or "Terminated" and look for patterns in the variables that may explain why employees become terminated.  

*__Current__ meaning currently employed by the firm.*  
*__Terminated__ meaning left the firm (voluntarily or non-voluntarily)*

<img src="DDSAnalytics_files/figure-html/unnamed-chunk-4-1.png" style="display: block; margin: auto;" />

```
## [1] "tbl_df"     "tbl"        "data.frame"
```

```
## [1] "Female" "Male"
```

```
##  [1]  6 10  0  8  2  7  1  9  5  4 25  3 12 14 22 15 27 21 17 11 13 37 16
## [24] 20 40 24 33 19 36 18 29 31 32 34 26 30 23
```

```
## [1] "Yes" "No"
```
As requested employees under the age of 18 have been excluded from this analsyis. The table below shows the youngest age record included in the data:
<table class="table table-striped" style="width: auto !important; ">
 <thead>
  <tr>
   <th style="text-align:right;"> Youngest Age Record </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 18 </td>
  </tr>
</tbody>
</table>
####Distributions  
The following are the distributions of employees by various measures.
<img src="DDSAnalytics_files/figure-html/unnamed-chunk-7-1.png" style="display: block; margin: auto;" /><img src="DDSAnalytics_files/figure-html/unnamed-chunk-7-2.png" style="display: block; margin: auto;" />

<img src="DDSAnalytics_files/figure-html/unnamed-chunk-8-1.png" style="display: block; margin: auto;" />

####Frequencies  
The following are frequencies by Gender and Job Roles
<img src="DDSAnalytics_files/figure-html/unnamed-chunk-9-1.png" style="display: block; margin: auto;" />
<img src="DDSAnalytics_files/figure-html/unnamed-chunk-10-1.png" style="display: block; margin: auto auto auto 0;" />
  
As requested we have captured the counts of management positions in the table below:

<table class="table table-striped" style="width: auto !important; ">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Count </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Sales Executives </td>
   <td style="text-align:right;"> 326 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Manufacturing Directors </td>
   <td style="text-align:right;"> 145 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Managers </td>
   <td style="text-align:right;"> 102 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Research Directors </td>
   <td style="text-align:right;"> 80 </td>
  </tr>
</tbody>
</table>
####Is there a relationship between Age and Income?  
There's no apparent relationship between Age and Income. The plot below shows a very slight upward incline as age increases but is relatively insignificant.  
<img src="DDSAnalytics_files/figure-html/unnamed-chunk-13-1.png" style="display: block; margin: auto;" />





####What are the top 3 factors that lead to attrition?

Using the Stepwise Variable selction method we have determined that the most effective predictors of years with the company are Years with Current Manager, Training Times Last Year,	Years In CurrentRole,	Years Since Last Promotion,	Number of Companies Worked,	Age,	Monthly Income,	Job Involvement, Percent Salary Hike and DailyRate.

These factors can be used to predict how long in years an employee will stay with the company using a statistical formula.

We advise caution be used in decision making based on the following variables for ethical or even legal reasons:  

* Gender  
* Marital Status  
* Relationship Satisfaction  
* Total Working Years
* Age

Our model actually only uses one of these factors (Age) which if used as a factor in decision making could be considered discriminatory therefore this analysis should be used with caution.

Inference can only be drawn to the employees in our dataset and not an larger external population.

```
## Stepwise Selection Method   
## ---------------------------
## 
## Candidate Terms: 
## 
## 1. Age 
## 2. DailyRate 
## 3. DistanceFromHome 
## 4. Education 
## 5. EnvironmentSatisfaction 
## 6. HourlyRate 
## 7. JobInvolvement 
## 8. JobLevel 
## 9. JobSatisfaction 
## 10. MonthlyIncome 
## 11. MonthlyRate 
## 12. NumCompaniesWorked 
## 13. PercentSalaryHike 
## 14. PerformanceRating 
## 15. RelationshipSatisfaction 
## 16. StockOptionLevel 
## 17. TotalWorkingYears 
## 18. TrainingTimesLastYear 
## 19. WorkLifeBalance 
## 20. YearsInCurrentRole 
## 21. YearsSinceLastPromotion 
## 22. YearsWithCurrManager 
## 
## We are selecting variables based on p value...
## 
## Variables Entered/Removed: 
## 
## - YearsWithCurrManager added 
## - TrainingTimesLastYear added 
## - YearsInCurrentRole added 
## - YearsSinceLastPromotion added 
## - NumCompaniesWorked added 
## - Age added 
## - MonthlyIncome added 
## - JobInvolvement added 
## - PercentSalaryHike added 
## - DailyRate added 
## 
## No more variables to be added/removed.
## 
## 
## Final Model Output 
## ------------------
## 
##                         Model Summary                          
## --------------------------------------------------------------
## R                       0.884       RMSE                2.877 
## R-Squared               0.781       Coef. Var          41.051 
## Adj. R-Squared          0.779       MSE                 8.277 
## Pred R-Squared          0.775       MAE                 1.897 
## --------------------------------------------------------------
##  RMSE: Root Mean Square Error 
##  MSE: Mean Square Error 
##  MAE: Mean Absolute Error 
## 
##                                  ANOVA                                   
## ------------------------------------------------------------------------
##                  Sum of                                                 
##                 Squares          DF    Mean Square       F         Sig. 
## ------------------------------------------------------------------------
## Regression    43062.379          10       4306.238    520.292    0.0000 
## Residual      12075.523        1459          8.277                      
## Total         55137.902        1469                                     
## ------------------------------------------------------------------------
## 
##                                         Parameter Estimates                                          
## ----------------------------------------------------------------------------------------------------
##                   model      Beta    Std. Error    Std. Beta      t        Sig      lower     upper 
## ----------------------------------------------------------------------------------------------------
##             (Intercept)     2.117         0.563                  3.756    0.000     1.011     3.222 
##    YearsWithCurrManager     0.563         0.032        0.328    17.770    0.000     0.500     0.625 
##   TrainingTimesLastYear     0.240         0.020        0.305    12.143    0.000     0.202     0.279 
##      YearsInCurrentRole     0.468         0.032        0.277    14.780    0.000     0.406     0.530 
## YearsSinceLastPromotion     0.310         0.029        0.163    10.714    0.000     0.254     0.367 
##      NumCompaniesWorked    -0.286         0.033       -0.117    -8.769    0.000    -0.350    -0.222 
##                     Age    -0.030         0.012       -0.045    -2.589    0.010    -0.053    -0.007 
##           MonthlyIncome     0.000         0.000        0.047     2.443    0.015     0.000     0.000 
##          JobInvolvement    -0.191         0.106       -0.022    -1.807    0.071    -0.399     0.016 
##       PercentSalaryHike    -0.036         0.021       -0.021    -1.742    0.082    -0.076     0.005 
##               DailyRate     0.000         0.000       -0.021    -1.716    0.086    -0.001     0.000 
## ----------------------------------------------------------------------------------------------------
```

```
## 
##                                       Stepwise Selection Summary                                        
## -------------------------------------------------------------------------------------------------------
##                                     Added/                   Adj.                                          
## Step           Variable            Removed     R-Square    R-Square      C(p)          AIC        RMSE     
## -------------------------------------------------------------------------------------------------------
##    1     YearsWithCurrManager      addition       0.592       0.591    1244.3580    8189.0915    3.9161    
##    2     TrainingTimesLastYear     addition       0.687       0.687     610.6050    7798.1456    3.4274    
##    3      YearsInCurrentRole       addition       0.744       0.744     234.6420    7504.4996    3.1005    
##    4    YearsSinceLastPromotion    addition       0.764       0.763     107.8300    7390.4311    2.9815    
##    5      NumCompaniesWorked       addition       0.777       0.777      19.5680    7305.2675    2.8954    
##    6              Age              addition       0.779       0.778      13.4860    7299.2046    2.8885    
##    7         MonthlyIncome         addition       0.780       0.779       9.2750    7294.9777    2.8833    
##    8        JobInvolvement         addition       0.780       0.779       7.8470    7293.5298    2.8810    
##    9       PercentSalaryHike       addition       0.781       0.779       6.6830    7292.3412    2.8788    
##   10           DailyRate           addition       0.781       0.779       5.7510    7291.3789    2.8769    
## -------------------------------------------------------------------------------------------------------
```


The top 3 factors that predict how long an employee will stay with the company in years are Years With Current Manager, Training Times Last Year and YearsInCurrentRole    

Though this analysis is significant it is merely a proof of concept; higher quality results can be achieved wiht additional time and resources for analyzing the data.

####Appendix

```
## Stepwise Selection Method   
## ---------------------------
## 
## Candidate Terms: 
## 
## 1. Age 
## 2. DailyRate 
## 3. DistanceFromHome 
## 4. Education 
## 5. EnvironmentSatisfaction 
## 6. HourlyRate 
## 7. JobInvolvement 
## 8. JobLevel 
## 9. JobSatisfaction 
## 10. MonthlyIncome 
## 11. MonthlyRate 
## 12. NumCompaniesWorked 
## 13. PercentSalaryHike 
## 14. PerformanceRating 
## 15. RelationshipSatisfaction 
## 16. StockOptionLevel 
## 17. TotalWorkingYears 
## 18. TrainingTimesLastYear 
## 19. WorkLifeBalance 
## 20. YearsInCurrentRole 
## 21. YearsSinceLastPromotion 
## 22. YearsWithCurrManager 
## 
## We are selecting variables based on p value...
## 
## Variables Entered/Removed: 
## 
## - YearsWithCurrManager added 
## - TrainingTimesLastYear added 
## - YearsInCurrentRole added 
## - YearsSinceLastPromotion added 
## - NumCompaniesWorked added 
## - Age added 
## - MonthlyIncome added 
## - JobInvolvement added 
## - PercentSalaryHike added 
## - DailyRate added 
## 
## No more variables to be added/removed.
## 
## 
## Final Model Output 
## ------------------
## 
##                         Model Summary                          
## --------------------------------------------------------------
## R                       0.884       RMSE                2.877 
## R-Squared               0.781       Coef. Var          41.051 
## Adj. R-Squared          0.779       MSE                 8.277 
## Pred R-Squared          0.775       MAE                 1.897 
## --------------------------------------------------------------
##  RMSE: Root Mean Square Error 
##  MSE: Mean Square Error 
##  MAE: Mean Absolute Error 
## 
##                                  ANOVA                                   
## ------------------------------------------------------------------------
##                  Sum of                                                 
##                 Squares          DF    Mean Square       F         Sig. 
## ------------------------------------------------------------------------
## Regression    43062.379          10       4306.238    520.292    0.0000 
## Residual      12075.523        1459          8.277                      
## Total         55137.902        1469                                     
## ------------------------------------------------------------------------
## 
##                                         Parameter Estimates                                          
## ----------------------------------------------------------------------------------------------------
##                   model      Beta    Std. Error    Std. Beta      t        Sig      lower     upper 
## ----------------------------------------------------------------------------------------------------
##             (Intercept)     2.117         0.563                  3.756    0.000     1.011     3.222 
##    YearsWithCurrManager     0.563         0.032        0.328    17.770    0.000     0.500     0.625 
##   TrainingTimesLastYear     0.240         0.020        0.305    12.143    0.000     0.202     0.279 
##      YearsInCurrentRole     0.468         0.032        0.277    14.780    0.000     0.406     0.530 
## YearsSinceLastPromotion     0.310         0.029        0.163    10.714    0.000     0.254     0.367 
##      NumCompaniesWorked    -0.286         0.033       -0.117    -8.769    0.000    -0.350    -0.222 
##                     Age    -0.030         0.012       -0.045    -2.589    0.010    -0.053    -0.007 
##           MonthlyIncome     0.000         0.000        0.047     2.443    0.015     0.000     0.000 
##          JobInvolvement    -0.191         0.106       -0.022    -1.807    0.071    -0.399     0.016 
##       PercentSalaryHike    -0.036         0.021       -0.021    -1.742    0.082    -0.076     0.005 
##               DailyRate     0.000         0.000       -0.021    -1.716    0.086    -0.001     0.000 
## ----------------------------------------------------------------------------------------------------
```

```
## 
##                                       Stepwise Selection Summary                                        
## -------------------------------------------------------------------------------------------------------
##                                     Added/                   Adj.                                          
## Step           Variable            Removed     R-Square    R-Square      C(p)          AIC        RMSE     
## -------------------------------------------------------------------------------------------------------
##    1     YearsWithCurrManager      addition       0.592       0.591    1244.3580    8189.0915    3.9161    
##    2     TrainingTimesLastYear     addition       0.687       0.687     610.6050    7798.1456    3.4274    
##    3      YearsInCurrentRole       addition       0.744       0.744     234.6420    7504.4996    3.1005    
##    4    YearsSinceLastPromotion    addition       0.764       0.763     107.8300    7390.4311    2.9815    
##    5      NumCompaniesWorked       addition       0.777       0.777      19.5680    7305.2675    2.8954    
##    6              Age              addition       0.779       0.778      13.4860    7299.2046    2.8885    
##    7         MonthlyIncome         addition       0.780       0.779       9.2750    7294.9777    2.8833    
##    8        JobInvolvement         addition       0.780       0.779       7.8470    7293.5298    2.8810    
##    9       PercentSalaryHike       addition       0.781       0.779       6.6830    7292.3412    2.8788    
##   10           DailyRate           addition       0.781       0.779       5.7510    7291.3789    2.8769    
## -------------------------------------------------------------------------------------------------------
```

```
## 
## Call:
## lm(formula = YearsAtCompany ~ YearsWithCurrManager + TrainingTimesLastYear + 
##     YearsInCurrentRole + YearsSinceLastPromotion + NumCompaniesWorked + 
##     Age + MonthlyIncome + JobInvolvement + PercentSalaryHike + 
##     DailyRate, data = MyPredictionData)
## 
## Coefficients:
##             (Intercept)     YearsWithCurrManager    TrainingTimesLastYear  
##               2.117e+00                5.626e-01                2.404e-01  
##      YearsInCurrentRole  YearsSinceLastPromotion       NumCompaniesWorked  
##               4.678e-01                3.104e-01               -2.857e-01  
##                     Age            MonthlyIncome           JobInvolvement  
##              -2.995e-02                6.177e-05               -1.914e-01  
##       PercentSalaryHike                DailyRate  
##              -3.578e-02               -3.204e-04
```

![](DDSAnalytics_files/figure-html/unnamed-chunk-18-1.png)<!-- -->![](DDSAnalytics_files/figure-html/unnamed-chunk-18-2.png)<!-- -->![](DDSAnalytics_files/figure-html/unnamed-chunk-18-3.png)<!-- -->![](DDSAnalytics_files/figure-html/unnamed-chunk-18-4.png)<!-- -->
