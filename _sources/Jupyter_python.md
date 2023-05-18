# Jupyter-Python Version

## Increasing access to the NHANES 1988-2018 surveys & mortality linkage data via a user-friendly Stata program

*Mu Jin, Johns Hopkins Bloomberg School of Public Health*   
*Junming Gong, Johns Hopkins Bloomberg School of Public Health*   
*Xueer Zhang, Johns Hopkins Bloomberg School of Public Health*   
*Sohyeon Kwon, Johns Hopkins Bloomberg School of Public Health*   

**Background:**   

The National Health and Nutrition Examination Survey (NHANES) is a comprehensive initiative tasked with evaluating the health and nutritional conditions of both children and adults in the United States. This distinctive survey is conducted through a blend of in-depth interviews and physical examinations. It is a cornerstone program of the National Center for Health Statistics (NCHS), a component of the Centers for Disease Control and Prevention (CDC).  

For the 700 course, we curated a dataset with all the [mortality records](https://data.nber.org/mortality/) in the United States from 1959-2017 and wrote a basic Stata script that output a [two-way plot](https://jhustata.github.io/book/_downloads/9359d2ae4f8ad2efcfe2fd34e3547c35/mortality.png) showing annual trends in number of deaths during this period. For the final project, our group designed a program using NHANES data to conduct survival analysis for any of the variables in the dataset.

**Methods:** 

This program is based on Stata/BE 17.0. This current program outputs an NHANES dataset with 22 pre-specified variables. Kaplan-Meier graph is used to show the difference between survival probability by exposure group. Scaled Schoenfeld residuals is used to test the proportional hazards assumption, and Cox proportional hazards model is used to evaluate the effect of selected variable on survival.

**Results:** 

This project outputs a Kaplan-Meier graphs by input variable, results from proportional hazards assumption test, and output a univariate Cox model. To call the program, you would use: `survival_analysis variable name`. We also showed an example, the exposure is `hab1` (general health status) and the outcome is time to death.  

Here is how we developed the NHANES mortality dataset:
  
```stata
set scheme s2color
nhanes 
```  
![](Graph.svg)       
    
```stata
use nh3andmort, clear
di "obs: `c(N)' & vars: `c(k)'"
```
<u>obs</u>: 19599  
<u>vars</u>: 22   
  
Here is our survival analysis program and an example:  

```stata
use nh3andmort, clear  
stset permth_exm, failure(mortstat) 
```   

```stata
capture program drop survival_analysis
program define survival_analysis
  args varname
  
  sts graph, by(`varname') title(Kaplan-Meier Estimates)
  
  di "Cox proportional hazards model for `varname':"
  stcox `varname'
  
  di "Proportional hazards assumption test for `varname':"
  estat phtest
  
end

survival_analysis hab1  
```   
![](Graph1.svg)  

  
Cox proportional hazards model for hab1:

| Variable | Haz. ratio | Std. err. |    z    | P > z | 95% Conf. Interval |
|----------|------------|-----------|---------|-------|--------------------|
|   hab1   |  1.446283  | 0.0162612 | 32.82   | 0.000 | 1.41476 - 1.478508 |

Proportional hazards assumption test for hab1:  
  
|             |   chi2   | df | Prob>chi2 |
|-------------|----------|----|-----------|
| Global test |  86.25   |  1 |   0.0000  |

 


**Conclusions:** 

NHANES is a large database with participants surveyed and questionnaire, exam, and lab items captured. It is soon going to be fully accessible to Stata users, in no small part because of this humble capstone project.  

This program can easily run and show the results for a survival analysis between a variable in the dataset and time to death for NHANES participants from 1959-2017.  

**Acknowledgments:**
  
We initially published our Stata output in a Jupyter book hosted by Github. All the .html content of the book was produced in a Python environment; however, Stata .html output will gradually replace the Python-based output of the book as we truly become advanced Stata users!  

VS Code terminal is our IDE choice for committing and pushing our git content to our hub and have established a seamless process for updating our publication.  
  
We used the Stata program and abstract template originally created by Professor Muzaale and we appreciated his kind help during this course.

**References:**  

1. https://jhustata.github.io/book/jjj.html
2. https://jupyterbook.org/en/stable/start/your-first-book.html
3. https://www.stata.com/stata-news/news36-1/spotlight-markdown/
4. https://wwwn.cdc.gov/nchs/data/nhanes3/1a/adult.sas
5. https://jhustata.github.io/class700/intro.html
6. https://www.jhsph.edu/courses/course/37447/2022/340.700.71/advanced-stata-programming
7. [Muzaale AD. Databases for surgical health services research: National Health and Nutrition Examination Survey. Surgery. 2019 May;165(5):873-875](https://www.surgjournal.com/article/S0039-6060(18)30076-X/fulltext)
8. https://www.ssc.wisc.edu/~hemken/Stataworkshops/dyndoc%20review/Review.html
