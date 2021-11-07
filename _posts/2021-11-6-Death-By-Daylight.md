---
layout: post
title: Death By Daylight
---
## Background
This project is inspired by [a recent NY Times podcast](https://www.nytimes.com/2021/11/05/learning/do-you-think-it-is-time-to-get-rid-of-daylight-saving-time.html) featuring a debate over the merits of daylight saving time vs. standard time. Both sides advocated for doing away with the current US system of changing twice a year and settling upon a single time system for the entire year. But they had arrived at opposite conclusions about which time system was best. 

What piqued my curiosity was a research finding cited by the neurologist arguing in favor of adopting standard time year round. He cited a study comparing cancer rates on the western edge of US time zones vs. the eastern edge. Cancer rates were found to be higher on the western edge, where the sun sets later. He proposed the underlying mechanism to be the "social jetlag" induced by people going to sleep later in areas where the sun sets later, but still having to wake up to meet the obligatory schedules of society whose timing is fixed (e.g., school and work start times), such that they are more chronically sleep deprived than their counterparts in areas where the sun sets earlier. Sleep deprivation has long been associated with negative health outcomes, ergo higher cancer rates for the sleepier cohort. 

The implication of this comparison across time zone boundaries is that year-round daylight saving time would be even worse for human health because it causes people nationwide to go to bed later.

I googled to learn more, and found a [2019 Washington Post article](https://www.washingtonpost.com/business/2019/04/19/how-living-wrong-side-time-zone-can-be-hazardous-your-health/) on the subject. This article reprints a beautiful visualization of average annual sunset time from the [original 2019 journal article](https://www.sciencedirect.com/science/article/abs/pii/S0167629618309718) by researchers from Pittsburgh and Switzerland. 

![lights out]({{ site.baseurl }}/images/lightsout_900px.png)

## Project Plan
My goal is to reproduce this effect in data from other sources. No guarantee I'll actually see an effect but it will be a useful learning experience. This project will help me build toolsets for visualizing geospatial data in 2D maps. It will also give me practice with performing regression analysis. Also I'll get familiar with identifying and collating real-world sources of health outcome data.

To do list:
- Find a suitable dataset (publicly available, nationwide, related to health outcomes, with many geospatial subdivisions per time zone) 
- Vet the dataset (structural complexity? how much missing/quirky data? how much variability?)
- Gather demographics of the geospatial subdivisions (population, economic, education, etc.)
- Compute annual average sunset times for each geospatial subdivision
- Recreate the nifty map of average sunset times, and create versions of that map colorcoded by health outcome value.
- Run the regression of health outcomes as a function of average sunset times 


### Candidate Datasets
CDC's [Behavioral Risk Factor Surveillance System](https://chronicdata.cdc.gov/Behavioral-Risk-Factors/Behavioral-Risk-Factors-Selected-Metropolitan-Area/j32a-sa6u)
- 153k rows, 27 columns
- downloaded CSV on 11/6/21 from CDC website
- subdivisions are selected metropolitan statistical areas (MMSAs)
- years covered: 2011-2019
- tons of health outcome measures, unclear how complete the coverage is though (only questions/years/MMSAs where there were more than 500 responses per MMSA are included)
- includes a lat-lon column for the location! I wouldn't have to compute it...

IHME's [United States Mortality Rates by County](https://www.kaggle.com/IHME/us-countylevel-mortality)
- 67k rows, 30 columns
- downloaded CSV on 11/5/21 from Kaggle
- subdivisions are US counties (appears to be all, and state level stats are given as well)
- years covered: every 5 years 1980-2010 plus 2014
- simpler to interpret outcome measures: age-standardized mortality rate (death per 100k population) by category
- This website has kernel for using R to create maps!

### Code for Sunset Times
I found [some R code on Github](https://gist.github.com/jonspring/78b2124cf9daa351de98b5e031473585) by a guy who made some cool animations in R showing how sunrise & sunset times shift for different cities throughout the year, and also showing a US map rotating to show correlation between later sunsets and voting patterns. He [tweeted](https://twitter.com/JustTheSpring/status/1194355907745865728) about it too!

Also found a [Python library](https://pypi.org/project/suncalc/) to do sun calculations for given locations.

_To be continued..._
