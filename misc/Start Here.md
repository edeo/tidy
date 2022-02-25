
Start Here!
========================================================
author: 
date: 
autosize: False



Welcome !
========================================================

These slides are to help you as you work through
the practice.Rmd file.

Additional instructions and links to videos
showing you how to work through the different 
exercises are included.








Mutate
========================================================

Frequently you'll want to create new columns based on the values in existing
columns, for example to do unit conversions, or to find the ratio of values in
two columns. For this we'll use `mutate()`.

We might be interested in the ratio of number of household members
to rooms used for sleeping (i.e. avg number of people per room):


library(tidyverse)

interviews %>%
    mutate(people_per_room = no_membrs / rooms)


Mutate 2
========================================================

We may be interested in investigating whether being a member of an
irrigation association had any effect on the ratio of household members
to rooms. To look at this relationship, we will first remove
data from our dataset where the respondent didn't answer the
question of whether they were a member of an irrigation association.
These cases are recorded as "NULL" in the dataset.

To remove these cases, we could insert a `filter()` in the chain:


interviews %>%   
    filter(!is.na(memb_assoc)) %>%  
    mutate(people_per_room = no_membrs / rooms) 

Mutate 3
========================================================
interviews %>%   
    filter(!is.na(memb_assoc)) %>%  
    mutate(people_per_room = no_membrs / rooms) 

The `!` symbol negates the result of the `is.na()` function. Thus, if `is.na()`
returns a value of `TRUE` (because the `memb_assoc` is missing), the `!` symbol
negates this and says we only want values of `FALSE`, where `memb_assoc` **is
not** missing.


Mutate Exercise
========================================================

> Create a new dataframe from the `interviews` data that meets the following
> criteria: 
> * contains only the `village` column and a new column called
>  `total_meals` containing a value that is equal to the total number of meals
>  served in the household per day on average (`no_membrs` times `no_meals`).
> * Only the rows where `total_meals` is greater than 20 should be shown in the
>  final dataframe.
>
>  **Hint**: think about how the commands should be ordered to produce this data
>  frame!  
>  Solution is on the next page

Mutate Exercise Solution
========================================================

> ## Solution
>
>  
>  interviews_total_meals <- interviews %>%
>      mutate(total_meals = no_membrs * no_meals) %>%
>      filter(total_meals > 20) %>%
>      select(village, total_meals)
> 

Split-apply-combine
========================================================
### Split-apply-combine data analysis and the summarize() function

Many data analysis tasks can be approached using the *split-apply-combine*
paradigm: split the data into groups, apply some analysis to each group, and
then combine the results. **`dplyr`** makes this very easy through the use of
the `group_by()` function.

The `summarize()` function
========================================================
`group_by()` is often used together with `summarize()`, which collapses each
group into a single-row summary of that group.  `group_by()` takes as arguments
the column names that contain the **categorical** variables for which you want
to calculate the summary statistics. So to compute the average household size by
village:

The `summarize()`  Exercise
========================================================
> ## Exercise
>
> How many households in the survey have an average of
> two meals per day? Three meals per day? Are there any other numbers
> of meals represented?


Solution is on the next slide

Solution
=========================================================

interviews %>%
    count(no_meals)
    
    
    
