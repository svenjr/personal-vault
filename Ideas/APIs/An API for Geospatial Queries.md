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

## Work

There is a lot of extra work that goes along with this than just creating a great backend service. I would need some frontend work as well for explaining the capabilities as well as for API setup for customers.

I would build the backend backbone as a Go service with a GraphQL API facing outward for users. I would also build a totally separate repo for the website - not sure what technology to use here as it would be my first time doing anything in the frontend. The other question might be to also control users in a separate micro-service instead of attaching it to the Go part - this part should be as fast and light as possible for performance.

If I take the micro-service path, using a federated graph with a [Apollo Router](https://www.apollographql.com/docs/router/) maybe. This means I could extend the graph for internal and external use. However, if the main business model is an API, it might be worth considering using an external and internal graph. That means there is a specific graph dedicated for customers.

That means, the work generally looks like:

- **Geoprocessing Service**: Go service to do all of the geoprocessing (either via a DB or ideally through a Go package)
- **User's Service**: Go service or Firebase to control user signup - preferably not Firebase since it does not work really well for machine-to-machine (M2M). The main goal for this is to be able to have customers pay for an API so OAuth2 might be the best route
- **Frontend Web App**: To showcase the tool/API and to market it
- A [Kubernetes](https://kubernetes.io/) (or [K3S](https://docs.k3s.io/)) cluster to host everything via AWS or Linode or something

It looks like I can get most of this up privately on Github with no cost. Cost only starts to come in with 

Domain:
- I have registered geo-get.xyz with Google Domains as of Dec 30, 2022 for $12 for the year. I would love to start building this this year with this domain.

## Define the Product - What will it do?
This is arguably the hardest part. What will the service do and why will that drive people to use it? My original idea is simple: abstract the computation, effort, and expertise away from users for geospatial tasks. Geospatial data is used all over web and mobile products that could be improved for their users, but it is a big investment to want to go in and control all of those tasks yourself. Imagine a user draws or inserts a line to your app for some reason, the app could then simply call geo-get.xyz/something with the line data and receive all sorts of information and statistics back. Which areas does the line cross, what is the true geodesic distance, what is Euclidian distance from start to end (signifying also if it is a loop), etc. 

I think geo data should be more utilized and more featured for people who want it. Points can get geocoded or given accurate elevation information or even weather using extended APIs. The main idea behind my product is if you have information that can be referenced to a place on Earth, I want you to use my API to decorate it.

### Functionality
- Line information - given a line, get information about the line back (length, elevation profile, etc)
- Point information - given a point, get information about the point back (weather, currency, elevation, polygons it falls within like property lines) 
- Polygon information - given a polygon, get information about the polygon back (area, if it intersects or falls within other public polygons, etc)
- Intersection - given two objects, do they intersect (or two subsets of data and ask if any object from one group intersects any from the other)