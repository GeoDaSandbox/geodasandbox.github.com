---
layout: post
title: "Easy point-in-polygon from shapefiles"
description: ""
category: darribas 
tags: [pandas, pysal, geo_tools]
author: dani
---
{% include JB/setup %}

All of a sudden, I was in need to perform a point in polygon operation to find
out in which polygon a bunch of point locations (both stored in a shapefile)
could be found, if any. This is a [well known problem](http://en.wikipedia.org/wiki/Point_in_polygon) and has well-known solutions (e.g. ArcGIS or QGIS). But this time I didn't have the costly Arc at hand and for the problem I'm facing (around 60k points and +800 polygons) QGIS wouldn't work in a reasonable time span. Plus, it would be nice to be able to leave a *code trace* in the form of a script that I could check 6 months down the road when I need to refresh my memory about what I did.

Luckily, [PySAL](http://pysal.org) has nice functionality to check whether a
point is within a polygon or not, so all I had to do basically is to writie a
wrapper function that takes the core functionality from PySAL and presents it
to an end-user in an easy way for this particular task. It turns out I wrote
not one function but two, `pip_shps` and `pip_shps_multi`. The first one uses
[pandas](http://pandas.pydata.org) and, based on my limited experiments, is
a little faster on one core. For some reason, it is a bit harder given my
limited expertise to parallelize it, so I wrote another one that uses the
'rtree' in PySAL and works on several cores. The API and functionality is the
same, so you pick your flavour depending on whether you have one very fast
core or many not that fast ones. The [code](https://github.com/GeoDaSandbox/sandbox/blob/master/pyGDsandbox/geo_tools.py) is documented so it should be self-explaining, but just to give you a very easy example, here's how you would typically find out whether any of the points in `pts.shp` is within any of the polygons of `polys.shp`:

    {% highlight python %}
    from pyGDsandbox.geo_tools import pip_shps, pip_shps_multi
    correspondences = pip_shps('pts.shp', 'polys.shp', polyID_col='polyIDcolumn')
    correspondences_multi = pip_shps_multi('pts.shp', 'polys.shp')
    {% endhighlight %}

where `polyIDcolumn` is the name of the column in the dbf for `polys.shp`. If
you leave that blank, it'll give back only the position of the polygon (e.g.
the 3rd one in the dbf). Please have a look at the code, play with it and have
fun. Of course, any comment or suggestion is more than welcome.

Ps. Big thanks to [@sergerey](http://twitter.com/sergerey) and
[@schmidtc](http://twitter.com/schmidtc) for pointing me to the rtree
functionality in PySAL and other additional help.

