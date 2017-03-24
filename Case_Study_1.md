# Case Study 1
squazi  
March 21 2017  
#Introduction
###The following analyzes data that ranks the GDP of 190 countries with corresponding educational data for these countries.The intent is discover correlation/causation between financial success and education on an aggregate country level scale.
###The data files can be found at: https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv
###&
###https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv
###Header's are included in these comma seperated value files; however, similar variables between the data sets are not names synonymously. 

#Common abbreviaions:
###-GDP: Gross Domestic Product
###-Commonly understood abbreviations for countries: Can be referenced at http://www.worldatlas.com/aatlas/ctycodes.htm

#Pre-analyis
#####By viewing both tables, you can tell that there is an easily discernible unique variable between both tables, the trigram country code, however the dataset Monies does not label it. The variable names are also lacking as the first for observations are blanks and appear to be extensions of the variable names. Monies also has several non-useful blank variables.
####The Brains dataset has a wide variety of usable variables, but some of them are redundant.
#####As a comical side note to this analysis, it seems that Monies leaves you empty, and Brains leaves you cluttered.

####I will reread the table Monies, into the table GDP12 to acccomodate for the apparent title of the table that was trapped as a variable name.I will then trim an extraneous data from the merged data, then analyze.


```r
library(repmis)
library(dplyr)
```

