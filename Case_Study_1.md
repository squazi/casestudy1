# Case Study 1
squazi  
March 21, 2017  
#Introduction
The following analyzes data that ranks the GDP of 190 countries with corresponding educational data for these countries.The intent is discover correlation/causation between financial success and education on an aggregate country level scale.
##The data files can be found at:
https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv
&
https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv
Header's are included in these comma seperated value files; however, similar variables between the data sets are not names synonymously. 

#Common abbreviaions:
-GDP: Gross Domestic Product
-Commonly understood abbreviations for countries: Can be referenced at http://www.worldatlas.com/aatlas/ctycodes.htm

#Pre-analyis
By viewing both tables, you can tell that there is an easily discernible unique variable between both tables, the trigram country code, however the dataset Monies does not label it. The variable names are also lacking as the first for observations are blanks and appear to be extensions of the variable names. Monies also has several non-useful blank variables.
The Brains dataset has a wide variety of usable variables, but some of them are redundant.
As a comical side note to this analysis, it seems that Monies leaves you empty, and Brains leaves you cluttered.

I will reread the table Monies, into the table GDP12 to acccomodate for the apparent title of the table that was trapped as a variable name.I will then trim an extraneous data from the merged data, then analyze

#Critical Questions on Merged Data
####Question 1
#####How many ID's match between the two data sets?
238
*The total number of observations; however, will have to be trimmed down to 190, as those are the countries we have rankings and GDP data for.

####Question 2
#####If the data is sorted in ascending order by GDP, what is the 13th country in the resulting data frame?
St. Kitts and Nevis. This is an island country in the Carribean located in a chain of islands on the Lesser Antilles.
It is known as the smalles sovereign state in the Western Hemisphere, both in population and area- yet it is 10 times the size of Tuvalu, the country with the lowest GDP on the list.

####Question 3
#####OECD Analysis
91.91304 is the mean of "High income: nonOECD" groups
32.96667 is the mean of "High income: OECD"
Organisation for Economic Co-operation and Development ("OECD") is an intergovernmental coalition that promotes economic development. As there are only 35 countries as members, and the average ranking of these countries is approximately 32, it can be concluded that whatever economic strategies this organization is conducting are working as they triumph in GDP over their similar situated, high-income, counterparts.

####Question 4
#####The distribution of GDP value of all countries, with color to indicate income groups

```
qplot(Ranking, GDPinUSD, data = mergedclean2, color = Income.Group)
```

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
