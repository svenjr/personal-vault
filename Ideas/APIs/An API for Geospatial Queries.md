I have an inkling of an idea about how there are many times where I wish to perform geospatial functions - like from PostGIS - but do not want to have a local DB call to do it but maybe I also don't want to use GDAL or PostGIS APIs to call the functions either. I want to keep things ultralight for my service. 

It would be an interesting idea to create a paid API but for geospatial power. For example, calling out to the web (this API) with a key, to perform geospatial functions with given information. Maybe something like

```shell
curl -X POST "https://the-geo-api/st_intersect" -d '{"point1": "12.5 46.3", ...}'
```

I am not even really sure anyone would want that. But what people might be willing to pay for is to also have data access. That would mean that you could obtain things like high def elevation and gradient profiles for a line or point. This would require either a finanial investment or working closely with a company who has the data. At first, I could tap into a public data source for the best free data I could find.

## Possible API Capabilities

- Elevation API
- Line simplification
- Data decoration (given a line, attach other data about it - maybe using OSM) - this could be a really nice one because it requires quite a bit of data
- 