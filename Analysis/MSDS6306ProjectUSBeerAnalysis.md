# MSDS630 1PROJECT US BEER ANALYSIS
Sanjay Kalluvilayil  
July 3, 2017  



## Introduction
The goal of this project is to assess the relationship between Alcohol Content by Volume (ABV) and  International Bitterness Units (IBU) in US beers.  An initial examination of two separate data      sets that contain beer and brewery data was conducted. These data sets were combined to enable the   analysis of beer data and metrics across the 50 states plus Washington, DC in the United States of  America.  The resulting conclusion is that there is a positive linear relationship with a           Pearson's correlation of 0.67 between Alcohol Content by Volume (ABV) and International             Bitterness Units (IBU) in US beers.


## Important
  * This data resides in the github directory
    https://github.com/sanjaystone/MSDS6306ProjectUSBeer.git
  * The deliverable includes the R Markdown file, Markdown file, and all relevant data sets 
  
## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button, a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

# Preparing the R Workspace
### R Workspace
The first step is preparing the R Workspace for use. The environment may be still filled with data and values, so we will use rm(list=ls()) to clear the workspace and clear it of any previous code.

### Installing & Loading Packages
Several packages will need to be installed and loaded to be able to conduct the full analysis.

### Session Info
This captures the session info for tracking purposes.


```r
rm(list=ls())
library(repmis)
```

```
## Warning: package 'repmis' was built under R version 3.4.1
```

```r
library(tidyr)
```

```
## Warning: package 'tidyr' was built under R version 3.4.1
```

```r
library(plyr)
```

```
## Warning: package 'plyr' was built under R version 3.4.1
```

```r
library(dplyr)
```

```
## Warning: package 'dplyr' was built under R version 3.4.1
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:plyr':
## 
##     arrange, count, desc, failwith, id, mutate, rename, summarise,
##     summarize
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
library(ggplot2)
sessionInfo()
```

```
## R version 3.4.0 (2017-04-21)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## Running under: Windows 10 x64 (build 15063)
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
## [1] ggplot2_2.2.1 dplyr_0.7.1   plyr_1.8.4    tidyr_0.6.3   repmis_0.5   
## 
## loaded via a namespace (and not attached):
##  [1] Rcpp_0.12.11      bindr_0.1         knitr_1.16       
##  [4] magrittr_1.5      munsell_0.4.3     colorspace_1.3-2 
##  [7] R.cache_0.12.0    R6_2.2.1          rlang_0.1.1      
## [10] stringr_1.2.0     httr_1.2.1        tools_3.4.0      
## [13] grid_3.4.0        gtable_0.2.0      data.table_1.10.4
## [16] R.oo_1.21.0       htmltools_0.3.6   lazyeval_0.2.0   
## [19] assertthat_0.2.0  yaml_2.1.14       rprojroot_1.2    
## [22] digest_0.6.12     tibble_1.3.1      bindrcpp_0.2     
## [25] R.utils_2.5.0     glue_1.1.0        evaluate_0.10    
## [28] rmarkdown_1.5     stringi_1.1.5     compiler_3.4.0   
## [31] scales_0.4.1      backports_1.1.0   R.methodsS3_1.7.1
## [34] pkgconfig_2.0.1
```
## Setting the Working Directories & Creating Sub Directories
To identify the current working directory, we used getwd().  To change the working directory, I used setwd("C:/RDATA") to the path specified path in the parenthesis. Sub-directories of folders were created to store Analysis and Data files.
### Git
In git, we opened the Git shell and cloned the Github repository. We ensured the initial working directory was set via  $ cd c:/RDATA.  We copied the Github repository by cloning the project via:  
git clone https://github.com/sanjaystone/MSDS6306ProjectUSBeer.git.  In addition, we created the Analysis folder with the Data as a sub-folder of the Analysis folder.


```r
getwd()
```

```
## [1] "C:/RDATA/MSDS6306ProjectUSBeer"
```

```r
dir.create ("/Analysis")
```

```
## Warning in dir.create("/Analysis"): '\Analysis' already exists
```

```r
dir.create ("/Analysis/Data")
```

```
## Warning in dir.create("/Analysis/Data"): '\Analysis\Data' already exists
```

