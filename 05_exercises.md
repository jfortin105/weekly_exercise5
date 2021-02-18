---
title: 'Weekly Exercises #5'
author: "Josh Fortin"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.2     v purrr   0.3.4
## v tibble  3.0.4     v dplyr   1.0.2
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.0
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(openintro)     # for the abbr2state() function
```

```
## Loading required package: airports
```

```
## Loading required package: cherryblossom
```

```
## Loading required package: usdata
```

```r
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
```

```
## 
## Attaching package: 'maps'
```

```
## The following object is masked from 'package:purrr':
## 
##     map
```

```r
library(ggmap)         # for mapping points on maps
```

```
## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.
```

```
## Please cite ggmap if you use it! See citation("ggmap") for details.
```

```r
library(gplots)        # for col2hex() function
```

```
## 
## Attaching package: 'gplots'
```

```
## The following object is masked from 'package:stats':
## 
##     lowess
```

```r
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
```

```
## Linking to GEOS 3.8.0, GDAL 3.0.4, PROJ 6.3.1
```

```r
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggmap':
## 
##     wind
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
```

```
## 
## Attaching package: 'transformr'
```

```
## The following object is masked from 'package:sf':
## 
##     st_normalize
```

```r
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
library(directlabels)   # for geom_dl
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   year = col_double(),
##   month = col_double(),
##   service = col_character(),
##   departure_station = col_character(),
##   arrival_station = col_character(),
##   journey_time_avg = col_double(),
##   total_num_trips = col_double(),
##   avg_delay_all_departing = col_double(),
##   avg_delay_all_arriving = col_double(),
##   num_late_at_departure = col_double(),
##   num_arriving_late = col_double(),
##   delay_cause = col_character(),
##   delayed_number = col_double()
## )
```

```r
# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele.num = col_double(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = ""),
##   time_hr = col_double(),
##   dist_km = col_double(),
##   speed = col_double()
## )
```

```r
# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele = col_logical(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   date = col_date(format = ""),
##   state = col_character(),
##   fips = col_character(),
##   cases = col_double(),
##   deaths = col_double()
## )
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  

```r
home_owner <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-02-09/home_owner.csv')
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   year = col_double(),
##   race = col_character(),
##   home_owner_pct = col_double()
## )
```

```r
home_ownership_race <- home_owner %>% 
  mutate(home_owner = home_owner_pct * 100) %>% 
  ggplot(aes(x = year, y = home_owner, color = race)) +
  geom_line(aes(linetype = race, size = race)) +
  scale_linetype_manual(values = c("solid", "solid", "solid")) +
  scale_color_manual(values = c("peru", "steelblue4", "coral4")) + 
  scale_size_manual(values = c(1.25, 1.25, 1.25)) +
  geom_dl(aes(label = race), method = list(dl.trans(x = x + 0.2), "last.points", cex = 1.25)) +
  theme(plot.background = element_rect("snow2"), 
        panel.background = element_rect("snow2"),
        panel.border = element_rect(fill = NA, color = "gray80"),
        panel.grid.major = element_line("gray80"),
        panel.grid.minor = element_blank(),
        axis.line = element_line(size = 0.5, 
                                 linetype = "solid",
                                 colour = "gray80"),
        legend.position = "none") +
  xlim(1976, 2021)+
  labs(title = "US Homeownership by Race/Ethnicity",
       subtitle = "Percentages from 1976 - 2016",
       caption = "Josh Fortin | Data: US Census, Urban Institute",
       color = "",
       x = "",
       y = "")

ggplotly(home_ownership_race)
```

```
## Warning in geom2trace.default(dots[[1L]][[3L]], dots[[2L]][[1L]], dots[[3L]][[1L]]): geom_GeomDl() has yet to be implemented in plotly.
##   If you'd like to see this geom implemented,
##   Please open an issue with your example code at
##   https://github.com/ropensci/plotly/issues

## Warning in geom2trace.default(dots[[1L]][[3L]], dots[[2L]][[1L]], dots[[3L]][[1L]]): geom_GeomDl() has yet to be implemented in plotly.
##   If you'd like to see this geom implemented,
##   Please open an issue with your example code at
##   https://github.com/ropensci/plotly/issues

## Warning in geom2trace.default(dots[[1L]][[3L]], dots[[2L]][[1L]], dots[[3L]][[1L]]): geom_GeomDl() has yet to be implemented in plotly.
##   If you'd like to see this geom implemented,
##   Please open an issue with your example code at
##   https://github.com/ropensci/plotly/issues
```

