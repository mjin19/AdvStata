# Background
We are developing skills that allow us to access publicly available large databases that may be queried to answer fundamental questions about the publics health. These datasets might exist in formats unfamiliar to Stata users or in sizes that cripple ones workflow.

In our first two weeks, we curated a dataset with all the mortality records in the United States from 1959-2017 and wrote a basic Stata script that output a two-way plot showing annual trends in number of deaths during this period. In the subsequent two weeks we wrote a Stata program, mortality, that allows the user to define the time-period of interest, plus other parameters such as cause-of-death, and ultimately produce a similar two-way plot with the convenience of a Stata command.

Our goal for the second-half of the class is to leverage this experience to give Stata users access to the entire range of NHANES surveys via a simple command, nhanes, with several user-defined options. We have not yet articulated what these options are but will do so on an emerging basis each week.

Today let’s start by reading in the alpha-version of this program, which we adopted from Chapter: r(mean) of the PH.340.600 book. Depending on your Stata edition, this program will either import a dataset with 20,000 observations and 3600 variables or 20,000 observations and 22 variables:  

```
qui do https://raw.githubusercontent.com/jhustata/book/main/nhanes-alpha.ado      
```
