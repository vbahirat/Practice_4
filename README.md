# Practice_4
---
title: "Practice 4"
author: "Vaidehee Bahirat"
date: "4/13/2022"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

This is an individual assignment

```{r}
library(tidyverse)
```

```{r}
av <- read.csv("https://raw.githubusercontent.com/fivethirtyeight/data/master/avengers/avengers.csv", stringsAsFactors = FALSE)
head(av)
```
```{r}
av0 = av %>% filter(Name.Alias != "")
av0 = av0 %>% filter(Name.Alias != "Vance Astrovik")
```


```{r}
deaths = av0 %>% gather(key = time, value = death, c(11, 13, 15, 17, 19)) %>%
  select(Name.Alias, time, death) %>% 
  mutate(time = parse_number(time))

```

```{r}
returns = av0 %>% gather(key = time, value = return, c(12, 14, 16, 18, 20)) %>%
  select(Name.Alias, time, return) %>%
  mutate(time = parse_number(time))

```

```{r}
av.new = left_join(deaths, returns, by = c("Name.Alias", "time"))
```

**Part 2**
I am analyzing the following statement:
**"I counted 89 total deaths and on 57 occasions the individual made a comeback." **
```{r}
filter(av.new,death=="YES")
```

**The number of columns are 82 thus total number of deaths are 82. However as mentioned there are 88 which is not in allignmnent with what I found. **

```{r}
filter(av.new,death=="YES"&return=="YES")
```

**The total number of comebacks found after dying are 55 whihc is not similar to what is stated in the document. ** 
