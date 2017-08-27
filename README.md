# Obamacare
Can Obamacare enrollment measure the likelihood that a county flipped from Obama 2012 to Trump 2016?

This paper (see PDF download) explored this question by developing a spatial regression model based on multiple factors:

-Enrollment volume by county in the Affordable Care Act (Obamacare) in March 2016
-Median age
-Percentage of the population with a high school education or less
-Total population
-Net migration
-Percent of the population that is caucasian
-Unemployment rate*

*Due to problems with the dataset, unemployment didn't make it into the final mode.

The project utilized linear regression as well as multiple tests of spatial autocorrelation, including:

-Contiguous neighbors for counties, "Queen" configuration
-Row standardized weight matrices
-Spatial lag test
-Spatial error test
-Breusch-Pagan test

The final result was that the model overutilized spatial autocorrelation and its predictions are therefore unreliable.

Data sources are available in the Citations section of the PDF.
