---
layout: post
title: "Mapping NAD83 Projection Maps With GeoDjango"
description: ""
category: programming
tags: [mapping, geodjango, projections, gis]
---
Placing shapes on a map is pretty straight-forward thanks to fantastic libraries like [Leaflet.js](http://leafletjs.com/examples/quick-start/example-overlays.html).
However, on one of my recent projects I needed to take maps that were using
NAD83 projections and translate them into usable [GeoJSON](http://geojson.org/).
Most mapping libaries used on the web use a more generic projection, WGS84, and
will not support drawing shapes using an alternative projection (like NAD83).

There are few tools better than
[GeoDjango](https://docs.djangoproject.com/en/1.10/ref/contrib/gis/) and
[PostGIS](http://postgis.net/) for building maps into web applications. I wanted
to use these tools to make the transformation.

If you search for "translating NAD83 to WGS84" you're going to find all sorts of
intimidating information (like [this whitepaper from
NOAA](https://www.ngs.noaa.gov/CORS/Articles/WGS84NAD83.pdf)). For a non-GIS
specialist like myself, this can be quite alarming. Fortunately, GeoDjango and
PostGIS have our back.

First, you'll need to get GeoDjango and PostGIS up and running. That's not in
the scope of this article, and there are plenty of wonderful tutorials on how to
do that so I will leave that as an exercise to the reader.

First, you need to get the SRID (also known as the EPSG) for the data you want
to map. You can get information about the file by inspecting it on the command
line with a tool like `ogrinfo` or using GeoDjango's `DataSource` class.

```
$ ogr2info path/to/filename.shp filename -so
```

```
$ ./manage.py shell
Python 3.5.2+ (default, Sep 22 2016, 12:18:14) 
Type "copyright", "credits" or "license" for more information.

IPython 5.1.0 -- An enhanced Interactive Python.
?         -> Introduction and overview of IPython's features.
%quickref -> Quick reference.
help      -> Python's own help system.
object?   -> Details about 'object', use 'object??' for extra details.

In [1]: import os

In [2]: shp = os.path.abspath('/path/to/filename.shp')

In [3]: from django.contrib.gis.gdal import DataSource

In [4]: ds = DataSource(shp)

In [5]: layer = ds[0]

In [6]: layer.srs
Out[6]: <django.contrib.gis.gdal.srs.SpatialReference at 0x7f949428a8d0>

In [7]: print(layer.srs)
```

Either way you choose to do it, you will see something like this:

```
PROJCS["NAD_1983_UTM_Zone_16N",
    GEOGCS["GCS_North_American_1983",
        DATUM["North_American_Datum_1983",
            SPHEROID["GRS_1980",6378137,298.257222101]],
        PRIMEM["Greenwich",0],
        UNIT["Degree",0.017453292519943295]],
    PROJECTION["Transverse_Mercator"],
    PARAMETER["latitude_of_origin",0],
    PARAMETER["central_meridian",-87],
    PARAMETER["scale_factor",0.9996],
    PARAMETER["false_easting",500000],
    PARAMETER["false_northing",0],
    UNIT["Meter",1]]
```

The part you want is that first line: `NAD_1983_UTM_Zone_16N`. Google that,
and you should be able to find a page like [this one on
spatialreference.org](http://spatialreference.org/ref/epsg/nad83-utm-zone-16n/).

Note that in this case, the SRID / EPSG is 26916. When you create a database
column in GeoDjango, you'll either need to translate this to WGS84 or you'll
need to indicate that the data is stored with `srid=26916`.

If you choose to store it in the original format, your model attribute will
look something like:

```
class Foobar(models.Model):
    geom = models.MultiPolygon(srid=26916)
    name = models.CharField(max_length=32)
```

To convert `Foobar.geom` to GeoJSON, you can use the [GeoDjango
`serializer`](https://docs.djangoproject.com/en/1.10/ref/contrib/gis/serializers/):

```
serialize('geojson', Foobar.objects.filter(name='Cookies'),
    geometry_field='geom',
    fields=('name',))
```

This will output a nice GeoJSON document that is projected in WGS84, useful for
showing on the web with a tool like Leaflet.js. Note that we did not need to
even provide the `srid` parameter here.
