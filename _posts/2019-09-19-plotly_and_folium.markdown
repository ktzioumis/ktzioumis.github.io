---
layout: post
title:      "Plotly and Folium"
date:       2019-09-19 22:23:50 -0400
permalink:  plotly_and_folium
---


During a recent project based on [New York City Restaurants](https://github.com/ktzioumis/New-York-Restaurant-Guide) I wanted to create some maps. It seemed to me like a useful thing to have on hand when talking about a city and they were very illustrative.The project ended up incorporating three choropleth maps based around New York Community Board Districts:
- Density of restaurants
- Most popular types of restaurants, 
- Average health department inspection scores,

All of these maps are made using the Folium library and I think they came out great. But there was one more map that I made but I didn't end up using - Year on year changes in health dept inspection score averages. For a few reasons, including the overall sprawl over the project at this point, I did not end including an analysis of time as a influencing factor on health department inspection scoring and grading. It was just as well because as much as I liked the idea behind that map, there were a few little nitpicking things I didn't like about the the way it turned out.

You can view and interact with it here: [https://ktzioumis.github.io/plotly-folium/m_ave_yronyr.html](https://ktzioumis.github.io/plotly-folium/m_ave_yronyr.html)

The map displays the annual average health inspection score for each Community Board area for the years 2016 (from july),  2017,2018 & 2019 (to july). Each year can be selescted or deselected as an overlay for the OpenStreetMap. The map as it is linked above is functional and illustrates the data well but my quibbles are as follows:

- Selecting between chorpleth maps does not unselect the other choropleths - makes it difficult to see changes from one map to the next, since they will either be overlayed as one is selected and the other deselected or the map goes blank in between selections
- The colorbar for each choropleth is permanently displayed regardless of whether that choropleth is turned on

Folium does not support a method to resolve either of these problems.

I no longer *needed* to make this map but I still *wanted* to able to make this map. The shortcomings of Folium were disappoing so I wanted to try out another plotting/mapping library - Plotly.

[Plotly Choropleth tutuorial](https://plot.ly/python/mapbox-county-choropleth/)

The choropleth tutorial is based on unemployment data for US counties and I used it as a starting point to make a layered choropleth map the way I wanted it to look. 

The process of creating a dropdown menu for choropleth selection I have adapted from [this tutorial](https://plot.ly/~empet/15237/choroplethmapbox-with-dropdown-menu/#/)

[github jupyter notebook](https://github.com/ktzioumis/plotly-folium/blob/master/Plotly_unemp_choro.ipynb)

Animated gif of the result: 

![](https://github.com/ktzioumis/plotly-folium/blob/master/ezgif-3-34e50aa5d99d.gif?raw=true)

I love this result! And it addresses both my problems directly.
- The dropdown allows for selection of choropleth that is tuned to set the visibility of the other choroploeth (A third option in the dropdown could be set to have both the choropleths visible should it be required).
- The colorbar displays only the scale for the selected choropleth.

As a bonus because the colorbar is offset from the map to the right, the text for the xticks and label on the legend are not displayed in front of the map and are much more legible as a result. Folium does not allows for the legend position on the choropleth to be changed.

Definitely a win for Plotly