# CREATING README.md FILE


```r
file.create("README.md")
```

```
## [1] TRUE
```

```r
cat("The of this project purpose is conduct an analysis of US Beer and Brewery data.
    
    INTRODUCTION
    The goal of this project is to assess the relationship between Alcohol Content by Volume (ABV)
    and International Bitterness Units (IBU) in US beers.  An initial examination of two separate
    data sets that contain beer and brewery data are conducted. These data sets are combined to
    enable the analysis of beer data and metrics across the 50 states plus Washington, DC in the
    United States of America.  The resulting conclusion is that there is a positive linear
    relationship with a Pearson's correlation of 0.67 between Alcohol Content by Volume (ABV) and
    International Bitterness Units (IBU) in US beers.

    The data we will analyze are 2 datasets: 
    1. Beer and 
    2. Breweries
    
    The datasets descriptions are as follows.
    
    The first data set, Beers, contains a list of 2410 US craft beers
    The source data file is CSV formatted file, beers.csv
    Name: Name of the beer.
    Beer ID: Unique identifier of the beer.
    ABV: Alcohol by volume of the beer.
    IBU: International Bitterness Units of the beer.
    Brewery ID: Brewery id associated with the beer.
    Style: Style of the beer.
    Ounces: Ounces of beer

    The second data set, Breweries, contains 558 US breweries.
    The source data file is a CSV formatted file, breweries.csv. 
    Brew ID: Unique identifier of the brewery.
    Name: Name of the brewery.
    City: City where the brewery is located.
    State: State where the brewery is located.
    
    The data sets will be merged,
    The Key Questions we will address and answer include:
    1. How many breweries are present in each state?
    2. Merge beer data with breweries data by brewery id. Print first 6 observations and the
       last six observations to check the merged file.
    3. Report the number of NA's in each column.
    4. Compute the median alcohol content and international bitterness unit for each state. Plot
       a bar chart to compare.
    5. Which state has the maximum alcoholic beer? Which state has the most bitter beer?
    6. Summary statistics for ABV (Alcohol by volume) variable.
    7. Is there a relationship between the bitterness of the beer and its alcoholic content? 
       Draw a scatter plot. ", file="README.md")
    
    cat("CONCLUSION
    There is a correlation between International Bitterness Units (IBU) and Alcohol by Volume (ABV)
    The Pearson's R Correlation was run on the full data set and the clean data set.
    The correlation result is 0.67, a moderate linear relationship.
    The 95% confidence interval is .64 to .69.", file="README.md", append=T)
```
    ## Preparing the Data
      The files have been stored on the github site as.csv files.  The RAW URLs are provided the
      datasets will be loaded into R.

```r
breweryURL<- 'https://raw.githubusercontent.com/sanjaystone/MSDS6306ProjectUSBeer/master/Analysis/Data/Breweries.csv'
beersURL <- 'https://raw.githubusercontent.com/sanjaystone/MSDS6306ProjectUSBeer/master/Analysis/Data/Beers.csv'
breweries <- read.csv(breweryURL, header=T)
beers <- read.csv(beersURL, header=T)
```

## Viewing the Data
We will load and run summary statistics on the dataset to ensure it was imported propery.
Using Dim, we can see the Breweries data set, which contains 558 rows or US breweries.
The dataset contains 4 columns: Brewery ID, Brewery Name, City, and State.
We can also summarize the data set.

```r
getwd()
```

```
## [1] "C:/RDATA/MSDS6306ProjectUSBeer"
```

```r
dim(breweries)
```

```
## [1] 558   4
```

```r
head(breweries)
```

```
##   Brew_ID                      Name          City State
## 1       1        NorthGate Brewing    Minneapolis    MN
## 2       2 Against the Grain Brewery    Louisville    KY
## 3       3  Jack's Abby Craft Lagers    Framingham    MA
## 4       4 Mike Hess Brewing Company     San Diego    CA
## 5       5   Fort Point Beer Company San Francisco    CA
## 6       6     COAST Brewing Company    Charleston    SC
```

```r
tail(breweries)
```

