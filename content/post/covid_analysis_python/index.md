---
title: Animated Covid 19 analysis using Python
subtitle: Using Plotly's chloropeth graphs and generic python graphing to visualize Covid 19 infection and death rates and the impact of lockdown in various countries.
# Date published
#date: "2021-07-20T00:00:00Z"
date: "2021-07-20"

# Date updated
#lastmod: "2021-07-20T00:00:00Z"

readingTime: ten

# Show this page in the Featured widget?
featured: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Covid 19 Analysis'
  focal_point: ""
  placement: 2
  preview_only: true
---

<!-- <iframe
       src="./ch001.html"
       width="90%"
       height="1000px"
       style="border:none;">
 </iframe> -->

 ### Covid 19 analysis using Python

# Code:
```python
fig = px.choropleth(dfconf, locations='Country', locationmode='country names', color='Confirmed', animation_frame='Date')
fig.layout.updatemenus[0].buttons[0].args[1]['frame']['duration'] = 30
fig.layout.updatemenus[0].buttons[0].args[1]['transition']['duration'] = 5
fig.update_geos(projection_type="equirectangular", visible=True, resolution=50)
fig.update_layout(
    title_text = 'Global Spread of Coronavirus',
    title_x = 0.5,
    geo=dict(
        showframe = False,
        showcoastlines = False,
    ))
#fig.show()
iplot(fig,show_link=False)
pio.write_json(fig,"file001.json",engine="json")
fig.write_html("plot001.html")
```

 # Chart 1:
 <!-- {{< chart data="file001" >}} -->
 <iframe
       src="https://github.com/saif-sayeed/resume-demo/blob/master/content/post/covid_analysis_python/ch001.html"
       width="90%"
       height="500px"
       style="border:none;">
 </iframe>