<!--html_preserve--><div id="htmlwidget-7cec7ae11266d8c1587b" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-7cec7ae11266d8c1587b">{"x":{"data":[{"x":[1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016],"y":[44.238216050207,44.1229423868313,44.5405540930174,48.1899330523184,48.6023759608665,47.8128179043744,47.2045530632742,45.345446388515,45.5175400606323,44.1455696202532,44.513626620394,45.4041523886313,42.4406047516199,41.8236909383581,42.3898531375167,42.4140193046575,42.2539023730037,42.2341376228776,42.4696392163815,41.9390819390819,43.923296190723,45.5033446197044,45.9756293089626,45.4964623578981,47.1242898280022,47.6848337634735,48.171235448742,47.694021537319,49.0644948272067,49.1273806937505,47.2789601485502,48.1677581162045,47.1445261494055,46.4131551901336,45.9945689069925,44.3301670488045,43.2843483283065,42.8112399193548,42.753984063745,42.3,41.6],"text":["race: Black<br />race: Black<br />year: 1976<br />home_owner: 44.23822<br />race: Black","race: Black<br />race: Black<br />year: 1977<br />home_owner: 44.12294<br />race: Black","race: Black<br />race: Black<br />year: 1978<br />home_owner: 44.54055<br />race: Black","race: Black<br />race: Black<br />year: 1979<br />home_owner: 48.18993<br />race: Black","race: Black<br />race: Black<br />year: 1980<br />home_owner: 48.60238<br />race: Black","race: Black<br />race: Black<br />year: 1981<br />home_owner: 47.81282<br />race: Black","race: Black<br />race: Black<br />year: 1982<br />home_owner: 47.20455<br />race: Black","race: Black<br />race: Black<br />year: 1983<br />home_owner: 45.34545<br />race: Black","race: Black<br />race: Black<br />year: 1984<br />home_owner: 45.51754<br />race: Black","race: Black<br />race: Black<br />year: 1985<br />home_owner: 44.14557<br />race: Black","race: Black<br />race: Black<br />year: 1986<br />home_owner: 44.51363<br />race: Black","race: Black<br />race: Black<br />year: 1987<br />home_owner: 45.40415<br />race: Black","race: Black<br />race: Black<br />year: 1988<br />home_owner: 42.44060<br />race: Black","race: Black<br />race: Black<br />year: 1989<br />home_owner: 41.82369<br />race: Black","race: Black<br />race: Black<br />year: 1990<br />home_owner: 42.38985<br />race: Black","race: Black<br />race: Black<br />year: 1991<br />home_owner: 42.41402<br />race: Black","race: Black<br />race: Black<br />year: 1992<br />home_owner: 42.25390<br />race: Black","race: Black<br />race: Black<br />year: 1993<br />home_owner: 42.23414<br />race: Black","race: Black<br />race: Black<br />year: 1994<br />home_owner: 42.46964<br />race: Black","race: Black<br />race: Black<br />year: 1995<br />home_owner: 41.93908<br />race: Black","race: Black<br />race: Black<br />year: 1996<br />home_owner: 43.92330<br />race: Black","race: Black<br />race: Black<br />year: 1997<br />home_owner: 45.50334<br />race: Black","race: Black<br />race: Black<br />year: 1998<br />home_owner: 45.97563<br />race: Black","race: Black<br />race: Black<br />year: 1999<br />home_owner: 45.49646<br />race: Black","race: Black<br />race: Black<br />year: 2000<br />home_owner: 47.12429<br />race: Black","race: Black<br />race: Black<br />year: 2001<br />home_owner: 47.68483<br />race: Black","race: Black<br />race: Black<br />year: 2002<br />home_owner: 48.17124<br />race: Black","race: Black<br />race: Black<br />year: 2003<br />home_owner: 47.69402<br />race: Black","race: Black<br />race: Black<br />year: 2004<br />home_owner: 49.06449<br />race: Black","race: Black<br />race: Black<br />year: 2005<br />home_owner: 49.12738<br />race: Black","race: Black<br />race: Black<br />year: 2006<br />home_owner: 47.27896<br />race: Black","race: Black<br />race: Black<br />year: 2007<br />home_owner: 48.16776<br />race: Black","race: Black<br />race: Black<br />year: 2008<br />home_owner: 47.14453<br />race: Black","race: Black<br />race: Black<br />year: 2009<br />home_owner: 46.41316<br />race: Black","race: Black<br />race: Black<br />year: 2010<br />home_owner: 45.99457<br />race: Black","race: Black<br />race: Black<br />year: 2011<br />home_owner: 44.33017<br />race: Black","race: Black<br />race: Black<br />year: 2012<br />home_owner: 43.28435<br />race: Black","race: Black<br />race: Black<br />year: 2013<br />home_owner: 42.81124<br />race: Black","race: Black<br />race: Black<br />year: 2014<br />home_owner: 42.75398<br />race: Black","race: Black<br />race: Black<br />year: 2015<br />home_owner: 42.30000<br />race: Black","race: Black<br />race: Black<br />year: 2016<br />home_owner: 41.60000<br />race: Black"],"type":"scatter","mode":"lines","line":{"width":4.7244094488189,"color":"rgba(205,133,63,1)","dash":"solid"},"hoveron":"points","name":"Black","legendgroup":"Black","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016],"y":[42.7069199457259,42.2590068159688,42.6150121065375,46.0042540261319,47.5841476655809,46.6461853558628,46.5326633165829,41.2239902080783,40.4299583911234,41.101781691583,40.571647803568,40.5684754521964,40.2246402246402,41.5736040609137,41.1764705882353,38.9549839228296,39.9278883837592,40.0543314216722,41.5647921760391,42.3787976729153,41.2394508124449,43.0759878419453,44.9010477299185,45.2097130242826,45.5306363343706,45.5850109627267,47.471187732165,47.4909604021519,47.3742730071844,49.293808507144,48.7499001517693,49.3023972866723,49.1191243721418,47.8063314711359,47.5635433899835,46.5349432857666,46.117076550052,45.9535444139501,45.3589069215472,45.6,46],"text":["race: Hispanic<br />race: Hispanic<br />year: 1976<br />home_owner: 42.70692<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1977<br />home_owner: 42.25901<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1978<br />home_owner: 42.61501<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1979<br />home_owner: 46.00425<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1980<br />home_owner: 47.58415<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1981<br />home_owner: 46.64619<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1982<br />home_owner: 46.53266<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1983<br />home_owner: 41.22399<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1984<br />home_owner: 40.42996<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1985<br />home_owner: 41.10178<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1986<br />home_owner: 40.57165<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1987<br />home_owner: 40.56848<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1988<br />home_owner: 40.22464<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1989<br />home_owner: 41.57360<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1990<br />home_owner: 41.17647<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1991<br />home_owner: 38.95498<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1992<br />home_owner: 39.92789<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1993<br />home_owner: 40.05433<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1994<br />home_owner: 41.56479<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1995<br />home_owner: 42.37880<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1996<br />home_owner: 41.23945<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1997<br />home_owner: 43.07599<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1998<br />home_owner: 44.90105<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 1999<br />home_owner: 45.20971<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2000<br />home_owner: 45.53064<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2001<br />home_owner: 45.58501<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2002<br />home_owner: 47.47119<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2003<br />home_owner: 47.49096<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2004<br />home_owner: 47.37427<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2005<br />home_owner: 49.29381<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2006<br />home_owner: 48.74990<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2007<br />home_owner: 49.30240<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2008<br />home_owner: 49.11912<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2009<br />home_owner: 47.80633<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2010<br />home_owner: 47.56354<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2011<br />home_owner: 46.53494<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2012<br />home_owner: 46.11708<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2013<br />home_owner: 45.95354<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2014<br />home_owner: 45.35891<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2015<br />home_owner: 45.60000<br />race: Hispanic","race: Hispanic<br />race: Hispanic<br />year: 2016<br />home_owner: 46.00000<br />race: Hispanic"],"type":"scatter","mode":"lines","line":{"width":4.7244094488189,"color":"rgba(54,100,139,1)","dash":"solid"},"hoveron":"points","name":"Hispanic","legendgroup":"Hispanic","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016],"y":[67.7537582308361,67.5531345156305,67.6651626975827,70.1931557593932,70.5324590905237,70.5935552092609,70.1626741711854,67.6177202044218,67.2999354630526,67.2538763806287,66.6227016297535,66.8404844469748,67.156456689903,67.3953395038503,67.4800094806831,67.3438889437803,67.4833180287726,68.1200735840552,67.8250209377693,68.6064702580699,68.9638035285348,69.1590543034835,69.7396232550577,70.3458239691786,70.8067662054727,71.4795068310563,71.8433647250833,72.0934038954662,72.5092973184576,73.0383290267011,72.3853485489593,72.0711683649227,71.8563377912356,71.2068585579819,71.0144623988103,70.6010009760555,69.8712924384308,69.4416867099944,69.0776322767511,68.2,68.2],"text":["race: White<br />race: White<br />year: 1976<br />home_owner: 67.75376<br />race: White","race: White<br />race: White<br />year: 1977<br />home_owner: 67.55313<br />race: White","race: White<br />race: White<br />year: 1978<br />home_owner: 67.66516<br />race: White","race: White<br />race: White<br />year: 1979<br />home_owner: 70.19316<br />race: White","race: White<br />race: White<br />year: 1980<br />home_owner: 70.53246<br />race: White","race: White<br />race: White<br />year: 1981<br />home_owner: 70.59356<br />race: White","race: White<br />race: White<br />year: 1982<br />home_owner: 70.16267<br />race: White","race: White<br />race: White<br />year: 1983<br />home_owner: 67.61772<br />race: White","race: White<br />race: White<br />year: 1984<br />home_owner: 67.29994<br />race: White","race: White<br />race: White<br />year: 1985<br />home_owner: 67.25388<br />race: White","race: White<br />race: White<br />year: 1986<br />home_owner: 66.62270<br />race: White","race: White<br />race: White<br />year: 1987<br />home_owner: 66.84048<br />race: White","race: White<br />race: White<br />year: 1988<br />home_owner: 67.15646<br />race: White","race: White<br />race: White<br />year: 1989<br />home_owner: 67.39534<br />race: White","race: White<br />race: White<br />year: 1990<br />home_owner: 67.48001<br />race: White","race: White<br />race: White<br />year: 1991<br />home_owner: 67.34389<br />race: White","race: White<br />race: White<br />year: 1992<br />home_owner: 67.48332<br />race: White","race: White<br />race: White<br />year: 1993<br />home_owner: 68.12007<br />race: White","race: White<br />race: White<br />year: 1994<br />home_owner: 67.82502<br />race: White","race: White<br />race: White<br />year: 1995<br />home_owner: 68.60647<br />race: White","race: White<br />race: White<br />year: 1996<br />home_owner: 68.96380<br />race: White","race: White<br />race: White<br />year: 1997<br />home_owner: 69.15905<br />race: White","race: White<br />race: White<br />year: 1998<br />home_owner: 69.73962<br />race: White","race: White<br />race: White<br />year: 1999<br />home_owner: 70.34582<br />race: White","race: White<br />race: White<br />year: 2000<br />home_owner: 70.80677<br />race: White","race: White<br />race: White<br />year: 2001<br />home_owner: 71.47951<br />race: White","race: White<br />race: White<br />year: 2002<br />home_owner: 71.84336<br />race: White","race: White<br />race: White<br />year: 2003<br />home_owner: 72.09340<br />race: White","race: White<br />race: White<br />year: 2004<br />home_owner: 72.50930<br />race: White","race: White<br />race: White<br />year: 2005<br />home_owner: 73.03833<br />race: White","race: White<br />race: White<br />year: 2006<br />home_owner: 72.38535<br />race: White","race: White<br />race: White<br />year: 2007<br />home_owner: 72.07117<br />race: White","race: White<br />race: White<br />year: 2008<br />home_owner: 71.85634<br />race: White","race: White<br />race: White<br />year: 2009<br />home_owner: 71.20686<br />race: White","race: White<br />race: White<br />year: 2010<br />home_owner: 71.01446<br />race: White","race: White<br />race: White<br />year: 2011<br />home_owner: 70.60100<br />race: White","race: White<br />race: White<br />year: 2012<br />home_owner: 69.87129<br />race: White","race: White<br />race: White<br />year: 2013<br />home_owner: 69.44169<br />race: White","race: White<br />race: White<br />year: 2014<br />home_owner: 69.07763<br />race: White","race: White<br />race: White<br />year: 2015<br />home_owner: 68.20000<br />race: White","race: White<br />race: White<br />year: 2016<br />home_owner: 68.20000<br />race: White"],"type":"scatter","mode":"lines","line":{"width":4.7244094488189,"color":"rgba(139,62,47,1)","dash":"solid"},"hoveron":"points","name":"White","legendgroup":"White","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"name":"(Black,1,NA)","legendgroup":"(Black,1,NA)","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"name":"(Hispanic,1,NA)","legendgroup":"(Hispanic,1,NA)","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"name":"(White,1,NA)","legendgroup":"(White,1,NA)","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":22.648401826484},"plot_bgcolor":"rgba(238,233,233,1)","paper_bgcolor":"rgba(238,233,233,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"US Homeownership by Race/Ethnicity","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1973.75,2023.25],"tickmode":"array","ticktext":["1980","1990","2000","2010","2020"],"tickvals":[1980,1990,2000,2010,2020],"categoryorder":"array","categoryarray":["1980","1990","2000","2010","2020"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":true,"linecolor":"rgba(204,204,204,1)","linewidth":0.66417600664176,"showgrid":true,"gridcolor":"rgba(204,204,204,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[37.250816667636,74.7424962818947],"tickmode":"array","ticktext":["40","50","60","70"],"tickvals":[40,50,60,70],"categoryorder":"array","categoryarray":["40","50","60","70"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":true,"linecolor":"rgba(204,204,204,1)","linewidth":0.66417600664176,"showgrid":true,"gridcolor":"rgba(204,204,204,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":"transparent","line":{"color":"rgba(204,204,204,1)","width":0.66417600664176,"linetype":"solid"},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"32885a1a2596":{"linetype":{},"size":{},"x":{},"y":{},"colour":{},"type":"scatter"},"328845dc12c3":{"label":{},"x":{},"y":{},"colour":{}}},"cur_data":"32885a1a2596","visdat":{"32885a1a2596":["function (y) ","x"],"328845dc12c3":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
  
  

```r
lettuce <- garden_harvest %>% 
  filter(vegetable == "lettuce") %>% 
  count(variety, name = "var_count") %>% 
  arrange(desc(var_count)) %>% 
  ggplot(aes(x = var_count, y = variety)) +
  geom_col() +
  labs(title = "Lettuce Harvests by Species", 
       x = "Number of Times Each Species was Harvested", 
       y = "Lettuce Species")

ggplotly(lettuce)
```

<!--html_preserve--><div id="htmlwidget-c572e7afe6dfcd0340fe" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-c572e7afe6dfcd0340fe">{"x":{"data":[{"orientation":"v","width":[29,27,9,3,1],"base":[1.55,0.55,4.55,3.55,2.55],"x":[14.5,13.5,4.5,1.5,0.5],"y":[0.9,0.9,0.9,0.9,0.9],"text":["var_count: 29<br />variety: Lettuce Mixture","var_count: 27<br />variety: Farmer's Market Blend","var_count:  9<br />variety: Tatsoi","var_count:  3<br />variety: reseed","var_count:  1<br />variety: mustard greens"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(89,89,89,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":148.310502283105},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Lettuce Harvests by Species","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.45,30.45],"tickmode":"array","ticktext":["0","10","20","30"],"tickvals":[0,10,20,30],"categoryorder":"array","categoryarray":["0","10","20","30"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Number of Times Each Species was Harvested","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,5.6],"tickmode":"array","ticktext":["Farmer's Market Blend","Lettuce Mixture","mustard greens","reseed","Tatsoi"],"tickvals":[1,2,3,4,5],"categoryorder":"array","categoryarray":["Farmer's Market Blend","Lettuce Mixture","mustard greens","reseed","Tatsoi"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"Lettuce Species","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"32881853ef2":{"x":{},"y":{},"type":"bar"}},"cur_data":"32881853ef2","visdat":{"32881853ef2":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
  
  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
small_trains %>% 
  filter(departure_station == "PARIS EST") %>% 
  group_by(year, arrival_station) %>% 
  summarize(avg_delay = mean(avg_delay_all_departing)) %>% 
  ggplot(aes(x = year, y = avg_delay, color = arrival_station)) +
  geom_line(size = 1.3) +
  labs(title = "Average Delay (Min) of All Departing Trains from PARIS EST Station",
       subtitle = "Year: {frame_along}",
       x = "",
       y = "",
       color = "Arrival Station") +
  transition_reveal(year)

anim_save("train_animation.gif")
```


```r
#anim_save("train_animation.gif")
```


```r
knitr::include_graphics("train_animation.gif")
```

![](train_animation.gif)<!-- -->


## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 

I have started the code for you below. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0.


```r
garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, date, fill = list(daily_harvest_lb = 0))
```

```
## `summarise()` regrouping output by 'date' (override with `.groups` argument)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["variety"],"name":[1],"type":["chr"],"align":["left"]},{"label":["date"],"name":[2],"type":["date"],"align":["right"]},{"label":["daily_harvest_lb"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Amish Paste","2":"2020-07-11","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-21","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-24","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-25","3":"1.02073906"},{"1":"Amish Paste","2":"2020-07-26","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-27","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-28","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-29","3":"0.46076558"},{"1":"Amish Paste","2":"2020-07-30","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-31","3":"0.43431014"},{"1":"Amish Paste","2":"2020-08-01","3":"0.21384814"},{"1":"Amish Paste","2":"2020-08-02","3":"1.12215158"},{"1":"Amish Paste","2":"2020-08-03","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-04","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-05","3":"0.84216484"},{"1":"Amish Paste","2":"2020-08-06","3":"0.38580850"},{"1":"Amish Paste","2":"2020-08-07","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-08","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-09","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-10","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-11","3":"1.11553772"},{"1":"Amish Paste","2":"2020-08-13","3":"1.41536604"},{"1":"Amish Paste","2":"2020-08-14","3":"1.15742550"},{"1":"Amish Paste","2":"2020-08-16","3":"1.23458720"},{"1":"Amish Paste","2":"2020-08-17","3":"1.29631656"},{"1":"Amish Paste","2":"2020-08-18","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-19","3":"2.19800614"},{"1":"Amish Paste","2":"2020-08-20","3":"2.22666620"},{"1":"Amish Paste","2":"2020-08-21","3":"0.94357736"},{"1":"Amish Paste","2":"2020-08-23","3":"3.39952404"},{"1":"Amish Paste","2":"2020-08-24","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-25","3":"3.08646800"},{"1":"Amish Paste","2":"2020-08-26","3":"4.15791332"},{"1":"Amish Paste","2":"2020-08-29","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-30","3":"6.46835508"},{"1":"Amish Paste","2":"2020-09-01","3":"3.38850094"},{"1":"Amish Paste","2":"2020-09-03","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-04","3":"4.76197920"},{"1":"Amish Paste","2":"2020-09-06","3":"2.90348454"},{"1":"Amish Paste","2":"2020-09-10","3":"1.52559704"},{"1":"Amish Paste","2":"2020-09-15","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-17","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-18","3":"0.50265336"},{"1":"Amish Paste","2":"2020-09-19","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-21","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-25","3":"6.03624956"},{"1":"Amish Paste","2":"2020-09-30","3":"3.19008514"},{"1":"Amish Paste","2":"2020-10-03","3":"0.55556424"},{"1":"Amish Paste","2":"2020-10-07","3":"1.57630330"},{"1":"Amish Paste","2":"2020-10-10","3":"0.00000000"},{"1":"Amish Paste","2":"2020-10-11","3":"5.46304836"},{"1":"Amish Paste","2":"2020-10-14","3":"2.59042850"},{"1":"Better Boy","2":"2020-07-11","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-21","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-24","3":"0.48501640"},{"1":"Better Boy","2":"2020-07-25","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-26","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-27","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-28","3":"0.68784144"},{"1":"Better Boy","2":"2020-07-29","3":"0.97444204"},{"1":"Better Boy","2":"2020-07-30","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-31","3":"0.63933980"},{"1":"Better Boy","2":"2020-08-01","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-02","3":"0.46517482"},{"1":"Better Boy","2":"2020-08-03","3":"0.67902296"},{"1":"Better Boy","2":"2020-08-04","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-05","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-06","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-07","3":"2.30382790"},{"1":"Better Boy","2":"2020-08-08","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-09","3":"2.42949124"},{"1":"Better Boy","2":"2020-08-10","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-11","3":"0.78043548"},{"1":"Better Boy","2":"2020-08-13","3":"1.60275874"},{"1":"Better Boy","2":"2020-08-14","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-16","3":"0.52469956"},{"1":"Better Boy","2":"2020-08-17","3":"1.68432968"},{"1":"Better Boy","2":"2020-08-18","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-19","3":"1.35584130"},{"1":"Better Boy","2":"2020-08-20","3":"0.50706260"},{"1":"Better Boy","2":"2020-08-21","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-23","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-24","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-25","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-26","3":"0.68122758"},{"1":"Better Boy","2":"2020-08-29","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-30","3":"0.86641566"},{"1":"Better Boy","2":"2020-09-01","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-03","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-04","3":"6.39119338"},{"1":"Better Boy","2":"2020-09-06","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-10","3":"3.06883104"},{"1":"Better Boy","2":"2020-09-15","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-17","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-18","3":"1.47709540"},{"1":"Better Boy","2":"2020-09-19","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-21","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-25","3":"2.73152418"},{"1":"Better Boy","2":"2020-09-30","3":"1.08908228"},{"1":"Better Boy","2":"2020-10-03","3":"0.00000000"},{"1":"Better Boy","2":"2020-10-07","3":"0.00000000"},{"1":"Better Boy","2":"2020-10-10","3":"0.00000000"},{"1":"Better Boy","2":"2020-10-11","3":"1.15963012"},{"1":"Better Boy","2":"2020-10-14","3":"1.42418452"},{"1":"Big Beef","2":"2020-07-11","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-21","3":"0.30203294"},{"1":"Big Beef","2":"2020-07-24","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-25","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-26","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-27","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-28","3":"0.44753786"},{"1":"Big Beef","2":"2020-07-29","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-30","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-31","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-01","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-02","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-03","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-04","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-05","3":"0.49163026"},{"1":"Big Beef","2":"2020-08-06","3":"0.67681834"},{"1":"Big Beef","2":"2020-08-07","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-08","3":"0.35714844"},{"1":"Big Beef","2":"2020-08-09","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-10","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-11","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-13","3":"0.91050806"},{"1":"Big Beef","2":"2020-08-14","3":"0.58642892"},{"1":"Big Beef","2":"2020-08-16","3":"0.87523414"},{"1":"Big Beef","2":"2020-08-17","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-18","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-19","3":"0.58201968"},{"1":"Big Beef","2":"2020-08-20","3":"0.75838928"},{"1":"Big Beef","2":"2020-08-21","3":"1.85629004"},{"1":"Big Beef","2":"2020-08-23","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-24","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-25","3":"2.18918766"},{"1":"Big Beef","2":"2020-08-26","3":"1.09569614"},{"1":"Big Beef","2":"2020-08-29","3":"2.27737246"},{"1":"Big Beef","2":"2020-08-30","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-01","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-03","3":"2.78884430"},{"1":"Big Beef","2":"2020-09-04","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-06","3":"3.63541838"},{"1":"Big Beef","2":"2020-09-10","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-15","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-17","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-18","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-19","3":"0.67020448"},{"1":"Big Beef","2":"2020-09-21","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-25","3":"1.45284458"},{"1":"Big Beef","2":"2020-09-30","3":"0.00000000"},{"1":"Big Beef","2":"2020-10-03","3":"0.00000000"},{"1":"Big Beef","2":"2020-10-07","3":"0.59965664"},{"1":"Big Beef","2":"2020-10-10","3":"0.00000000"},{"1":"Big Beef","2":"2020-10-11","3":"0.69665992"},{"1":"Big Beef","2":"2020-10-14","3":"1.74385442"},{"1":"Black Krim","2":"2020-07-11","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-21","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-24","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-25","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-26","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-27","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-28","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-29","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-30","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-31","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-01","3":"0.96121432"},{"1":"Black Krim","2":"2020-08-02","3":"1.88935934"},{"1":"Black Krim","2":"2020-08-03","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-04","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-05","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-06","3":"0.86641566"},{"1":"Black Krim","2":"2020-08-07","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-08","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-09","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-10","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-11","3":"0.79145858"},{"1":"Black Krim","2":"2020-08-13","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-14","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-16","3":"0.64154442"},{"1":"Black Krim","2":"2020-08-17","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-18","3":"0.69886454"},{"1":"Black Krim","2":"2020-08-19","3":"1.27647498"},{"1":"Black Krim","2":"2020-08-20","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-21","3":"3.39070556"},{"1":"Black Krim","2":"2020-08-23","3":"3.46786726"},{"1":"Black Krim","2":"2020-08-24","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-25","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-26","3":"0.47619792"},{"1":"Black Krim","2":"2020-08-29","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-30","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-01","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-03","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-04","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-06","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-10","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-15","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-17","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-18","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-19","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-21","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-25","3":"0.52029032"},{"1":"Black Krim","2":"2020-09-30","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-03","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-07","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-10","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-11","3":"0.82673250"},{"1":"Black Krim","2":"2020-10-14","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-11","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-21","3":"0.74736618"},{"1":"Bonny Best","2":"2020-07-24","3":"0.30864680"},{"1":"Bonny Best","2":"2020-07-25","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-26","3":"0.32628376"},{"1":"Bonny Best","2":"2020-07-27","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-28","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-29","3":"0.33730686"},{"1":"Bonny Best","2":"2020-07-30","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-31","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-01","3":"0.95900970"},{"1":"Bonny Best","2":"2020-08-02","3":"0.34392072"},{"1":"Bonny Best","2":"2020-08-03","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-04","3":"0.85318794"},{"1":"Bonny Best","2":"2020-08-05","3":"1.24120106"},{"1":"Bonny Best","2":"2020-08-06","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-07","3":"0.79145858"},{"1":"Bonny Best","2":"2020-08-08","3":"1.24340568"},{"1":"Bonny Best","2":"2020-08-09","3":"0.39462698"},{"1":"Bonny Best","2":"2020-08-10","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-11","3":"0.67681834"},{"1":"Bonny Best","2":"2020-08-13","3":"0.73193384"},{"1":"Bonny Best","2":"2020-08-14","3":"1.56748482"},{"1":"Bonny Best","2":"2020-08-16","3":"1.19710866"},{"1":"Bonny Best","2":"2020-08-17","3":"0.80248168"},{"1":"Bonny Best","2":"2020-08-18","3":"0.59745202"},{"1":"Bonny Best","2":"2020-08-19","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-20","3":"1.39331984"},{"1":"Bonny Best","2":"2020-08-21","3":"0.72752460"},{"1":"Bonny Best","2":"2020-08-23","3":"0.59304278"},{"1":"Bonny Best","2":"2020-08-24","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-25","3":"1.38670598"},{"1":"Bonny Best","2":"2020-08-26","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-29","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-30","3":"0.34171610"},{"1":"Bonny Best","2":"2020-09-01","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-03","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-04","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-06","3":"1.56528020"},{"1":"Bonny Best","2":"2020-09-10","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-15","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-17","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-18","3":"2.31926024"},{"1":"Bonny Best","2":"2020-09-19","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-21","3":"1.57409868"},{"1":"Bonny Best","2":"2020-09-25","3":"1.05160374"},{"1":"Bonny Best","2":"2020-09-30","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-03","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-07","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-10","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-11","3":"0.85098332"},{"1":"Bonny Best","2":"2020-10-14","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-11","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-21","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-24","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-25","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-26","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-27","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-28","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-29","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-30","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-31","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-01","3":"0.70547840"},{"1":"Brandywine","2":"2020-08-02","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-03","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-04","3":"0.50926722"},{"1":"Brandywine","2":"2020-08-05","3":"0.63933980"},{"1":"Brandywine","2":"2020-08-06","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-07","3":"0.78484472"},{"1":"Brandywine","2":"2020-08-08","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-09","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-10","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-11","3":"0.48060716"},{"1":"Brandywine","2":"2020-08-13","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-14","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-16","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-17","3":"0.67240910"},{"1":"Brandywine","2":"2020-08-18","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-19","3":"0.73854770"},{"1":"Brandywine","2":"2020-08-20","3":"1.06483146"},{"1":"Brandywine","2":"2020-08-21","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-23","3":"0.98326052"},{"1":"Brandywine","2":"2020-08-24","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-25","3":"1.92022402"},{"1":"Brandywine","2":"2020-08-26","3":"2.29721404"},{"1":"Brandywine","2":"2020-08-29","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-30","3":"1.01412520"},{"1":"Brandywine","2":"2020-09-01","3":"0.39242236"},{"1":"Brandywine","2":"2020-09-03","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-04","3":"0.94798660"},{"1":"Brandywine","2":"2020-09-06","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-10","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-15","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-17","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-18","3":"1.57409868"},{"1":"Brandywine","2":"2020-09-19","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-21","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-25","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-30","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-03","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-07","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-10","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-11","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-14","3":"0.92153116"},{"1":"Cherokee Purple","2":"2020-07-11","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-21","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-24","3":"0.54454114"},{"1":"Cherokee Purple","2":"2020-07-25","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-26","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-27","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-28","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-29","3":"0.52910880"},{"1":"Cherokee Purple","2":"2020-07-30","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-31","3":"0.67681834"},{"1":"Cherokee Purple","2":"2020-08-01","3":"1.36465978"},{"1":"Cherokee Purple","2":"2020-08-02","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-03","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-04","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-05","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-06","3":"0.66799986"},{"1":"Cherokee Purple","2":"2020-08-07","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-08","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-09","3":"0.67902296"},{"1":"Cherokee Purple","2":"2020-08-10","3":"0.47619792"},{"1":"Cherokee Purple","2":"2020-08-11","3":"1.76810524"},{"1":"Cherokee Purple","2":"2020-08-13","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-14","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-16","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-17","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-18","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-19","3":"1.92242864"},{"1":"Cherokee Purple","2":"2020-08-20","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-21","3":"3.52959662"},{"1":"Cherokee Purple","2":"2020-08-23","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-24","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-25","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-26","3":"1.30733966"},{"1":"Cherokee Purple","2":"2020-08-29","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-30","3":"1.32056738"},{"1":"Cherokee Purple","2":"2020-09-01","3":"0.44312862"},{"1":"Cherokee Purple","2":"2020-09-03","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-04","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-06","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-10","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-15","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-17","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-18","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-19","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-21","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-25","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-30","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-03","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-07","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-10","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-11","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-14","3":"0.48281178"},{"1":"grape","2":"2020-07-11","3":"0.05291088"},{"1":"grape","2":"2020-07-21","3":"0.18959732"},{"1":"grape","2":"2020-07-24","3":"0.06834322"},{"1":"grape","2":"2020-07-25","3":"0.23368972"},{"1":"grape","2":"2020-07-26","3":"0.00000000"},{"1":"grape","2":"2020-07-27","3":"0.00000000"},{"1":"grape","2":"2020-07-28","3":"0.28880522"},{"1":"grape","2":"2020-07-29","3":"0.08818480"},{"1":"grape","2":"2020-07-30","3":"0.20062042"},{"1":"grape","2":"2020-07-31","3":"0.22046200"},{"1":"grape","2":"2020-08-01","3":"0.37037616"},{"1":"grape","2":"2020-08-02","3":"0.22487124"},{"1":"grape","2":"2020-08-03","3":"0.00000000"},{"1":"grape","2":"2020-08-04","3":"0.26014516"},{"1":"grape","2":"2020-08-05","3":"0.47840254"},{"1":"grape","2":"2020-08-06","3":"0.00000000"},{"1":"grape","2":"2020-08-07","3":"0.64374904"},{"1":"grape","2":"2020-08-08","3":"0.17857422"},{"1":"grape","2":"2020-08-09","3":"0.14109568"},{"1":"grape","2":"2020-08-10","3":"0.00000000"},{"1":"grape","2":"2020-08-11","3":"0.66579524"},{"1":"grape","2":"2020-08-13","3":"0.92814502"},{"1":"grape","2":"2020-08-14","3":"0.27778212"},{"1":"grape","2":"2020-08-16","3":"1.05160374"},{"1":"grape","2":"2020-08-17","3":"0.96121432"},{"1":"grape","2":"2020-08-18","3":"0.29982832"},{"1":"grape","2":"2020-08-19","3":"0.99428362"},{"1":"grape","2":"2020-08-20","3":"1.08687766"},{"1":"grape","2":"2020-08-21","3":"0.58422430"},{"1":"grape","2":"2020-08-23","3":"0.96121432"},{"1":"grape","2":"2020-08-24","3":"0.16534650"},{"1":"grape","2":"2020-08-25","3":"1.11553772"},{"1":"grape","2":"2020-08-26","3":"1.80558378"},{"1":"grape","2":"2020-08-29","3":"0.83775560"},{"1":"grape","2":"2020-08-30","3":"1.83644846"},{"1":"grape","2":"2020-09-01","3":"0.00000000"},{"1":"grape","2":"2020-09-03","3":"2.49342522"},{"1":"grape","2":"2020-09-04","3":"0.97444204"},{"1":"grape","2":"2020-09-06","3":"1.35584130"},{"1":"grape","2":"2020-09-10","3":"1.12215158"},{"1":"grape","2":"2020-09-15","3":"0.56879196"},{"1":"grape","2":"2020-09-17","3":"0.00000000"},{"1":"grape","2":"2020-09-18","3":"0.00000000"},{"1":"grape","2":"2020-09-19","3":"2.33248796"},{"1":"grape","2":"2020-09-21","3":"0.00000000"},{"1":"grape","2":"2020-09-25","3":"1.80558378"},{"1":"grape","2":"2020-09-30","3":"1.49473236"},{"1":"grape","2":"2020-10-03","3":"0.00000000"},{"1":"grape","2":"2020-10-07","3":"0.00000000"},{"1":"grape","2":"2020-10-10","3":"3.03576174"},{"1":"grape","2":"2020-10-11","3":"0.00000000"},{"1":"grape","2":"2020-10-14","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-11","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-21","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-24","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-25","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-26","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-27","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-28","3":"0.69445530"},{"1":"Jet Star","2":"2020-07-29","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-30","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-31","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-01","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-02","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-03","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-04","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-05","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-06","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-07","3":"1.23899644"},{"1":"Jet Star","2":"2020-08-08","3":"0.40565008"},{"1":"Jet Star","2":"2020-08-09","3":"1.30293042"},{"1":"Jet Star","2":"2020-08-10","3":"0.53131342"},{"1":"Jet Star","2":"2020-08-11","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-13","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-14","3":"0.39903622"},{"1":"Jet Star","2":"2020-08-16","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-17","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-18","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-19","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-20","3":"0.79366320"},{"1":"Jet Star","2":"2020-08-21","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-23","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-24","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-25","3":"1.27427036"},{"1":"Jet Star","2":"2020-08-26","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-29","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-30","3":"1.65787424"},{"1":"Jet Star","2":"2020-09-01","3":"1.70417126"},{"1":"Jet Star","2":"2020-09-03","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-04","3":"2.59704236"},{"1":"Jet Star","2":"2020-09-06","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-10","3":"1.66228348"},{"1":"Jet Star","2":"2020-09-15","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-17","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-18","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-19","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-21","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-25","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-30","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-03","3":"0.76279852"},{"1":"Jet Star","2":"2020-10-07","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-10","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-11","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-14","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-11","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-21","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-24","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-25","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-26","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-27","3":"1.76590062"},{"1":"Mortgage Lifter","2":"2020-07-28","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-29","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-30","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-31","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-01","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-02","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-03","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-04","3":"0.74736618"},{"1":"Mortgage Lifter","2":"2020-08-05","3":"1.72180822"},{"1":"Mortgage Lifter","2":"2020-08-06","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-07","3":"0.80248168"},{"1":"Mortgage Lifter","2":"2020-08-08","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-09","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-10","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-11","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-13","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-14","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-16","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-17","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-18","3":"1.34040896"},{"1":"Mortgage Lifter","2":"2020-08-19","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-20","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-21","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-23","3":"1.55205248"},{"1":"Mortgage Lifter","2":"2020-08-24","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-25","3":"2.26194012"},{"1":"Mortgage Lifter","2":"2020-08-26","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-29","3":"2.41846814"},{"1":"Mortgage Lifter","2":"2020-08-30","3":"1.29852118"},{"1":"Mortgage Lifter","2":"2020-09-01","3":"2.64995324"},{"1":"Mortgage Lifter","2":"2020-09-03","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-04","3":"0.56217810"},{"1":"Mortgage Lifter","2":"2020-09-06","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-10","3":"0.69665992"},{"1":"Mortgage Lifter","2":"2020-09-15","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-17","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-18","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-19","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-21","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-25","3":"4.42246772"},{"1":"Mortgage Lifter","2":"2020-09-30","3":"0.72091074"},{"1":"Mortgage Lifter","2":"2020-10-03","3":"0.46958406"},{"1":"Mortgage Lifter","2":"2020-10-07","3":"0.55997348"},{"1":"Mortgage Lifter","2":"2020-10-10","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-10-11","3":"0.44092400"},{"1":"Mortgage Lifter","2":"2020-10-14","3":"1.89376858"},{"1":"Old German","2":"2020-07-11","3":"0.00000000"},{"1":"Old German","2":"2020-07-21","3":"0.00000000"},{"1":"Old German","2":"2020-07-24","3":"0.00000000"},{"1":"Old German","2":"2020-07-25","3":"0.00000000"},{"1":"Old German","2":"2020-07-26","3":"0.00000000"},{"1":"Old German","2":"2020-07-27","3":"0.00000000"},{"1":"Old German","2":"2020-07-28","3":"1.34702282"},{"1":"Old German","2":"2020-07-29","3":"0.00000000"},{"1":"Old German","2":"2020-07-30","3":"0.00000000"},{"1":"Old German","2":"2020-07-31","3":"1.39552446"},{"1":"Old German","2":"2020-08-01","3":"0.00000000"},{"1":"Old German","2":"2020-08-02","3":"0.74075232"},{"1":"Old German","2":"2020-08-03","3":"0.00000000"},{"1":"Old German","2":"2020-08-04","3":"0.00000000"},{"1":"Old German","2":"2020-08-05","3":"0.00000000"},{"1":"Old German","2":"2020-08-06","3":"0.00000000"},{"1":"Old German","2":"2020-08-07","3":"0.51367646"},{"1":"Old German","2":"2020-08-08","3":"0.00000000"},{"1":"Old German","2":"2020-08-09","3":"0.00000000"},{"1":"Old German","2":"2020-08-10","3":"0.00000000"},{"1":"Old German","2":"2020-08-11","3":"0.00000000"},{"1":"Old German","2":"2020-08-13","3":"0.00000000"},{"1":"Old German","2":"2020-08-14","3":"0.52469956"},{"1":"Old German","2":"2020-08-16","3":"1.32056738"},{"1":"Old German","2":"2020-08-17","3":"0.00000000"},{"1":"Old German","2":"2020-08-18","3":"0.23148510"},{"1":"Old German","2":"2020-08-19","3":"0.00000000"},{"1":"Old German","2":"2020-08-20","3":"0.00000000"},{"1":"Old German","2":"2020-08-21","3":"0.53572266"},{"1":"Old German","2":"2020-08-23","3":"1.76590062"},{"1":"Old German","2":"2020-08-24","3":"0.00000000"},{"1":"Old German","2":"2020-08-25","3":"0.25353130"},{"1":"Old German","2":"2020-08-26","3":"1.46827692"},{"1":"Old German","2":"2020-08-29","3":"0.00000000"},{"1":"Old German","2":"2020-08-30","3":"1.89817782"},{"1":"Old German","2":"2020-09-01","3":"1.77471910"},{"1":"Old German","2":"2020-09-03","3":"0.00000000"},{"1":"Old German","2":"2020-09-04","3":"0.00000000"},{"1":"Old German","2":"2020-09-06","3":"0.00000000"},{"1":"Old German","2":"2020-09-10","3":"1.48591388"},{"1":"Old German","2":"2020-09-15","3":"0.00000000"},{"1":"Old German","2":"2020-09-17","3":"0.00000000"},{"1":"Old German","2":"2020-09-18","3":"3.59573522"},{"1":"Old German","2":"2020-09-19","3":"0.00000000"},{"1":"Old German","2":"2020-09-21","3":"0.00000000"},{"1":"Old German","2":"2020-09-25","3":"4.01902226"},{"1":"Old German","2":"2020-09-30","3":"0.00000000"},{"1":"Old German","2":"2020-10-03","3":"0.00000000"},{"1":"Old German","2":"2020-10-07","3":"0.80027706"},{"1":"Old German","2":"2020-10-10","3":"0.00000000"},{"1":"Old German","2":"2020-10-11","3":"1.97974876"},{"1":"Old German","2":"2020-10-14","3":"1.06703608"},{"1":"volunteers","2":"2020-07-11","3":"0.00000000"},{"1":"volunteers","2":"2020-07-21","3":"0.00000000"},{"1":"volunteers","2":"2020-07-24","3":"0.00000000"},{"1":"volunteers","2":"2020-07-25","3":"0.00000000"},{"1":"volunteers","2":"2020-07-26","3":"0.00000000"},{"1":"volunteers","2":"2020-07-27","3":"0.00000000"},{"1":"volunteers","2":"2020-07-28","3":"0.00000000"},{"1":"volunteers","2":"2020-07-29","3":"0.00000000"},{"1":"volunteers","2":"2020-07-30","3":"0.00000000"},{"1":"volunteers","2":"2020-07-31","3":"0.00000000"},{"1":"volunteers","2":"2020-08-01","3":"0.00000000"},{"1":"volunteers","2":"2020-08-02","3":"0.00000000"},{"1":"volunteers","2":"2020-08-03","3":"0.00000000"},{"1":"volunteers","2":"2020-08-04","3":"0.16093726"},{"1":"volunteers","2":"2020-08-05","3":"0.14770954"},{"1":"volunteers","2":"2020-08-06","3":"0.00000000"},{"1":"volunteers","2":"2020-08-07","3":"0.00000000"},{"1":"volunteers","2":"2020-08-08","3":"0.00000000"},{"1":"volunteers","2":"2020-08-09","3":"0.11904948"},{"1":"volunteers","2":"2020-08-10","3":"0.00000000"},{"1":"volunteers","2":"2020-08-11","3":"0.35273920"},{"1":"volunteers","2":"2020-08-13","3":"0.00000000"},{"1":"volunteers","2":"2020-08-14","3":"1.08026380"},{"1":"volunteers","2":"2020-08-16","3":"0.72311536"},{"1":"volunteers","2":"2020-08-17","3":"0.67461372"},{"1":"volunteers","2":"2020-08-18","3":"0.32628376"},{"1":"volunteers","2":"2020-08-19","3":"0.67461372"},{"1":"volunteers","2":"2020-08-20","3":"0.73413846"},{"1":"volunteers","2":"2020-08-21","3":"1.23899644"},{"1":"volunteers","2":"2020-08-23","3":"0.00000000"},{"1":"volunteers","2":"2020-08-24","3":"0.00000000"},{"1":"volunteers","2":"2020-08-25","3":"1.07585456"},{"1":"volunteers","2":"2020-08-26","3":"0.57540582"},{"1":"volunteers","2":"2020-08-29","3":"2.87261986"},{"1":"volunteers","2":"2020-08-30","3":"1.81219764"},{"1":"volunteers","2":"2020-09-01","3":"4.30562286"},{"1":"volunteers","2":"2020-09-03","3":"1.34481820"},{"1":"volunteers","2":"2020-09-04","3":"2.72050108"},{"1":"volunteers","2":"2020-09-06","3":"5.24038174"},{"1":"volunteers","2":"2020-09-10","3":"0.91050806"},{"1":"volunteers","2":"2020-09-15","3":"1.59834950"},{"1":"volunteers","2":"2020-09-17","3":"0.46737944"},{"1":"volunteers","2":"2020-09-18","3":"0.00000000"},{"1":"volunteers","2":"2020-09-19","3":"6.46835508"},{"1":"volunteers","2":"2020-09-21","3":"0.20943890"},{"1":"volunteers","2":"2020-09-25","3":"4.36073836"},{"1":"volunteers","2":"2020-09-30","3":"0.15432340"},{"1":"volunteers","2":"2020-10-03","3":"0.00000000"},{"1":"volunteers","2":"2020-10-07","3":"0.14109568"},{"1":"volunteers","2":"2020-10-10","3":"4.35853374"},{"1":"volunteers","2":"2020-10-11","3":"0.50706260"},{"1":"volunteers","2":"2020-10-14","3":"6.25671156"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>


## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  
  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

  
## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the y-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  
  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for all Fridays. So, use `wday()` to create a day of week variable and filter to all the Fridays.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  



```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   state = col_character(),
##   est_pop_2018 = col_double()
## )
```

```r
states_map <- map_data("state")
```

## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