```
##     Brew_ID                          Name          City State
## 553     553         Mickey Finn's Brewery  Libertyville    IL
## 554     554           Covington Brewhouse     Covington    LA
## 555     555               Dave's Brewfarm        Wilson    WI
## 556     556         Ukiah Brewing Company         Ukiah    CA
## 557     557       Butternuts Beer and Ale Garrattsville    NY
## 558     558 Sleeping Lady Brewing Company     Anchorage    AK
```

```r
names(breweries)
```

```
## [1] "Brew_ID" "Name"    "City"    "State"
```

```r
str(breweries)
```

```
## 'data.frame':	558 obs. of  4 variables:
##  $ Brew_ID: int  1 2 3 4 5 6 7 8 9 10 ...
##  $ Name   : Factor w/ 551 levels "10 Barrel Brewing Company",..: 355 12 266 319 201 136 227 477 59 491 ...
##  $ City   : Factor w/ 384 levels "Abingdon","Abita Springs",..: 228 200 122 299 300 62 91 48 152 136 ...
##  $ State  : Factor w/ 51 levels " AK"," AL"," AR",..: 24 18 20 5 5 41 6 23 23 23 ...
```

```r
summary(breweries)
```

```
##     Brew_ID                           Name           City    
##  Min.   :  1.0   Blackrocks Brewery     :  2   Portland: 17  
##  1st Qu.:140.2   Blue Mountain Brewery  :  2   Boulder :  9  
##  Median :279.5   Lucette Brewing Company:  2   Chicago :  9  
##  Mean   :279.5   Oskar Blues Brewery    :  2   Seattle :  9  
##  3rd Qu.:418.8   Otter Creek Brewing    :  2   Austin  :  8  
##  Max.   :558.0   Sly Fox Brewing Company:  2   Denver  :  8  
##                  (Other)                :546   (Other) :498  
##      State    
##   CO    : 47  
##   CA    : 39  
##   MI    : 32  
##   OR    : 29  
##   TX    : 28  
##   PA    : 25  
##  (Other):358
```
We will load and run summary statistics on the dataset to ensure it was imported properly.
Using Dim, we can see the the Breweries data set, which contains a list of 2410 US craft beers.
The dataset contains 7 columns: Name, Beer_ID, ABV, IBU, Brewery ID, Style, and Ounces.

```r
dim(beers)
```

```
## [1] 2410    7
```

```r
head(beers)
```

```
##                  Name Beer_ID   ABV IBU Brewery_id
## 1            Pub Beer    1436 0.050  NA        409
## 2         Devil's Cup    2265 0.066  NA        178
## 3 Rise of the Phoenix    2264 0.071  NA        178
## 4            Sinister    2263 0.090  NA        178
## 5       Sex and Candy    2262 0.075  NA        178
## 6        Black Exodus    2261 0.077  NA        178
##                            Style Ounces
## 1            American Pale Lager     12
## 2        American Pale Ale (APA)     12
## 3                   American IPA     12
## 4 American Double / Imperial IPA     12
## 5                   American IPA     12
## 6                  Oatmeal Stout     12
```

```r
tail(beers)
```

```
##                             Name Beer_ID   ABV IBU Brewery_id
## 2405 Rocky Mountain Oyster Stout    1035 0.075  NA        425
## 2406                   Belgorado     928 0.067  45        425
## 2407               Rail Yard Ale     807 0.052  NA        425
## 2408             B3K Black Lager     620 0.055  NA        425
## 2409         Silverback Pale Ale     145 0.055  40        425
## 2410        Rail Yard Ale (2009)      84 0.052  NA        425
##                         Style Ounces
## 2405           American Stout     12
## 2406              Belgian IPA     12
## 2407 American Amber / Red Ale     12
## 2408              Schwarzbier     12
## 2409  American Pale Ale (APA)     12
## 2410 American Amber / Red Ale     12
```

```r
names(beers)
```

```
## [1] "Name"       "Beer_ID"    "ABV"        "IBU"        "Brewery_id"
## [6] "Style"      "Ounces"
```

```r
summary(beers)
```

