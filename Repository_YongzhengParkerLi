# Homework 01, STAT 545A, UBC, Yongzheng Parker Li

This page has three sections: *About This Page*, *About Me*, and *About My Favorite R Code*.

## About This Page

This repository is the homepage of *Homework 01* of the course STAT545A, taught by [Vincenzo Coia](https://github.com/vincenzocoia) at the University of British Columbia (UBC). The detailed requirements of this assignment could be found [here](http://stat545.com/Classroom/assignments/hw01/hw01.html). The STAT545A course page is [here](http://stat545.com/Classroom/). This assignment is finished directly on the GitHub website.

Registration info:
- Name: Yongzheng Li
- Preferred Name: Parker
- Student ID: 9917 4161
- UBC email: parker.li@ubc.ca
- Preferred email: parker.lyz@gmail.com
- I am an *auditing* student in this course. My GitHub participation repository for this course is here: [ParkerLi](https://github.com/ParkerLi/STAT545_participation).

## About Me

My name is **Yongzheng Parker Li**, a second-year MA student in the [Department of Political Science](https://politics.ubc.ca/), UBC. Some quick facts about me:

- My research focuses on the relationship between *economic globalization* and *income inequality*.
- I received my BSc. in the [Hong Kong University of Science and Technology](https://www.ust.hk/).
- I strongly **dislike** social media and emojis. :thumbsdown: 
- I came to Vancouver last year, before that I had stayed in
  + Beijing, Hong Kong, Macao/China   
  + Osaka/Japan
  + Rome/Italy     
  + Bangkok/Thailand
  + Ann Arbor/US
  + Gagetown/Canada
    
One thing I want to highlight is that I am a movie geek and am doing a part-time movie critic job for a film magazine. [DeepFocus](http://www.filmdeepfocus.com/) has published several of my articles and here is one piece of my work: [All the Money in the World](https://www.douban.com/note/659425892/) (in Chinese). My favorite movie quote is from *Midnight in Paris*:

> "Nostalgia is denial - denial of the painful present... the name for this denial is golden age thinking - the erroneous notion that a different time period is better than the one ones living in - its a flaw in the romantic imagination of those people who find it difficult to cope with the present."

![](https://ih0.redbubble.net/image.12813797.9187/flat,550x550,075,f.u2.jpg)

# About My Favorite R Code

STAT545A is a **R** course. Let me finish this page with my favorite R code. But why is it my favorite? Let's look at the code first (hw4.dta is [here](https://www.dropbox.com/s/dugkz47wbq49j5q/hw4.dta?dl=0)):

```R
options(max.print=10000)

hw4.data <- read.dta("hw4.dta")
summary(hw4.data)
var(hw4.data$hgt,na.rm=TRUE)
1/2163.225
var(hw4.data$age)
1/47.52796
var(hw4.data$hc,na.rm = T)
1/34.97469
var(hw)

wgt <- hw4.data$wgt
age <- hw4.data$age
hgt <- hw4.data$hgt
hc <- hw4.data$hc
N <- length(hw4.data$wgt)

hw4.missing.data <- list("wgt","age","hgt","hc","N")

missing.params<-c("alpha", "beta", "hgt", "hc","age")

set.seed(123)
weight.mod <- function(){
  for (i in 1:N) {
    
    wgt[i] ~ dnorm( mu[i], tau)
    mu[i] <- alpha + beta[1] * hgt[i]+ beta[2] * age[i]+beta[3]*hc[i]
    
    hgt[i]~dnorm(132.15,0.0004622728)
    age[i]~dnorm(9.159,0.02104025)
    hc[i]~dnorm(51.51,0.0285921)
  }   
  
  for (i in 1:3) {
    beta[i] ~ dunif(-100, 100)
  }
  tau ~ dgamma(.5, .5)
  alpha~dunif(-100,100)
}

set.seed(123)
weight <- jags(data=hw4.missing.data, inits=NULL, missing.params, n.chains=2, n.iter=1000, n.burnin=100, model.file=weight.mod)

set.seed(123)
weight.upd <- autojags(weight,n.burnin=100)
print(weight.upd)
```
Because it is Bayesian? No, because it is the first R chunk I ever encountered in my life and I will never forget that inspiring R-introduction course at [ICRSR](https://www.icpsr.umich.edu/icpsrweb/), University of Michigan Ann Arbor.

Thank you! 
