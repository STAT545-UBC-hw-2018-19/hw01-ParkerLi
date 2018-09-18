This file is for the first assignment of the course STAT545A. It aims to
explore a dataset via using R Markdown.

Setting Up
----------

    install.packages("cem",repos = "http://cran.us.r-project.org")

    ## 
    ## The downloaded binary packages are in
    ##  /var/folders/s3/tl0mpflj60j51p2q8pq58fg00000gp/T//RtmpI460Qc/downloaded_packages

    library(cem)

    ## Loading required package: tcltk

    ## Loading required package: lattice

    ## 
    ## How to use CEM? Type vignette("cem")

    data(LL)
    data <- LL
    colnames(data)

    ##  [1] "treated"   "age"       "education" "black"     "married"  
    ##  [6] "nodegree"  "re74"      "re75"      "re78"      "hispanic" 
    ## [11] "u74"       "u75"

This part shows the package and dataset installation process. It also
gives the variable names.

Basic Data Frame Exploration
----------------------------

    re74.bar <- mean(LL$re74)
    re74.bar

    ## [1] 3630.738

    median(LL$re74)

    ## [1] 823.8215

    summary(LL$re74)

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##     0.0     0.0   823.8  3630.7  5211.8 39570.7

    summary(LL)

    ##     treated            age          education         black       
    ##  Min.   :0.0000   Min.   :17.00   Min.   : 3.00   Min.   :0.0000  
    ##  1st Qu.:0.0000   1st Qu.:19.00   1st Qu.: 9.00   1st Qu.:1.0000  
    ##  Median :0.0000   Median :23.00   Median :10.00   Median :1.0000  
    ##  Mean   :0.4114   Mean   :24.52   Mean   :10.27   Mean   :0.8006  
    ##  3rd Qu.:1.0000   3rd Qu.:27.00   3rd Qu.:11.00   3rd Qu.:1.0000  
    ##  Max.   :1.0000   Max.   :55.00   Max.   :16.00   Max.   :1.0000  
    ##     married         nodegree           re74              re75        
    ##  Min.   :0.000   Min.   :0.0000   Min.   :    0.0   Min.   :    0.0  
    ##  1st Qu.:0.000   1st Qu.:1.0000   1st Qu.:    0.0   1st Qu.:    0.0  
    ##  Median :0.000   Median :1.0000   Median :  823.8   Median :  936.3  
    ##  Mean   :0.162   Mean   :0.7798   Mean   : 3630.7   Mean   : 3042.9  
    ##  3rd Qu.:0.000   3rd Qu.:1.0000   3rd Qu.: 5211.8   3rd Qu.: 3993.2  
    ##  Max.   :1.000   Max.   :1.0000   Max.   :39570.7   Max.   :37431.7  
    ##       re78          hispanic           u74              u75        
    ##  Min.   :    0   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:    0   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median : 3952   Median :0.0000   Median :0.0000   Median :0.0000  
    ##  Mean   : 5455   Mean   :0.1053   Mean   :0.4529   Mean   :0.4003  
    ##  3rd Qu.: 8772   3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:1.0000  
    ##  Max.   :60308   Max.   :1.0000   Max.   :1.0000   Max.   :1.0000

    table(LL$black)

    ## 
    ##   0   1 
    ## 144 578

    which.max(table(LL$education))

    ## 11 
    ##  9

    table(LL$education)

    ## 
    ##   3   4   5   6   7   8   9  10  11  12  13  14  15  16 
    ##   1   6   5   7  15  62 110 162 195 122  23  11   2   1

    freq.education <- table(LL$education)
    which.max(freq.education)

    ## 11 
    ##  9

    prop.table(table(LL$education))

    ## 
    ##           3           4           5           6           7           8 
    ## 0.001385042 0.008310249 0.006925208 0.009695291 0.020775623 0.085872576 
    ##           9          10          11          12          13          14 
    ## 0.152354571 0.224376731 0.270083102 0.168975069 0.031855956 0.015235457 
    ##          15          16 
    ## 0.002770083 0.001385042

    prop.table(table(LL$education))*100

    ## 
    ##          3          4          5          6          7          8 
    ##  0.1385042  0.8310249  0.6925208  0.9695291  2.0775623  8.5872576 
    ##          9         10         11         12         13         14 
    ## 15.2354571 22.4376731 27.0083102 16.8975069  3.1855956  1.5235457 
    ##         15         16 
    ##  0.2770083  0.1385042

This section explores the mean and median of one variable within a
dataframe. Furthermore, it summaries statistics of all variables within
a dataframe and gives different styles of count/frenquency tables.

Measures of Dispersion
======================

    var(LL$re74)

    ## [1] 38696328

    sd(LL$re74)

    ## [1] 6220.637

    install.packages("moments",repos = "http://cran.us.r-project.org")

    ## 
    ## The downloaded binary packages are in
    ##  /var/folders/s3/tl0mpflj60j51p2q8pq58fg00000gp/T//RtmpI460Qc/downloaded_packages

    library(moments)
    skewness(LL$re74)

    ## [1] 2.766771

    kurtosis(LL$re74)

    ## [1] 12.19937

    sd.re74 <- sqrt(var(LL$re74))
    sd.re74

    ## [1] 6220.637

This section measuares dispersion: variance, standard deviation,
skewness, and kurtosis.