```
##                      Name         Beer_ID            ABV         
##  Nonstop Hef Hop       :  12   Min.   :   1.0   Min.   :0.00100  
##  Dale's Pale Ale       :   6   1st Qu.: 808.2   1st Qu.:0.05000  
##  Oktoberfest           :   6   Median :1453.5   Median :0.05600  
##  Longboard Island Lager:   4   Mean   :1431.1   Mean   :0.05977  
##  1327 Pod's ESB        :   3   3rd Qu.:2075.8   3rd Qu.:0.06700  
##  Boston Lager          :   3   Max.   :2692.0   Max.   :0.12800  
##  (Other)               :2376                    NA's   :62       
##       IBU           Brewery_id                               Style     
##  Min.   :  4.00   Min.   :  1.0   American IPA                  : 424  
##  1st Qu.: 21.00   1st Qu.: 94.0   American Pale Ale (APA)       : 245  
##  Median : 35.00   Median :206.0   American Amber / Red Ale      : 133  
##  Mean   : 42.71   Mean   :232.7   American Blonde Ale           : 108  
##  3rd Qu.: 64.00   3rd Qu.:367.0   American Double / Imperial IPA: 105  
##  Max.   :138.00   Max.   :558.0   American Pale Wheat Ale       :  97  
##  NA's   :1005                     (Other)                       :1298  
##      Ounces     
##  Min.   : 8.40  
##  1st Qu.:12.00  
##  Median :12.00  
##  Mean   :13.59  
##  3rd Qu.:16.00  
##  Max.   :32.00  
## 
```

## 1. How many breweries are present in each state?
To answer the question, we ordered the data set by State.  We created a vector to summarize the State column. We summarized the counts (Min, Max, etc.).   The max is 47 (Colorado) and min is 1 (North Dakota), while the median is 7 breweries. We printed out the results by state.


```r
BrewerybyState <- breweries[order(breweries$`State`),]
View(BrewerybyState)
StateCount <-summary(BrewerybyState$State)
summary(StateCount)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    1.00    3.50    7.00   10.94   16.00   47.00
```

```r
StateCount
```

```
##  AK  AL  AR  AZ  CA  CO  CT  DC  DE  FL  GA  HI  IA  ID  IL  IN  KS  KY 
##   7   3   2  11  39  47   8   1   2  15   7   4   5   5  18  22   3   4 
##  LA  MA  MD  ME  MI  MN  MO  MS  MT  NC  ND  NE  NH  NJ  NM  NV  NY  OH 
##   5  23   7   9  32  12   9   2   9  19   1   5   3   3   4   2  16  15 
##  OK  OR  PA  RI  SC  SD  TN  TX  UT  VA  VT  WA  WI  WV  WY 
##   6  29  25   5   4   1   3  28   4  16  10  23  20   1   4
```

## 2. Merge beer data with breweries data by brewery id.Print first 6 observations and the last six
Prior to merging the files, we cleaned up the names of the columns to be a bit more clear and human readable We also double-checked to make sure Brewery ID is consistent across both data sets.


```r
names (beers) [1] <- "Beer Name"
names (beers) [5] <- "Brewery ID"
names (breweries) [1] <- "Brewery ID"
names (breweries) [2] <- "Brewery Name"
BeerBreweryData <- merge(x=beers, y=breweries, by="Brewery ID", all=TRUE) 
View(BeerBreweryData )
head(BeerBreweryData)
```

```
##   Brewery ID     Beer Name Beer_ID   ABV IBU
## 1          1  Get Together    2692 0.045  50
## 2          1 Maggie's Leap    2691 0.049  26
## 3          1    Wall's End    2690 0.048  19
## 4          1       Pumpion    2689 0.060  38
## 5          1    Stronghold    2688 0.060  25
## 6          1   Parapet ESB    2687 0.056  47
##                                 Style Ounces       Brewery Name
## 1                        American IPA     16 NorthGate Brewing 
## 2                  Milk / Sweet Stout     16 NorthGate Brewing 
## 3                   English Brown Ale     16 NorthGate Brewing 
## 4                         Pumpkin Ale     16 NorthGate Brewing 
## 5                     American Porter     16 NorthGate Brewing 
## 6 Extra Special / Strong Bitter (ESB)     16 NorthGate Brewing 
##          City State
## 1 Minneapolis    MN
## 2 Minneapolis    MN
## 3 Minneapolis    MN
## 4 Minneapolis    MN
## 5 Minneapolis    MN
## 6 Minneapolis    MN
```

