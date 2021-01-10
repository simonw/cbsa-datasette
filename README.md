# cbsa-datasette

https://cbsa.datasettes.com/ - provides [an API](https://cbsa.datasettes.com/core/by_lat_lon) for looking up [core-based statistical areas](https://en.wikipedia.org/wiki/Core-based_statistical_area) based on a latitude/longitude point.

More details: [cbsa-datasette in my Weeknotes](https://simonwillison.net/2021/Jan/10/weeknotes/#cbsa-datasette)

## Running this locally

Download the shapefile from [Bureau of Transportation Stastics: Core Based Statistical Areas](https://data-usdot.opendata.arcgis.com/datasets/b0d0e777e2ad4b53803dbc0527c73d88_0):

    wget https://opendata.arcgis.com/datasets/b0d0e777e2ad4b53803dbc0527c73d88_0.zip

Install [shapefile-to-sqlite](https://datasette.io/tools/shapefile-to-sqlite) and [SpatiaLite](https://docs.datasette.io/en/stable/spatialite.html#installation) and run this command:

    shapefile-to-sqlite core.db b0d0e777e2ad4b53803dbc0527c73d88_0.zip \
        --table Core_Based_Statistical_Areas \
        --spatial-index

This will produce `core.db` containing a `Core_Based_Statistical_Areas` SpatiaLite table plus spatial indexes.

Run this command to browse it with Datasette:

    datasette -m metadata.yml core.db
