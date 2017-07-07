The of this project purpose is conduct an analysis of US Beer and Brewery data.
    
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
       Draw a scatter plot. CONCLUSION
    There is a correlation between International Bitterness Units (IBU) and Alcohol by Volume (ABV)
    The Pearson's R Correlation was run on the full data set and the clean data set.
    The correlation result is 0.67, a moderate linear relationship.
    The 95% confidence interval is .64 to .69.