```r
tail(BeerBreweryData)
```

```
##      Brewery ID                 Beer Name Beer_ID   ABV IBU
## 2405        556             Pilsner Ukiah      98 0.055  NA
## 2406        557  Heinnieweisse Weissebier      52 0.049  NA
## 2407        557           Snapperhead IPA      51 0.068  NA
## 2408        557         Moo Thunder Stout      50 0.049  NA
## 2409        557         Porkslap Pale Ale      49 0.043  NA
## 2410        558 Urban Wilderness Pale Ale      30 0.049  NA
##                        Style Ounces                  Brewery Name
## 2405         German Pilsener     12         Ukiah Brewing Company
## 2406              Hefeweizen     12       Butternuts Beer and Ale
## 2407            American IPA     12       Butternuts Beer and Ale
## 2408      Milk / Sweet Stout     12       Butternuts Beer and Ale
## 2409 American Pale Ale (APA)     12       Butternuts Beer and Ale
## 2410        English Pale Ale     12 Sleeping Lady Brewing Company
##               City State
## 2405         Ukiah    CA
## 2406 Garrattsville    NY
## 2407 Garrattsville    NY
## 2408 Garrattsville    NY
## 2409 Garrattsville    NY
## 2410     Anchorage    AK
```

# 3. Report the number of NA's in each column.
We calculated the number of NA's by each column or by column sums as a double-check.
ABV has 62 & IBU has 1005 NA's. From the visual check, we know Style has a couple of blanks(""s). We replaced the blanks(""s) with NA. Now Style has 5 NA's.


```r
IBU <- (is.na(BeerBreweryData$IBU))
summary(IBU)
```

```
##    Mode   FALSE    TRUE 
## logical    1405    1005
```

```r
any(is.na(BeerBreweryData$ABV))
```

```
## [1] TRUE
```

```r
sum(is.na(BeerBreweryData$IBU))
```

```
## [1] 1005
```

```r
sum(is.na(BeerBreweryData$'Brewery ID'))
```

```
## [1] 0
```

```r
sum(is.na(BeerBreweryData$'Beer Name'))
```

```
## [1] 0
```

```r
sum(is.na(BeerBreweryData$ABV))
```

```
## [1] 62
```

```r
sum(is.na(BeerBreweryData$IBU))
```

```
## [1] 1005
```

```r
sum(is.na(BeerBreweryData$Style))
```

```
## [1] 0
```

```r
sum(is.na(BeerBreweryData$Ounces))
```

```
## [1] 0
```

```r
sum(is.na(BeerBreweryData$'Brewery Name'))
```

```
## [1] 0
```

```r
sum(is.na(BeerBreweryData$City))
```

```
## [1] 0
```

```r
sum(is.na(BeerBreweryData$State)) 
```

```
## [1] 0
```

```r
colSums(is.na(BeerBreweryData))
```

```
##   Brewery ID    Beer Name      Beer_ID          ABV          IBU 
##            0            0            0           62         1005 
##        Style       Ounces Brewery Name         City        State 
##            0            0            0            0            0
```

```r
BeerBreweryData[BeerBreweryData==""] <- NA
colSums(is.na(BeerBreweryData))
```

```
##   Brewery ID    Beer Name      Beer_ID          ABV          IBU 
##            0            0            0           62         1005 
##        Style       Ounces Brewery Name         City        State 
##            5            0            0            0            0
```


## 4. Compute the median alcohol content and international bitterness unit for each state.
From a visual perspective, we ordered the data using the arrange from the plyr package.
We created a clean data set that removed all the NA's from the data set since this would affect
the median calculation and the plotting of the values. Next, the median for ABV by State was calculated using the aggregate function.

##    Plot a bar chart to compare.
The bar chart was created using the ggplot from the ggplot2 package. From the ABV chart, Maine and West Virginia have the highest median Alcohol by Volume. Utah has the lowest median Alcohol by Volume (ABV) which should not be too surprising. From the IBU chart, it seems that Maine and West Virginia have the highest median values for International Bitterness Units (IBU). Wisconsin has the lowest median value for International Bitterness Units (IBU)


