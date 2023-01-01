The idea is very simple and I have had it for years - I even presented at current workplaces. You build, maintain, and expose ephemeral data related to the outdoors. Urban location are flooded with information related to their current* status or use. From traffic information to construction and locations being open, the urban world is visible to users in real time. 

The outdoors is not. Safe, planned, expected information should be available just like for urban areas but about the outdoors. Business, closures or the status of trails can help with planning, safety, efficiency and sustainability.

The Open Outdoor Network (OON) will be a place for users and apps to create and inspect observations made by the community relating to the outdoor world - trails, outdoors POIs, viewpoints, etc. 

## Core object: The observation
An observation has the following properties:
- Spatial: Relates to a location or area on Earth(point, line or polygon)
- Temporal: Relates to a specific time
- Ephemeral: It does not last long - it expires
- Informational: It **must** represent information about the area that would be considered "reasonably useful" by others. This would include traffic, hazards, positive information like a water fill-up. Observation information **should not** relate solely to a user personal experience only (i.e. - "My favorite tree on the hike was here")
- Accountable: Observation **must** have an accountable party. Whether observations get added manually or through automation, they will need to be associated with an accountable party. The reason this is important is so that accounts in the future can be penalized or rewarded based on the quality and accuracy of the information provided. 

## The API
One of the backbones of the OON will be the ability for others to ingest and add to the network. Access to the network will be based on a Freemium model. API calls to create observations on the network will be free but calls to observe the network at large will cost money at some point (maybe after a certain number of calls). This should allow apps to help contribute while still being able to make money. 

With the core dataset, we can also use the observations passively to decorate other information. Imagine a user planning to do a hike, an app could call the OON to inspect current, non-expired observation that the user might encounter with this plan. This might include but is not limited to, reported hazards nearby, animal spotting, conditions reports, etc. 

## The App
In order to built a critical mass of information, the main OON will need to be accompanied by a web app and/or mobile app. All actions through the main applications (create and read) will be free to all users to join the network and contribute without paying. The easiest way to make money from the venture will be via an API into the network after critical mass.