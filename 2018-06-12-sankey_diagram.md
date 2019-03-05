---
layout: post
title: Sankey Diagram
tags:
- visualisation
- Sankey Diagram
excerpt_separator: <!--more-->

---

Sankey diagrams are useful to visualize flows. Here are some tools to plot them.

# Plotly

[Plotly](https://plot.ly/python/sankey-diagram/) has more features, however you need to get an account to create diagrams (limited to 15 for free). The documentation could be clearer...

<iframe width="500" height="500" frameborder="0" scrolling="no" src="//plot.ly/~arthur.gaudron/22.embed"></iframe>

# IPython Sankey diagram widget

[Ipysankeywidget](https://github.com/ricklupton/ipysankeywidget) does the job. It would be even better if the values can be plotted. The interactive example in the tutorials is interesting.

![Sankey with Ipysankeywidget](/img/sankey_ipyw.png)

# Holoviews

[Holoviews](http://holoviews.org/reference/elements/bokeh/Sankey.html) is library to use bokeh/matplotlib at a higher level. More information compared to the previous one. However I couldn't figure out how to export it as an html file (as you can do with bokeh objects).

![Sankey with Holoviews](/img/sankey_bokeh.png)