```r
library(plyr)
library(ggplot2)
ABVbyState<-arrange(BeerBreweryData, State, ABV)
CleanABVbyState<-na.omit(ABVbyState)
View(CleanABVbyState)
any(is.na(CleanABVbyState))
```

```
## [1] FALSE
```

```r
MedianABVbyState <- aggregate(ABV~State, data=CleanABVbyState, FUN=median)
MedianABVbyState
```

```
##    State    ABV
## 1     AK 0.0570
## 2     AL 0.0600
## 3     AR 0.0400
## 4     AZ 0.0550
## 5     CA 0.0580
## 6     CO 0.0650
## 7     CT 0.0610
## 8     DC 0.0590
## 9     DE 0.0550
## 10    FL 0.0620
## 11    GA 0.0620
## 12    HI 0.0520
## 13    IA 0.0560
## 14    ID 0.0580
## 15    IL 0.0570
## 16    IN 0.0570
## 17    KS 0.0500
## 18    KY 0.0575
## 19    LA 0.0510
## 20    MA 0.0540
## 21    MD 0.0565
## 22    ME 0.0670
## 23    MI 0.0560
## 24    MN 0.0555
## 25    MO 0.0500
## 26    MS 0.0580
## 27    MT 0.0570
## 28    NC 0.0610
## 29    ND 0.0500
## 30    NE 0.0560
## 31    NH 0.0465
## 32    NJ 0.0460
## 33    NM 0.0610
## 34    NV 0.0550
## 35    NY 0.0595
## 36    OH 0.0575
## 37    OK 0.0630
## 38    OR 0.0560
## 39    PA 0.0570
## 40    RI 0.0525
## 41    SC 0.0500
## 42    TN 0.0550
## 43    TX 0.0550
## 44    UT 0.0400
## 45    VA 0.0570
## 46    VT 0.0550
## 47    WA 0.0560
## 48    WI 0.0510
## 49    WV 0.0620
## 50    WY 0.0510
```

```r
ggplot(data=MedianABVbyState, aes(x = State, y = ABV))+ geom_bar(stat='identity', fill="blue")
```

