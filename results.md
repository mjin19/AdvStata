# Results

When a Kaplan-Meier graph pops up on your screen, that will be your cue that the program has run to completion and that you have an NHANES III dataset in your `pwd`.


```
    qui do https://raw.githubusercontent.com/jhustata/book/main/nhanes-alpha.ado    
    set scheme s2color
    nhanes
```

<img src="https://raw.githubusercontent.com/mjin19/AdvStata/master/_build/html/_images/Graph.svg" alt="Graph Title" width="800" height="600">
  
```  
    use nh3andmort, clear
    di "obs: `c(N)' & vars: `c(k)'"      
```