T-test
======

    t.test(LL$re74, mu=6059, alternative="less")

    ## 
    ##  One Sample t-test
    ## 
    ## data:  LL$re74
    ## t = -10.489, df = 721, p-value < 2.2e-16
    ## alternative hypothesis: true mean is less than 6059
    ## 95 percent confidence interval:
    ##      -Inf 4012.025
    ## sample estimates:
    ## mean of x 
    ##  3630.738

    t.test(re78 ~ treated, data=LL, alternative = "less", var.equal=FALSE)

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  re78 by treated
    ## t = -1.8154, df = 557.06, p-value = 0.035
    ## alternative hypothesis: true difference in means is less than 0
    ## 95 percent confidence interval:
    ##       -Inf -81.94117
    ## sample estimates:
    ## mean in group 0 mean in group 1 
    ##        5090.048        5976.352

    LL.0 <- subset(LL, treated==0)
    t.test(LL.0$re74, LL.0$re78, alternative = "less", paired = TRUE)

    ## 
    ##  Paired t-test
    ## 
    ## data:  LL.0$re74 and LL.0$re78
    ## t = -3.8458, df = 424, p-value = 6.93e-05
    ## alternative hypothesis: true difference in means is less than 0
    ## 95 percent confidence interval:
    ##      -Inf -809.946
    ## sample estimates:
    ## mean of the differences 
    ##               -1417.563

    LL.1 <- subset(LL, treated==1)
    t.test(LL.1$re74, LL.1$re78, alternative = "less", paired = TRUE)

    ## 
    ##  Paired t-test
    ## 
    ## data:  LL.1$re74 and LL.1$re78
    ## t = -4.7241, df = 296, p-value = 1.788e-06
    ## alternative hypothesis: true difference in means is less than 0
    ## 95 percent confidence interval:
    ##       -Inf -1565.224
    ## sample estimates:
    ## mean of the differences 
    ##               -2405.353

This chunk does the one-sample t-test and two-sample t-test (both
independet samples and dependet samples).

Cross-Tabulations and Correlation
=================================

    install.packages("gmodels",repos = "http://cran.us.r-project.org")

    ## 
    ## The downloaded binary packages are in
    ##  /var/folders/s3/tl0mpflj60j51p2q8pq58fg00000gp/T//RtmpI460Qc/downloaded_packages

    library(gmodels)
    CrossTable(y=LL$u75, x=LL$treated)

    ## 
    ##  
    ##    Cell Contents
    ## |-------------------------|
    ## |                       N |
    ## | Chi-square contribution |
    ## |           N / Row Total |
    ## |           N / Col Total |
    ## |         N / Table Total |
    ## |-------------------------|
    ## 
    ##  
    ## Total Observations in Table:  722 
    ## 
    ##  
    ##              | LL$u75 
    ##   LL$treated |         0 |         1 | Row Total | 
    ## -------------|-----------|-----------|-----------|
    ##            0 |       247 |       178 |       425 | 
    ##              |     0.244 |     0.365 |           | 
    ##              |     0.581 |     0.419 |     0.589 | 
    ##              |     0.570 |     0.616 |           | 
    ##              |     0.342 |     0.247 |           | 
    ## -------------|-----------|-----------|-----------|
    ##            1 |       186 |       111 |       297 | 
    ##              |     0.349 |     0.523 |           | 
    ##              |     0.626 |     0.374 |     0.411 | 
    ##              |     0.430 |     0.384 |           | 
    ##              |     0.258 |     0.154 |           | 
    ## -------------|-----------|-----------|-----------|
    ## Column Total |       433 |       289 |       722 | 
    ##              |     0.600 |     0.400 |           | 
    ## -------------|-----------|-----------|-----------|
    ## 
    ## 

    CrossTable(y=LL$u75, x=LL$treated, prop.c=TRUE,
    prop.r=FALSE, prop.t= FALSE, prop.chisq=FALSE, chisq=TRUE,
    format="SPSS")

    ## 
    ##    Cell Contents
    ## |-------------------------|
    ## |                   Count |
    ## |          Column Percent |
    ## |-------------------------|
    ## 
    ## Total Observations in Table:  722 
    ## 
    ##              | LL$u75 
    ##   LL$treated |        0  |        1  | Row Total | 
    ## -------------|-----------|-----------|-----------|
    ##            0 |      247  |      178  |      425  | 
    ##              |   57.044% |   61.592% |           | 
    ## -------------|-----------|-----------|-----------|
    ##            1 |      186  |      111  |      297  | 
    ##              |   42.956% |   38.408% |           | 
    ## -------------|-----------|-----------|-----------|
    ## Column Total |      433  |      289  |      722  | 
    ##              |   59.972% |   40.028% |           | 
    ## -------------|-----------|-----------|-----------|
    ## 
    ##  
    ## Statistics for All Table Factors
    ## 
    ## 
    ## Pearson's Chi-squared test 
    ## ------------------------------------------------------------
    ## Chi^2 =  1.480414     d.f. =  1     p =  0.2237097 
    ## 
    ## Pearson's Chi-squared test with Yates' continuity correction 
    ## ------------------------------------------------------------
    ## Chi^2 =  1.298555     d.f. =  1     p =  0.2544773 
    ## 
    ##  
    ##        Minimum expected frequency: 118.8823

    cor(LL$education, LL$re74)

    ## [1] 0.08916458

The final section gives a further data exploration of cross-tabluation
and correlation.