![](MSDS6306ProjectUSBeerAnalysis_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

```r
MedianIBUbyState <- aggregate(IBU~State, data=CleanABVbyState, FUN=median)
MedianIBUbyState
```

```
##    State  IBU
## 1     AK 46.0
## 2     AL 43.0
## 3     AR 39.0
## 4     AZ 20.0
## 5     CA 42.0
## 6     CO 40.0
## 7     CT 29.0
## 8     DC 47.5
## 9     DE 52.0
## 10    FL 55.0
## 11    GA 55.0
## 12    HI 22.5
## 13    IA 26.0
## 14    ID 39.0
## 15    IL 30.0
## 16    IN 33.0
## 17    KS 20.0
## 18    KY 31.5
## 19    LA 31.5
## 20    MA 35.0
## 21    MD 29.0
## 22    ME 61.0
## 23    MI 35.0
## 24    MN 44.5
## 25    MO 24.0
## 26    MS 45.0
## 27    MT 40.0
## 28    NC 33.5
## 29    ND 32.0
## 30    NE 35.0
## 31    NH 48.5
## 32    NJ 34.5
## 33    NM 51.0
## 34    NV 41.0
## 35    NY 47.0
## 36    OH 40.0
## 37    OK 35.0
## 38    OR 40.0
## 39    PA 30.0
## 40    RI 24.0
## 41    SC 30.0
## 42    TN 37.0
## 43    TX 34.0
## 44    UT 34.0
## 45    VA 42.0
## 46    VT 30.0
## 47    WA 38.0
## 48    WI 19.0
## 49    WV 57.5
## 50    WY 21.0
```

```r
ggplot(data=MedianIBUbyState, aes(x = State, y = IBU))+ geom_bar(stat='identity', fill="red")
```

![](MSDS6306ProjectUSBeerAnalysis_files/figure-html/unnamed-chunk-10-2.png)<!-- -->

## 5. Which state has the maximum alcoholic beer? Which state has the most bitter beer?
Colorado is the state with the highest Alcohol by Volume (ABV) of 0.128, although it was not on
of the top 2 states with the highest median Alcohol by Volume (ABV.

Oregon is the state with the highest International Bitterness Units (IBU) of 138, although it was not on one of the top 2 states with the highest International Bitterness Units (IBU)


```r
ABVbyState[which.max(ABVbyState$ABV),]$ABV
```

```
## [1] 0.128
```

```r
ABVbyState[which.max(ABVbyState$ABV),]$State
```

```
## [1]  CO
## 51 Levels:  AK  AL  AR  AZ  CA  CO  CT  DC  DE  FL  GA  HI  IA  ID ...  WY
```

```r
ABVbyState[which.max(ABVbyState$IBU),]$IBU
```

```
## [1] 138
```

```r
ABVbyState[which.max(ABVbyState$IBU),]$State
```

```
## [1]  OR
## 51 Levels:  AK  AL  AR  AZ  CA  CO  CT  DC  DE  FL  GA  HI  IA  ID ...  WY
```
##   6. Summary statistics for ABV (Alcohol by Volume) variable.
The summary for ABV (Alcohol by Volume) generates a report that indicates the Max is 0.128 and the Min is 0.001.  The median value of 0.0556 and mean of 0.05977. If we run the clean data w/o the N/As the values change to a median value of 0.05700 and a mean of 0.05992.  This shows the importance of cleaning the data.


```r
summary(ABVbyState$ABV)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
## 0.00100 0.05000 0.05600 0.05977 0.06700 0.12800      62
```

```r
summary(CleanABVbyState$ABV)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 0.02700 0.05000 0.05700 0.05992 0.06800 0.12500
```
## 7. Is there a relationship between the bitterness of the beer and its alcoholic content? Draw a          scatter plot.
The ggplot function was used to create the scatterplot to create a visual representation of the correlation between the two variables, or the relationship between International Bitterness Units (IBU) and Alcohol by Volume (ABV). The x-axis is Alcohol by Volume (ABV), the y-axis is International Bitterness Units (IBU), and a regression line was added to the plot. Based on the plot, there seems to be a linear relationship between the variables.


```r
ggplot(data=ABVbyState, aes(x = ABV, y = IBU))+ geom_point(shape=1, alpha=3/4, col="blue")+geom_smooth(method=lm, col="red")
```

```
## Warning: Removed 1005 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 1005 rows containing missing values (geom_point).
```

![](MSDS6306ProjectUSBeerAnalysis_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

```r
ggplot(data=CleanABVbyState, aes(x = ABV, y = IBU))+ geom_point(shape=1, col="blue")+geom_smooth(method=lm, col="red")
```

![](MSDS6306ProjectUSBeerAnalysis_files/figure-html/unnamed-chunk-13-2.png)<!-- -->
## Correlation Discussion

The Pearson's Correlation was run on the full data set and the clean data set to assess the correlation between International Bitterness Units (IBU) and Alcohol by Volume (ABV). Pearson's correlation is a measure of the linear correlation between two variables X and Y. It has a value between +1 and −1, where 1 is total positive linear correlation, 0 is no linear correlation, and −1 is total negative linear correlation.  The correlation result is 0.67, a moderate linear relationship. The 95% confidence interval is .64 to .69.


```r
correlation <- cor.test(ABVbyState$ABV, ABVbyState$IBU, method="pearson")
correlation
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  ABVbyState$ABV and ABVbyState$IBU
## t = 33.863, df = 1403, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.6407982 0.6984238
## sample estimates:
##       cor 
## 0.6706215
```

```r
correlation2 <- cor.test(CleanABVbyState$ABV, CleanABVbyState$IBU, method="pearson")
correlation2
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  CleanABVbyState$ABV and CleanABVbyState$IBU
## t = 33.848, df = 1401, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.6408842 0.6985369
## sample estimates:
##       cor 
## 0.6707224
```
# Conclusion
The is a correlation between International Bitterness Units (IBU) and Alcohol by Volume (ABV). The Pearson's R Correlation was run on the full data set and the clean data set. The correlation result is 0.67, indicating a moderate linear relationship. The 95% confidence interval is .64 to .69.




