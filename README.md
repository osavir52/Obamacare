# Did Obamacare enrollees as a group vote for Trump?
In December of 2016, Vox's Sarah Kliff traveled to Corbin, KY to interview voters who were enrolled in Obamacare but had voted for Donald Trump for President, including even an Obamacare enrollment counselor. This finding was intriguing - but it left one wondering whether it was a coincidence of Corbin, KY or a phenomenon observable nation-wide.

Thirty-eight U.S. states utilize the Affordable Care Act's marketplace exchanges, and enrollment data for these states can be found on the Health and Human Services website. Unfortunately, since Kentucky has its own progra modeled after Obamcare, it's not included in the data - but it's still interesting to look into what is available. Can enrollment in Obamacare be used to predict whether or not a given county flipped from voting for Barack Obama in 2012 to voting for Donald Trump in 2016?

To investigate this, I've utilized the HHS enrollment data for the ACA and county-level election results,, as well data on other identifying factors for "Trump" counties - the median age; percent of population with a high school education or lower; the net migration expressed as a positive (net immigration into) or negative (net emigraton from) percent of the population; the total population; and the percent of the population that was caucasian. Data on the unemployment rate was also obtained, but because it lacked identifying information such as FIPS code or State associated with county (becauase many states have the same county name), it unfortunately could not be used.

I used linear regression to model which counties flipped from Obama 2012 to Trump 2016, using the above factors. However, this being geographic data, there is always the possibility that the resulting model would overutilize spatial autocorrelation to generate accurate results. In order to account for spatial dependence, I measured the spatial relationships of individual counties based on contiguity — counties that share borders were considered to be neighbors, “shared borders” defined as borders that share at least a single point (“Queen” configuration). 

While some counties in the U.S. are virtual squares, in no state are counties arrayed in a perfect grid, and most counties are irregular polygons. Therefore, most counties that share a border share a significant border — in other words, there are few if any pairs of counties that are contiguous but share such a small border that their neighboring one another does not reflect any shared characteristics (an argument can be made that larger counties do in fact share borders without sharing characteristics; however, by the same token, since county lines are drawn politically or arbitrarily, a point on the border of a large county may just as well not share any characteristics with a point in its center or on an opposite border).

In constructing spatial weight matrices, I opted for row standardized weighting. Due to the irregular shape and lack of consistency in size across most counties, it is assumed there may be some counties that are overrepresented by binary weighting.

Moran’s I testing was utilized to test for the influence of spatial dependence upon the value of Trump’s percentage of the vote per county. As we will see, it was found that spatial dependence did impact the result, and spatial lag regression as well as spatial error regression were both used, with a Breusch-Pagan test was to determine whether or not the lag and error models still retained any spatial dependence within the final model. All regressions were performed with α = .05.

The results of the Moran's I test show the influence of spatial dependence on a any regression model that might be built:

![Moran's I table](/aca_table_moransI.jpg)

![Moran's I chart](/acamoransi.jpg)

The results show that spatial dependnece was significant Before moving forward, a linear model was constructed to test the significance of the individual variables, yielding the following results:

![Linear Regression Model](/aca_table_lm.jpg)

These results show that, among the chosen variables, the only one which was not significant was the volume of plan selections in the Affordable Care Act per county. In order to account for the impact of spatial dependnece, I used the spatial lag regression and spatial error regression tests, with results shown below.

Spatial Lag Regression

![Spatial Lag Regression Table](/aca_table_spatlag.jpg)

Spatial Error Regression

![Spatial Lag Error Table](/aca_table_spaterr.jpg)

The results show that, with both models, spatial dependnece was a significant influencing factor. The unequivocally lower AIC values show that removing spatial dependence significantly detracted from both models.

A final Breusch-Pagan test shows that, even then, the resulting model still retains significant influence from spatial dependence:

![Breusch-Pagan Test Table](/aca_table_bptest.jpg)

The BP Test results demosntrate that both models retain evidence of significant spatial dependence. Even removing the plan selections varaible from the model yields little change to the ultimate results. In other words, since spatial dependence cannot be fully separated from the results of hte model, there is no statistical evidnece based on this data that enrollment in the AFfordable Care Act is an effective predictor of Donald Trump's county-level electoral successes in the 2016 election (importanty, there is similarly no evidence to the _contrary_).

Citations and Data Sources:

R Core Team (2016). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria.
URL https://www.R-project.org/.

Kliff, Sarah. “Why Obamacare enrollees voted from Trump.” Vox.com
http://www.vox.com/science-and-health/2016/12/13/13848794/kentucky-obamacare-trump

Presidential election results for 2012 and 2016 from The Guardian and townhall.com. (Accessed February 20, 2017); Retrieved from:
https://github.com/tonmcg/County_Level_Election_Results_12-16

Plan Selections by ZIP Code and County in the health insurance marketplace: March 2016 (Accessed February 21, 2017) Retrieved from:
https://aspe.hhs.gov/basic-report/plan-selections-zip-code-and-county-health-insurance-marketplace-march-2016

U.S. Census Bureau, 2015 American Community Survey 5-Year estimates, B16010 (Accessed February 25, 2017) Retrieved from:
http://factfinder.census.gov

U.S. Census Bureau, 2015 American Community Survey 5-Year estimates, DP05 (Accessed February 25, 2017) Retrieved from:
http://factfinder.census.gov

U.S. Census Bureau, 2015 Population Estimates, PEPTCOMP (Accessed February 25, 2017) Retrieved from:
http://factfinder.census.gov
