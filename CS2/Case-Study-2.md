---
title: "Case Study 2"
author: "Milca Arellano"
date: "January 18, 2020"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---





## Background

I learned to use new commands, such as group_by(), theme_bw(), etc. I also learned to use geom_line() and geom_point().

## Images


```r
gapminder1 <- filter(gapminder, gdpPercap <= 50000)
gapminder2 <- filter(gapminder1, country !="Kuwait")
gapminder3 <- gapminder2 %>% 
  group_by(continent, year) %>% 
  summarize(Population = mean(pop / 3000), weighted_gdp = weighted.mean(gdpPercap, pop))
ggplot(data=gapminder2, mapping = aes(x=lifeExp, y = gdpPercap, color = continent, size = pop / 100000 )) + geom_point() + facet_grid(~year) + scale_y_continuous(trans = "sqrt") + theme_bw()+ labs(x="Life Expectancy", y = "GDP per capita", size = "Population(100k)", color = "Continent")
```

![](Case-Study-2_files/figure-html/unnamed-chunk-2-1.png)<!-- -->


```r
ggplot() +
  geom_point(data=gapminder2, mapping = aes(x=year, y = gdpPercap, color = continent)) +
  geom_line(data = gapminder2, aes(x = year, y = gdpPercap, color = continent, group = country)) + 
  geom_point(data = gapminder3, aes(x = year, y = weighted_gdp, size = Population)) +
  geom_line(data = gapminder3, aes(x = year, y = weighted_gdp)) +
  facet_grid(~continent) + labs(x="Year", y ="GDP per capita",  size = "Population(100k)", color = "Continent") + theme_bw()
```

![](Case-Study-2_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

