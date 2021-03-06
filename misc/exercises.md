
Start Here!
========================================================
author: 
date: 
autosize: TRUE



Welcome !
========================================================

These slides are to help you as you work through
the dplyr.Rmd file.

Additional instructions and links to videos
showing you how to work through the different 
exercises are included.





Exercise 1 
========================================================
> 
>
>  Using pipes, subset the `interviews` data to include interviews
> where respondents were members of an irrigation association
> (`memb_assoc`) and retain only the columns `affect_conflicts`,
> `liv_count`, and `no_meals`.
>

Solution
========================================================


```r
interviews %>%
filter(memb_assoc == "yes") %>%
    select(affect_conflicts, liv_count, no_meals)
```

Exercise2
========================================================
>
>  Create a new dataframe from the `interviews` data that meets the following
>  criteria: contains only the `village` column and a new column called
>  `total_meals` containing a value that is equal to the total number of meals
>  served in the household per day on average (`no_membrs` times `no_meals`).
>  Only the rows where `total_meals` is greater than 20 should be shown in the
>  final dataframe.
>
>  **Hint**: think about how the commands should be ordered to produce this data
>  frame!
>


Solution
========================================================


```r
interviews_total_meals <- interviews %>%  
      mutate(total_meals = no_membrs * no_meals) %>% 
      filter(total_meals > 20) %>% select(village, total_meals) 
```



exercise 3
=========================================================


>
> How many households in the survey have an average of
> two meals per day? Three meals per day? Are there any other numbers
> of meals represented?
>

## Solution
=========================================================

> > interviews %>%
> >    count(no_meals)
>

exercise 4
=========================================================
> Use `group_by()` and `summarize()` to find the mean, min, and max
> number of household members for each village. Also add the number of
> observations (hint: see `?n`).

## Solution
=========================================================
> > interviews %>%
> >   group_by(village) %>%
> >   summarize(
> >       mean_no_membrs = mean(no_membrs),
> >       min_no_membrs = min(no_membrs),
> >       max_no_membrs = max(no_membrs),
> >       n = n()
> >   )
> > ```


exercise 6
==========================================================
>
> What was the largest household interviewed in each month?
>

solution exercise 6
==========================================================
 ## Solution

```r
> > # if not already included, add month, year, and day columns
> > library(lubridate) # load lubridate if not already loaded
> > interviews %>%
> >     mutate(month = month(interview_date),
> >            day = day(interview_date),
> >            year = year(interview_date)) %>%
> >     group_by(year, month) %>%
> >     summarize(max_no_membrs = max(no_membrs))
```


