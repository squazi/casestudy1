# Case Study 1
squazi  
March 21, 2017  
#Introduction
##The following analyzes data that ranks the GDP of 190 countries with corresponding educational data for these countries.The intent is discover correlation/causation between financial success and education on an aggregate country level scale.
##The data files can be found at:
##https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv
##&
##https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv
##Header's are included in these comma seperated value files; however, similar variables between the data sets are not names synonymously. 

#Common abbreviaions:
##-GDP: Gross Domestic Product
##-Commonly understood abbreviations for countries: Can be referenced at ##http://www.worldatlas.com/aatlas/ctycodes.htm

##By viewing both tables, you can tell that there is an easily discernible unique variable between both tables, the trigram country code, however the dataset Monies does not label it. The variable names are also lacking as the first for observations are blanks and appear to be extensions of the variable names. Monies also has several non-useful blank variables.
##The Brains dataset has a wide variety of usable variables, but some of them are redundant.
##As a comical side note to this analysis, it seems that Monies leaves you empty, and Brains leaves you cluttered.

##I will reread the table Monies, into the table GDP12 to acccomodate for the apparent title of the table that was trapped as a variable name.

#Question 1
##How many of the short codes match?
###238
#Question 2
###St. Kitts and Nevis
#Question 3
###91.91304 is the mean of "High income: nonOECD" groups
###32.96667 is the mean of High income: OECD