```
## Warning: package 'dplyr' was built under R version 3.3.3
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

```r
library(tidyr)
```

```
## Warning: package 'tidyr' was built under R version 3.3.3
```

```r
library(ggplot2)
getwd()
```

```
## [1] "C:/Users/esunqua/Documents/R/Case Study 1"
```

```r
setwd("C:/Users/esunqua/Documents/R/Case Study 1")
getwd()
```

```
## [1] "C:/Users/esunqua/Documents/R/Case Study 1"
```

```r
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv",destfile="./GDP.csv")
list.files()
```

```
## [1] "~$Code.docx"          "Case Study 1.Rmd"     "Case_Study_1.html"   
## [4] "Case_Study_1.md"      "Case_Study_1.Rmd"     "Code.docx"           
## [7] "EDU.csv"              "GDP.csv"              "obs-casestudy1.RData"
```

```r
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv",destfile="./EDU.csv")
list.files()
```

```
## [1] "~$Code.docx"          "Case Study 1.Rmd"     "Case_Study_1.html"   
## [4] "Case_Study_1.md"      "Case_Study_1.Rmd"     "Code.docx"           
## [7] "EDU.csv"              "GDP.csv"              "obs-casestudy1.RData"
```

```r
Monies <-read.csv("GDP.csv", header = TRUE)
head(Monies)
```

```
##     X Gross.domestic.product.2012 X.1           X.2          X.3 X.4 X.5
## 1                                  NA                                 NA
## 2                                  NA               (millions of      NA
## 3                         Ranking  NA       Economy  US dollars)      NA
## 4                                  NA                                 NA
## 5 USA                           1  NA United States  16,244,600       NA
## 6 CHN                           2  NA         China   8,227,103       NA
##   X.6 X.7 X.8
## 1  NA  NA  NA
## 2  NA  NA  NA
## 3  NA  NA  NA
## 4  NA  NA  NA
## 5  NA  NA  NA
## 6  NA  NA  NA
```

```r
Brains <-read.csv("EDU.csv", header = TRUE)
str(Brains)
```

```
## 'data.frame':	234 obs. of  31 variables:
##  $ CountryCode                                      : Factor w/ 234 levels "ABW","ADO","AFG",..: 1 2 3 4 5 6 7 8 9 10 ...
##  $ Long.Name                                        : Factor w/ 234 levels "American Samoa",..: 5 104 57 99 108 226 4 109 1 2 ...
##  $ Income.Group                                     : Factor w/ 6 levels "","High income: nonOECD",..: 2 2 4 5 6 2 6 5 6 6 ...
##  $ Region                                           : Factor w/ 8 levels "","East Asia & Pacific",..: 4 3 7 8 3 5 4 3 2 4 ...
##  $ Lending.category                                 : Factor w/ 4 levels "","Blend","IBRD",..: 1 1 4 4 3 1 3 2 1 3 ...
##  $ Other.groups                                     : Factor w/ 3 levels "","Euro area",..: 1 1 3 1 1 1 1 1 1 1 ...
##  $ Currency.Unit                                    : Factor w/ 155 levels "","Afghan afghani",..: 8 49 2 5 3 144 6 7 145 44 ...
##  $ Latest.population.census                         : Factor w/ 28 levels "","1970","1979",..: 17 28 3 2 18 22 18 18 17 18 ...
##  $ Latest.household.survey                          : Factor w/ 56 levels "","CPS (monthly)",..: 1 1 39 38 40 1 1 16 1 1 ...
##  $ Special.Notes                                    : Factor w/ 70 levels "","A simple multiplier is used to convert the national currencies of EMU members to euros. The following irrevocable euro conversi"| __truncated__,..: 1 1 27 1 1 1 1 1 1 63 ...
##  $ National.accounts.base.year                      : Factor w/ 44 levels "","1954","1973",..: 25 1 38 28 1 25 22 1 1 18 ...
##  $ National.accounts.reference.year                 : int  NA NA NA NA 1996 NA NA 1996 NA NA ...
##  $ System.of.National.Accounts                      : int  NA NA NA NA 1993 NA 1993 1993 NA NA ...
##  $ SNA.price.valuation                              : Factor w/ 3 levels "","VAB","VAP": 1 1 2 3 2 2 2 2 1 2 ...
##  $ Alternative.conversion.factor                    : Factor w/ 33 levels "","1960-85","1965-84",..: 1 1 1 24 1 1 6 21 1 1 ...
##  $ PPP.survey.year                                  : int  NA NA NA 2005 2005 NA 2005 2005 NA NA ...
##  $ Balance.of.Payments.Manual.in.use                : Factor w/ 3 levels "","BPM4","BPM5": 1 1 1 3 3 2 3 3 1 3 ...
##  $ External.debt.Reporting.status                   : Factor w/ 4 levels "","Actual","Estimate",..: 1 1 2 2 2 1 2 2 1 1 ...
##  $ System.of.trade                                  : Factor w/ 3 levels "","General","Special": 3 2 2 3 2 2 3 3 1 2 ...
##  $ Government.Accounting.concept                    : Factor w/ 3 levels "","Budgetary",..: 1 1 3 1 3 3 3 3 1 1 ...
##  $ IMF.data.dissemination.standard                  : Factor w/ 3 levels "","GDDS","SDDS": 1 1 2 2 2 2 3 3 1 2 ...
##  $ Source.of.most.recent.Income.and.expenditure.data: Factor w/ 77 levels "","1-2-3, 2005-06",..: 1 1 1 35 66 1 45 46 1 1 ...
##  $ Vital.registration.complete                      : Factor w/ 2 levels "","Yes": 1 2 1 1 2 1 2 2 2 2 ...
##  $ Latest.agricultural.census                       : Factor w/ 45 levels "","1960","1964-65",..: 1 1 1 3 32 32 41 1 1 1 ...
##  $ Latest.industrial.data                           : int  NA NA NA NA 2005 NA 2001 NA NA NA ...
##  $ Latest.trade.data                                : int  2008 2006 2008 1991 2008 2008 2008 2008 NA 2007 ...
##  $ Latest.water.withdrawal.data                     : int  NA NA 2000 2000 2000 2005 2000 2000 NA 1990 ...
##  $ X2.alpha.code                                    : Factor w/ 208 levels "","AD","AE","AF",..: 13 2 4 8 6 3 9 7 10 5 ...
##  $ WB.2.code                                        : Factor w/ 209 levels "","AD","AE","AF",..: 13 2 4 8 6 3 9 7 10 5 ...
##  $ Table.Name                                       : Factor w/ 234 levels "Afghanistan",..: 10 5 1 6 2 220 8 9 4 7 ...
##  $ Short.Name                                       : Factor w/ 234 levels "Afghanistan",..: 10 5 1 6 2 220 8 9 4 7 ...
```

```r
GDP12 <-Monies[-c(1,2,3,4), ]
GDP12 <-subset(GDP12, select = -X.1)
GDP12 <-GDP12[1:4]
names(GDP12)<- c("CountryCode","Ranking","CountryName","GDPinUSD")
GDP12sort<-arrange(GDP12,CountryCode)
GDP12short <-GDP12sort[-c(1:98), ]
mergeddata <-merge(x=GDP12short, y=Brains, by="CountryCode")
str(mergeddata)
```

```
## 'data.frame':	224 obs. of  34 variables:
##  $ CountryCode                                      : Factor w/ 229 levels "","ABW","ADO",..: 2 3 4 5 6 7 8 9 10 11 ...
##  $ Ranking                                          : Factor w/ 195 levels "",".. Not available.  ",..: 72 1 10 149 32 118 111 41 1 84 ...
##  $ CountryName                                      : Factor w/ 230 levels "","  East Asia & Pacific",..: 20 15 11 16 12 217 18 19 14 17 ...
##  $ GDPinUSD                                         : Factor w/ 207 levels ""," 1,008 "," 1,129 ",..: 65 192 68 24 26 109 134 186 192 5 ...
##  $ Long.Name                                        : Factor w/ 234 levels "American Samoa",..: 5 104 57 99 108 226 4 109 1 2 ...
##  $ Income.Group                                     : Factor w/ 6 levels "","High income: nonOECD",..: 2 2 4 5 6 2 6 5 6 6 ...
##  $ Region                                           : Factor w/ 8 levels "","East Asia & Pacific",..: 4 3 7 8 3 5 4 3 2 4 ...
##  $ Lending.category                                 : Factor w/ 4 levels "","Blend","IBRD",..: 1 1 4 4 3 1 3 2 1 3 ...
##  $ Other.groups                                     : Factor w/ 3 levels "","Euro area",..: 1 1 3 1 1 1 1 1 1 1 ...
##  $ Currency.Unit                                    : Factor w/ 155 levels "","Afghan afghani",..: 8 49 2 5 3 144 6 7 145 44 ...
##  $ Latest.population.census                         : Factor w/ 28 levels "","1970","1979",..: 17 28 3 2 18 22 18 18 17 18 ...
##  $ Latest.household.survey                          : Factor w/ 56 levels "","CPS (monthly)",..: 1 1 39 38 40 1 1 16 1 1 ...
##  $ Special.Notes                                    : Factor w/ 70 levels "","A simple multiplier is used to convert the national currencies of EMU members to euros. The following irrevocable euro conversi"| __truncated__,..: 1 1 27 1 1 1 1 1 1 63 ...
##  $ National.accounts.base.year                      : Factor w/ 44 levels "","1954","1973",..: 25 1 38 28 1 25 22 1 1 18 ...
##  $ National.accounts.reference.year                 : int  NA NA NA NA 1996 NA NA 1996 NA NA ...
##  $ System.of.National.Accounts                      : int  NA NA NA NA 1993 NA 1993 1993 NA NA ...
##  $ SNA.price.valuation                              : Factor w/ 3 levels "","VAB","VAP": 1 1 2 3 2 2 2 2 1 2 ...
##  $ Alternative.conversion.factor                    : Factor w/ 33 levels "","1960-85","1965-84",..: 1 1 1 24 1 1 6 21 1 1 ...
##  $ PPP.survey.year                                  : int  NA NA NA 2005 2005 NA 2005 2005 NA NA ...
##  $ Balance.of.Payments.Manual.in.use                : Factor w/ 3 levels "","BPM4","BPM5": 1 1 1 3 3 2 3 3 1 3 ...
##  $ External.debt.Reporting.status                   : Factor w/ 4 levels "","Actual","Estimate",..: 1 1 2 2 2 1 2 2 1 1 ...
##  $ System.of.trade                                  : Factor w/ 3 levels "","General","Special": 3 2 2 3 2 2 3 3 1 2 ...
##  $ Government.Accounting.concept                    : Factor w/ 3 levels "","Budgetary",..: 1 1 3 1 3 3 3 3 1 1 ...
##  $ IMF.data.dissemination.standard                  : Factor w/ 3 levels "","GDDS","SDDS": 1 1 2 2 2 2 3 3 1 2 ...
##  $ Source.of.most.recent.Income.and.expenditure.data: Factor w/ 77 levels "","1-2-3, 2005-06",..: 1 1 1 35 66 1 45 46 1 1 ...
##  $ Vital.registration.complete                      : Factor w/ 2 levels "","Yes": 1 2 1 1 2 1 2 2 2 2 ...
##  $ Latest.agricultural.census                       : Factor w/ 45 levels "","1960","1964-65",..: 1 1 1 3 32 32 41 1 1 1 ...
##  $ Latest.industrial.data                           : int  NA NA NA NA 2005 NA 2001 NA NA NA ...
##  $ Latest.trade.data                                : int  2008 2006 2008 1991 2008 2008 2008 2008 NA 2007 ...
##  $ Latest.water.withdrawal.data                     : int  NA NA 2000 2000 2000 2005 2000 2000 NA 1990 ...
##  $ X2.alpha.code                                    : Factor w/ 208 levels "","AD","AE","AF",..: 13 2 4 8 6 3 9 7 10 5 ...
##  $ WB.2.code                                        : Factor w/ 209 levels "","AD","AE","AF",..: 13 2 4 8 6 3 9 7 10 5 ...
##  $ Table.Name                                       : Factor w/ 234 levels "Afghanistan",..: 10 5 1 6 2 220 8 9 4 7 ...
##  $ Short.Name                                       : Factor w/ 234 levels "Afghanistan",..: 10 5 1 6 2 220 8 9 4 7 ...
```

```r
mergedclean <-mergeddata[-c(1:38), ]
mergedclean2 <-subset(x=mergedclean,  !is.na(Ranking))
mergedclean2$Ranking <-as.numeric(as.character(mergedclean2$Ranking))
mergedclean3 <-mergedclean2
mergedclean3$GDPinUSD <-gsub(",", "",mergedclean3$GDPinUSD)
mergedclean3$GDPinUSD <-as.numeric(as.character(mergedclean3$GDPinUSD))
```

```
## Warning: NAs introduced by coercion
```

```r
mergedclean2 <-arrange(mergedclean3,GDPinUSD)
mergedclean2 <-subset(x=mergedclean2,  !is.na(Ranking))
```
#Critical Questions on Merged Data
####Question 1
#####How many ID's match between the two data sets?
#####224
#####*The total number of observations; however, will have to be trimmed down to 190, as those are the countries we have rankings and GDP data for.

####Question 2
#####If the data is sorted in ascending order by GDP, what is the 13th country in the resulting data frame?
#####St. Kitts and Nevis. This is an island country in the Carribean located in a chain of islands on the Lesser Antilles.
######It is known as the smalles sovereign state in the Western Hemisphere, both in population and area- yet it is 10 times the size of Tuvalu, the country with the lowest GDP on the list.

####Question 3
#####OECD Analysis
######91.91304 is the mean of "High income: nonOECD" groups
######32.96667 is the mean of "High income: OECD"
######Organisation for Economic Co-operation and Development ("OECD") is an intergovernmental coalition that promotes economic development. As there are only 35 countries as members, and the average ranking of these countries is approximately 32, it can be concluded that whatever economic strategies this organization is conducting are working as they triumph in GDP over their similar situated, high-income, counterparts.

####Question 4
#####The distribution of GDP value of all countries, with color to indicate income groups


```r
qplot(Ranking, GDPinUSD, data = mergedclean2, color = Income.Group)
```

![](Case_Study_1_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

####Question 5
#####Summary Statistics for all 5 Income Groups


```
#High-Income & Non-OECD (dataframe reused from question 3)
summary(highOECD$GDPinUSD)
#High-Income & OECD (dataframe reused from question 3)
summary(highOECD2$GDPinUSD)
#Low-Income
low <-ifelse(mergedclean2$Income.Group == "Low income", mergedclean2$GDPinUSD, NA)
low <-low[!is.na(low)]
summary(low)
```
