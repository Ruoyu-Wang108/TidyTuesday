# TidyTuesday 2020-08-17

I made a waffle bar plot for the first time!!

Find more codes on [hrbrmstr/waffle](https://github.com/hrbrmstr/waffle)

### **Disadvantages: **

1. When the counts are large, the square will become extremely small

2. not suitable to work with elements > 5, especially when the quantity are close. When there are a lot of elements in one waffle bar, the color becomes burr and hard to identify or differeniate.

3. It took forever to make a plot

### Important codes:

```
library(dplyr)
library(waffle)

storms %>% 
  filter(year >= 2010) %>% 
  count(year, status) -> storms_df

ggplot(storms_df, aes(fill = status, values = n)) +
  geom_waffle(color = "white", size = .25, n_rows = 10, flip = TRUE) +
  facet_wrap(~year, nrow = 1, strip.position = "bottom") +
  scale_x_discrete() + 
  scale_y_continuous(labels = function(x) x * 10, # make this multiplyer the same as n_rows
                     expand = c(0,0)) +
  ggthemes::scale_fill_tableau(name=NULL) +
  coord_equal() +
  labs(
    title = "Faceted Waffle Bar Chart",
    subtitle = "{dplyr} storms data",
    x = "Year",
    y = "Count"
  ) +
  theme_minimal(base_family = "Roboto Condensed") +
  theme(panel.grid = element_blank(), axis.ticks.y = element_line()) +
  guides(fill = guide_legend(reverse = TRUE))
```
