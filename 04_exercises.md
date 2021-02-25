---
title: 'Weekly Exercises #4'
author: "Brian Lee"
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
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
## ✓ tibble  3.0.5     ✓ dplyr   1.0.2
## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
## ✓ readr   1.4.0     ✓ forcats 0.5.0
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
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
## Linking to GEOS 3.8.1, GDAL 3.1.1, PROJ 6.3.1
```

```r
library(leaflet)       # for highly customizable mapping
library(carData)       # for Minneapolis police stops data
library(ggthemes)      # for more themes (including theme_map())
theme_set(theme_minimal())
```


```r
# Starbucks locations
Starbucks <- read_csv("https://www.macalester.edu/~ajohns24/Data/Starbucks.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   Brand = col_character(),
##   `Store Number` = col_character(),
##   `Store Name` = col_character(),
##   `Ownership Type` = col_character(),
##   `Street Address` = col_character(),
##   City = col_character(),
##   `State/Province` = col_character(),
##   Country = col_character(),
##   Postcode = col_character(),
##   `Phone Number` = col_character(),
##   Timezone = col_character(),
##   Longitude = col_double(),
##   Latitude = col_double()
## )
```

```r
starbucks_us_by_state <- Starbucks %>% 
  filter(Country == "US") %>% 
  count(`State/Province`) %>% 
  mutate(state_name = str_to_lower(abbr2state(`State/Province`))) 

# Lisa's favorite St. Paul places - example for you to create your own data
favorite_stp_by_lisa <- tibble(
  place = c("Home", "Macalester College", "Adams Spanish Immersion", 
            "Spirit Gymnastics", "Bama & Bapa", "Now Bikes",
            "Dance Spectrum", "Pizza Luce", "Brunson's"),
  long = c(-93.1405743, -93.1712321, -93.1451796, 
           -93.1650563, -93.1542883, -93.1696608, 
           -93.1393172, -93.1524256, -93.0753863),
  lat = c(44.950576, 44.9378965, 44.9237914,
          44.9654609, 44.9295072, 44.9436813, 
          44.9399922, 44.9468848, 44.9700727)
  )

#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   date = col_date(format = ""),
##   state = col_character(),
##   fips = col_character(),
##   cases = col_double(),
##   deaths = col_double()
## )
```

## Put your homework on GitHub!

If you were not able to get set up on GitHub last week, go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) and get set up first. Then, do the following (if you get stuck on a step, don't worry, I will help! You can always get started on the homework and we can figure out the GitHub piece later):

* Create a repository on GitHub, giving it a nice name so you know it is for the 4th weekly exercise assignment (follow the instructions in the document/video).  
* Copy the repo name so you can clone it to your computer. In R Studio, go to file --> New project --> Version control --> Git and follow the instructions from the document/video.  
* Download the code from this document and save it in the repository folder/project on your computer.  
* In R Studio, you should then see the .Rmd file in the upper right corner in the Git tab (along with the .Rproj file and probably .gitignore).  
* Check all the boxes of the files in the Git tab under Stage and choose commit.  
* In the commit window, write a commit message, something like "Initial upload" would be appropriate, and commit the files.  
* Either click the green up arrow in the commit window or close the commit window and click the green up arrow in the Git tab to push your changes to GitHub.  
* Refresh your GitHub page (online) and make sure the new documents have been pushed out.  
* Back in R Studio, knit the .Rmd file. When you do that, you should have two (as long as you didn't make any changes to the .Rmd file, in which case you might have three) files show up in the Git tab - an .html file and an .md file. The .md file is something we haven't seen before and is here because I included `keep_md: TRUE` in the YAML heading. The .md file is a markdown (NOT R Markdown) file that is an interim step to creating the html file. They are displayed fairly nicely in GitHub, so we want to keep it and look at it there. Click the boxes next to these two files, commit changes (remember to include a commit message), and push them (green up arrow).  
* As you work through your homework, save and commit often, push changes occasionally (maybe after you feel finished with an exercise?), and go check to see what the .md file looks like on GitHub.  
* If you have issues, let me know! This is new to many of you and may not be intuitive at first. But, I promise, you'll get the hang of it! 


## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.


## Warm-up exercises from tutorial

These exercises will reiterate what you learned in the "Mapping data with R" tutorial. If you haven't gone through the tutorial yet, you should do that first.

### Starbucks locations (`ggmap`)

  1. Add the `Starbucks` locations to a world map. Add an aesthetic to the world map that sets the color of the points according to the ownership type. What, if anything, can you deduce from this visualization?  


```r
sbux <- Starbucks
class(sbux$'Ownership Type')
```

```
## [1] "character"
```

```r
sbux$'Ownership Type' <- as.factor(sbux$'Ownership Type')
class(sbux$'Ownership Type')
```

```
## [1] "factor"
```

```r
levels(sbux$'Ownership Type')
```

```
## [1] "Company Owned" "Franchise"     "Joint Venture" "Licensed"
```



```r
# Get the map information
world <- get_stamenmap(
    bbox = c(left = -180, bottom = -57, right = 179, top = 82.1), 
    maptype = "terrain",
    zoom = 2)
```

```
## Source : http://tile.stamen.com/terrain/2/0/0.png
```

```
## Source : http://tile.stamen.com/terrain/2/1/0.png
```

```
## Source : http://tile.stamen.com/terrain/2/2/0.png
```

```
## Source : http://tile.stamen.com/terrain/2/3/0.png
```

```
## Source : http://tile.stamen.com/terrain/2/0/1.png
```

```
## Source : http://tile.stamen.com/terrain/2/1/1.png
```

```
## Source : http://tile.stamen.com/terrain/2/2/1.png
```

```
## Source : http://tile.stamen.com/terrain/2/3/1.png
```

```
## Source : http://tile.stamen.com/terrain/2/0/2.png
```

```
## Source : http://tile.stamen.com/terrain/2/1/2.png
```

```
## Source : http://tile.stamen.com/terrain/2/2/2.png
```

```
## Source : http://tile.stamen.com/terrain/2/3/2.png
```

```r
# Plot the points on the map
ggmap(world) + # creates the map "background"
  geom_point(data = Starbucks, 
             aes(x = Longitude, 
                 y = Latitude,
                 color = `Ownership Type`), 
             alpha = .3, 
             size = .1) +
  theme_map() +
  theme(legend.background = element_blank())
```

```
## Warning: Removed 1 rows containing missing values (geom_point).
```

![](04_exercises_files/figure-html/unnamed-chunk-2-1.png)<!-- -->


  2. Construct a new map of Starbucks locations in the Twin Cities metro area (approximately the 5 county metro area).  


```r
twinCities <- get_stamenmap(
    bbox = c(left = -93.65, bottom = 44.66, right = -92.78, top = 45.26), 
    maptype = "terrain",
    zoom = 10)
```

```
## Source : http://tile.stamen.com/terrain/10/245/367.png
```

```
## Source : http://tile.stamen.com/terrain/10/246/367.png
```

```
## Source : http://tile.stamen.com/terrain/10/247/367.png
```

```
## Source : http://tile.stamen.com/terrain/10/248/367.png
```

```
## Source : http://tile.stamen.com/terrain/10/245/368.png
```

```
## Source : http://tile.stamen.com/terrain/10/246/368.png
```

```
## Source : http://tile.stamen.com/terrain/10/247/368.png
```

```
## Source : http://tile.stamen.com/terrain/10/248/368.png
```

```
## Source : http://tile.stamen.com/terrain/10/245/369.png
```

```
## Source : http://tile.stamen.com/terrain/10/246/369.png
```

```
## Source : http://tile.stamen.com/terrain/10/247/369.png
```

```
## Source : http://tile.stamen.com/terrain/10/248/369.png
```

```r
ggmap(twinCities) +
  geom_point(data = Starbucks, 
             aes(x = Longitude, y = Latitude),
             color = "blue",
             size = 0.8) +
  theme_map()
```

```
## Warning: Removed 25455 rows containing missing values (geom_point).
```

![](04_exercises_files/figure-html/unnamed-chunk-3-1.png)<!-- -->


  3. In the Twin Cities plot, play with the zoom number. What does it do?  (just describe what it does - don't actually include more than one map).  

The zoom number essentially controls how much detail is shown in the graph -- the higher the zoom, the more detail is showed on the map. As zoom decreases, the map becomes more zoomed in -- thus showing less detail than before. Because higher zoom values show much more detail, they tend to take a longer time to run and load. On the contrary, a lower zoom number will typically load faster than that of a higher one, since it is showing less detail on the map.


  4. Try a couple different map types (see `get_stamenmap()` in help and look at `maptype`). Include a map with one of the other map types.  
  

```r
twinCities_tonerlite <- get_stamenmap(
    bbox = c(left = -93.65, bottom = 44.66, right = -92.78, top = 45.26), 
    maptype = "toner-lite",
    zoom = 10)
```

```
## Source : http://tile.stamen.com/toner-lite/10/245/367.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/246/367.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/247/367.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/248/367.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/245/368.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/246/368.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/247/368.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/248/368.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/245/369.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/246/369.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/247/369.png
```

```
## Source : http://tile.stamen.com/toner-lite/10/248/369.png
```

```r
ggmap(twinCities) +
  geom_point(data = Starbucks, 
             aes(x = Longitude, y = Latitude),
             color = "blue",
             size = 0.8) +
  theme_map()
```

```
## Warning: Removed 25455 rows containing missing values (geom_point).
```

![](04_exercises_files/figure-html/unnamed-chunk-4-1.png)<!-- -->


  5. Add a point to the map that indicates Macalester College and label it appropriately. There are many ways you can do think, but I think it's easiest with the `annotate()` function (see `ggplot2` cheatsheet).
  

```r
twinCities <- get_stamenmap(
    bbox = c(left = -93.65, bottom = 44.66, right = -92.78, top = 45.26), 
    maptype = "terrain",
    zoom = 10)

ggmap(twinCities) +
   annotate(geom = "point",
            x = -93.1712321,
            y = 44.9378965,
            color = "orange",
            size = 2) +
  annotate(geom = "text",
            x = -93.1712321,
            y = 44.9378965,
            color = "cadetblue4",
            label = "Macalester College") +
  theme_map()
```

![](04_exercises_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


### Choropleth maps with Starbucks data (`geom_map()`)

The example I showed in the tutorial did not account for population of each state in the map. In the code below, a new variable is created, `starbucks_per_10000`, that gives the number of Starbucks per 10,000 people. It is in the `starbucks_with_2018_pop_est` dataset.


```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% #creates new dataset called census_pop_est_2018, reads_csv reads in the dataset being used.
  separate(state, into = c("dot","state"), extra = "merge") %>% #
  select(-dot) %>% 
  mutate(state = str_to_lower(state))
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   state = col_character(),
##   est_pop_2018 = col_double()
## )
```

```r
starbucks_with_2018_pop_est <-
  starbucks_us_by_state %>% 
  left_join(census_pop_est_2018,
            by = c("state_name" = "state")) %>% 
  mutate(starbucks_per_10000 = (n/est_pop_2018)*10000)
```


```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% #creates new dataset called census_pop_est_2018, reads_csv reads in the dataset being used.
  separate(state, into = c("dot","state"), extra = "merge") %>% #separates dot and state into two columns
  select(-dot) %>% # Gets rid of dot column
  mutate(state = str_to_lower(state)) # mutates state column so that they are all lowercase
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   state = col_character(),
##   est_pop_2018 = col_double()
## )
```

```r
census_pop_est_2018
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["state"],"name":[1],"type":["chr"],"align":["left"]},{"label":["est_pop_2018"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"alabama","2":"4887871"},{"1":"alaska","2":"737438"},{"1":"arizona","2":"7171646"},{"1":"arkansas","2":"3013825"},{"1":"california","2":"39557045"},{"1":"colorado","2":"5695564"},{"1":"connecticut","2":"3572665"},{"1":"delaware","2":"967171"},{"1":"district of columbia","2":"702455"},{"1":"florida","2":"21299325"},{"1":"georgia","2":"10519475"},{"1":"hawaii","2":"1420491"},{"1":"idaho","2":"1754208"},{"1":"illinois","2":"12741080"},{"1":"indiana","2":"6691878"},{"1":"iowa","2":"3156145"},{"1":"kansas","2":"2911505"},{"1":"kentucky","2":"4468402"},{"1":"louisiana","2":"4659978"},{"1":"maine","2":"1338404"},{"1":"maryland","2":"6042718"},{"1":"massachusetts","2":"6902149"},{"1":"michigan","2":"9995915"},{"1":"minnesota","2":"5611179"},{"1":"mississippi","2":"2986530"},{"1":"missouri","2":"6126452"},{"1":"montana","2":"1062305"},{"1":"nebraska","2":"1929268"},{"1":"nevada","2":"3034392"},{"1":"new hampshire","2":"1356458"},{"1":"new jersey","2":"8908520"},{"1":"new mexico","2":"2095428"},{"1":"new york","2":"19542209"},{"1":"north carolina","2":"10383620"},{"1":"north dakota","2":"760077"},{"1":"ohio","2":"11689442"},{"1":"oklahoma","2":"3943079"},{"1":"oregon","2":"4190713"},{"1":"pennsylvania","2":"12807060"},{"1":"rhode island","2":"1057315"},{"1":"south carolina","2":"5084127"},{"1":"south dakota","2":"882235"},{"1":"tennessee","2":"6770010"},{"1":"texas","2":"28701845"},{"1":"utah","2":"3161105"},{"1":"vermont","2":"626299"},{"1":"virginia","2":"8517685"},{"1":"washington","2":"7535591"},{"1":"west virginia","2":"1805832"},{"1":"wisconsin","2":"5813568"},{"1":"wyoming","2":"577737"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>


  6. **`dplyr` review**: Look through the code above and describe what each line of code does.

Commented in code above

  7. Create a choropleth map that shows the number of Starbucks per 10,000 people on a map of the US. Use a new fill color, add points for all Starbucks in the US (except Hawaii and Alaska), add an informative title for the plot, and include a caption that says who created the plot (you!). Make a conclusion about what you observe.
  

```r
states_map <- map_data("state")

starbucks_with_2018_pop_est %>% 
  # map that colors state by number of Starbucks
  ggplot() +
  geom_map(map = states_map,
           aes(map_id = state_name,
               fill = starbucks_per_10000)) +
  geom_point(data = Starbucks %>% filter(Country == "US", !(`State/Province`%in% c("AK", "HI"))), 
             aes(x = Longitude, y = Latitude),
             size = .05,
             alpha = .2, 
             color = "goldenrod") +
  #This assures the map looks decently nice:
  expand_limits(x = states_map$long, y = states_map$lat) + 
  theme_map() +
  theme(legend.background = element_blank()) +
  labs(title = "Locations of Starbucks per 10,000 People", 
       caption = "Created by Brian Lee",
       fill = "Locations/10K People") 
```

![](04_exercises_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
  
It seems that most Starbucks locations are concentrated on the coasts -- more so on the east coast, particularly in the northeast. We can also see that Starbucks locations seem to be scarcer in states that are known to be more rural, such as Montana, Wyoming, Idaho, Colorado, and Arizona.

### A few of your favorite things (`leaflet`)

  8. In this exercise, you are going to create a single map of some of your favorite places! The end result will be one map that satisfies the criteria below. 
  * Create a data set using the `tibble()` function that has 10-15 rows of your favorite places. The columns will be the name of the location, the latitude, the longitude, and a column that indicates if it is in your top 3 favorite locations or not. For an example of how to use `tibble()`, look at the `favorite_stp_by_lisa` I created in the data R code chunk at the beginning.  

  * Create a `leaflet` map that uses circles to indicate your favorite places. Label them with the name of the place. Choose the base map you like best. Color your 3 favorite places differently than the ones that are not in your top 3 (HINT: `colorFactor()`). Add a legend that explains what the colors mean.  
  
  * Connect all your locations together with a line in a meaningful way (you may need to order them differently in the original data).  
  
  * If there are other variables you want to add that could enhance your plot, do that now.  


```r
fav_places <- tibble(
  place = c("Macalester College", "Kyoto Sushi", "Feng Cha", 
            "Sushi Train", "Orchestra Hall", "Poke House & Tea Bar", 
            "Kims Asian Market", "Minehaha Falls",
            "Como Conservatory", "Walker Art Center", "K-Bop", "Mall of America"),
  lon = c(-93.16907460237587, -93.16086609865805, -93.23470920041346, 
           -93.27681974720282, -93.27493601427953, -93.16641688690099,
           -93.16729238877157, -93.21134406401353, -93.15446101760651,
           -93.28855284274243, -93.23674200226355, -93.24224698877565),
  lat = c(44.93802680674747, 45.035478143924095, 44.98054632654729, 
          44.97203857263388, 44.97231906204429, 44.92702650108423,
          44.961997100038815, 44.91666598055442, 44.9828768856244,
          44.96835671688722, 44.98206741131076, 44.85507803621259),
  top_3 = c("Macalester College" = FALSE, "Kyoto Sushi" = TRUE, 
                "Feng Cha" = TRUE, "Sushi Train" = FALSE,
                "Orchestra Hall" = TRUE, "Poke House & Tea Bar" = FALSE, "Kims Asian Market" = FALSE,
                "Minehaha Falls" = FALSE, "Como Conservatory" = FALSE, "Walker Art Center" = FALSE, "K-Bop" = FALSE, "Mall of America" = FALSE))
```


```r
fav_places
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["place"],"name":[1],"type":["chr"],"align":["left"]},{"label":["lon"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["lat"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["top_3"],"name":[4],"type":["lgl"],"align":["right"]}],"data":[{"1":"Macalester College","2":"-93.16907","3":"44.93803","4":"FALSE","_row":"Macalester College"},{"1":"Kyoto Sushi","2":"-93.16087","3":"45.03548","4":"TRUE","_row":"Kyoto Sushi"},{"1":"Feng Cha","2":"-93.23471","3":"44.98055","4":"TRUE","_row":"Feng Cha"},{"1":"Sushi Train","2":"-93.27682","3":"44.97204","4":"FALSE","_row":"Sushi Train"},{"1":"Orchestra Hall","2":"-93.27494","3":"44.97232","4":"TRUE","_row":"Orchestra Hall"},{"1":"Poke House & Tea Bar","2":"-93.16642","3":"44.92703","4":"FALSE","_row":"Poke House & Tea Bar"},{"1":"Kims Asian Market","2":"-93.16729","3":"44.96200","4":"FALSE","_row":"Kims Asian Market"},{"1":"Minehaha Falls","2":"-93.21134","3":"44.91667","4":"FALSE","_row":"Minehaha Falls"},{"1":"Como Conservatory","2":"-93.15446","3":"44.98288","4":"FALSE","_row":"Como Conservatory"},{"1":"Walker Art Center","2":"-93.28855","3":"44.96836","4":"FALSE","_row":"Walker Art Center"},{"1":"K-Bop","2":"-93.23674","3":"44.98207","4":"FALSE","_row":"K-Bop"},{"1":"Mall of America","2":"-93.24225","3":"44.85508","4":"FALSE","_row":"Mall of America"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
pal_fav <- colorFactor("viridis",
                         domain = fav_places$top_3)

leaflet(data = fav_places) %>% 
  addProviderTiles(providers$CartoDB.DarkMatter) %>% # made darker so we can see the points better
  addCircles(lng = ~lon, 
             lat = ~lat, 
             label = ~place,
              weight = 5, 
             opacity = 1,
             radius = 10,
             color = ~pal_fav(top_3)) %>% 
   addPolylines(lng = ~lon, 
               lat = ~lat,
               color = col2hex("pink"))
```

<!--html_preserve--><div id="htmlwidget-c461d094e686bc0c8848" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-c461d094e686bc0c8848">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addProviderTiles","args":["CartoDB.DarkMatter",null,null,{"errorTileUrl":"","noWrap":false,"detectRetina":false}]},{"method":"addCircles","args":[[44.9380268067475,45.0354781439241,44.9805463265473,44.9720385726339,44.9723190620443,44.9270265010842,44.9619971000388,44.9166659805544,44.9828768856244,44.9683567168872,44.9820674113108,44.8550780362126],[-93.1690746023759,-93.160866098658,-93.2347092004135,-93.2768197472028,-93.2749360142795,-93.166416886901,-93.1672923887716,-93.2113440640135,-93.1544610176065,-93.2885528427424,-93.2367420022636,-93.2422469887756],10,null,null,{"interactive":true,"className":"","stroke":true,"color":["#440154","#FDE725","#FDE725","#440154","#FDE725","#440154","#440154","#440154","#440154","#440154","#440154","#440154"],"weight":5,"opacity":1,"fill":true,"fillColor":["#440154","#FDE725","#FDE725","#440154","#FDE725","#440154","#440154","#440154","#440154","#440154","#440154","#440154"],"fillOpacity":0.2},null,null,["Macalester College","Kyoto Sushi","Feng Cha","Sushi Train","Orchestra Hall","Poke House &amp; Tea Bar","Kims Asian Market","Minehaha Falls","Como Conservatory","Walker Art Center","K-Bop","Mall of America"],{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null,null]},{"method":"addPolylines","args":[[[[{"lng":[-93.1690746023759,-93.160866098658,-93.2347092004135,-93.2768197472028,-93.2749360142795,-93.166416886901,-93.1672923887716,-93.2113440640135,-93.1544610176065,-93.2885528427424,-93.2367420022636,-93.2422469887756],"lat":[44.9380268067475,45.0354781439241,44.9805463265473,44.9720385726339,44.9723190620443,44.9270265010842,44.9619971000388,44.9166659805544,44.9828768856244,44.9683567168872,44.9820674113108,44.8550780362126]}]]],null,null,{"interactive":true,"className":"","stroke":true,"color":"#FFC0CB","weight":5,"opacity":0.5,"fill":false,"fillColor":"#FFC0CB","fillOpacity":0.2,"smoothFactor":1,"noClip":false},null,null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]}],"limits":{"lat":[44.8550780362126,45.0354781439241],"lng":[-93.2885528427424,-93.1544610176065]}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


## Revisiting old datasets

This section will revisit some datasets we have used previously and bring in a mapping component. 

### Bicycle-Use Patterns

The data come from Washington, DC and cover the last quarter of 2014.

Two data tables are available:

- `Trips` contains records of individual rentals
- `Stations` gives the locations of the bike rental stations

Here is the code to read in the data. We do this a little differently than usualy, which is why it is included here rather than at the top of this file. To avoid repeatedly re-reading the files, start the data import chunk with `{r cache = TRUE}` rather than the usual `{r}`. This code reads in the large dataset right away.


```r
data_site <- 
  "https://www.macalester.edu/~dshuman1/data/112/2014-Q4-Trips-History-Data.rds" 
Trips <- readRDS(gzcon(url(data_site)))
Stations<-read_csv("http://www.macalester.edu/~dshuman1/data/112/DC-Stations.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   name = col_character(),
##   lat = col_double(),
##   long = col_double(),
##   nbBikes = col_double(),
##   nbEmptyDocks = col_double()
## )
```

  9. Use the latitude and longitude variables in `Stations` to make a visualization of the total number of departures from each station in the `Trips` data. Use either color or size to show the variation in number of departures. This time, plot the points on top of a map. Use any of the mapping tools you'd like.
  

  
  10. Only 14.4% of the trips in our data are carried out by casual users. Create a plot that shows which area(s) have stations with a much higher percentage of departures by casual users. What patterns do you notice? Also plot this on top of a map. I think it will be more clear what the patterns are.
  

  
### COVID-19 data

The following exercises will use the COVID-19 data from the NYT.

  11. Create a map that colors the states by the most recent cumulative number of COVID-19 cases (remember, these data report cumulative numbers so you don't need to compute that). Describe what you see. What is the problem with this map?
  
  12. Now add the population of each state to the dataset and color the states by most recent cumulative cases/10,000 people. See the code for doing this with the Starbucks data. You will need to make some modifications. 
  
  13. **CHALLENGE** Choose 4 dates spread over the time period of the data and create the same map as in exercise 12 for each of the dates. Display the four graphs together using faceting. What do you notice?
  
## Minneapolis police stops

These exercises use the datasets `MplsStops` and `MplsDemo` from the `carData` library. Search for them in Help to find out more information.

  14. Use the `MplsStops` dataset to find out how many stops there were for each neighborhood and the proportion of stops that were for a suspicious vehicle or person. Sort the results from most to least number of stops. Save this as a dataset called `mpls_suspicious` and display the table.  
  
  15. Use a `leaflet` map and the `MplsStops` dataset to display each of the stops on a map as a small point. Color the points differently depending on whether they were for suspicious vehicle/person or a traffic stop (the `problem` variable). HINTS: use `addCircleMarkers`, set `stroke = FAlSE`, use `colorFactor()` to create a palette.  
  
  16. Save the folder from moodle called Minneapolis_Neighborhoods into your project/repository folder for this assignment. Make sure the folder is called Minneapolis_Neighborhoods. Use the code below to read in the data and make sure to **delete the `eval=FALSE`**. Although it looks like it only links to the .sph file, you need the entire folder of files to create the `mpls_nbhd` data set. These data contain information about the geometries of the Minneapolis neighborhoods. Using the `mpls_nbhd` dataset as the base file, join the `mpls_suspicious` and `MplsDemo` datasets to it by neighborhood (careful, they are named different things in the different files). Call this new dataset `mpls_all`.


```r
mpls_nbhd <- st_read("Minneapolis_Neighborhoods/Minneapolis_Neighborhoods.shp", quiet = TRUE)
```

  17. Use `leaflet` to create a map from the `mpls_all` data that colors the neighborhoods by `prop_suspicious`. Display the neighborhood name as you scroll over it. Describe what you observe in the map.
  
  18. Use `leaflet` to create a map of your own choosing. Come up with a question you want to try to answer and use the map to help answer that question. Describe what your map shows. 
  
  
## GitHub link

  19. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 04_exercises.Rmd, provide a link to the 04_exercises.md file, which is the one that will be most readable on GitHub.


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
