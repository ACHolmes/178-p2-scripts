
# Understanding the data

#### Notes

I recommend installing the `Prettify JSON` extension for VSCode, use the command palette and run `Prettify JSON` if your JSON looks horrific. If it doesn't work, my first guess is you (or I) changed something so that pandas NaNs or other invalid JSON slipped through so it doesn't know what to do.

## Andrew's route-orientated data

Anything in `out/route_orientated` is designed to make the data easy to access and think about when working kinda 'route-orientated'. That is, if I know which route I'm interested in, I can quickly find stuff for that route. I could, for example, quickly find how to draw the route, or info about the trips running on this route on this day. I could not, for example, quickly find: 'what are the next 3 buses arriving at the quad stop?` - that would require looking through all the routes, i.e. basically the entire JSON file. I'll try to make a 'stop-orientated' version of this soon.

Here is the current rough 'schema' of what one entry in the JSON looks like (i.e. the data for one route), using the 1636'er as an example:

## With Andrew's annotations
```JSON
"route_id": 777,
"route_short_name": "1636",
"route_long_name": "1636'er",
"route_color": "0099FF",
"route_text_color": "FFFFFF",

-> Shapes stores info about every 'shape' or actual route/trace of points that this route covers. Most routes are 1:1 with shapes - the HUIT 'route' apparently travels two different shapes depending on the time, hence why 'shapes' not 'shape' and having to be able to store multiple shapes
"shapes": {
  "48686": {
    -> points stores all the points to draw on the map to display this route.
    "points": [
      {
        "shape_pt_lat": 42.381867,
        "shape_pt_lon": -71.125325,
        "shape_pt_sequence": 1
      },
      {
        "shape_pt_lat": 42.380436,
        "shape_pt_lon": -71.12435,
        "shape_pt_sequence": 2
      },
      ...
    ]
  }
}
-> trips stores all info about every trip that runs on that route.
"trips": {
  -> Idenitified by 'trip_id'
  "670294": {
    'service_id' aligns with calendar stuff. There's the weekday 'day' service, the weekday 'evening service', everyday overnight service and so on.
    "service_id": 48686.126106,
    "trip_id": 670294,
    "trip_headsign": "",
    "trip_short_name": "",
    -> The shape that this trip travels, in case the route has multiple shapes
    "shape_id": 48686,
    "stops": [
      -> Info about all the stops this trip will hit
      {
        "arrival_time": "16:30:00",
        "departure_time": "16:30:00",
        "stop_id": 5049,
        "stop_sequence": 1,
        "stop_code": 5049,
        "stop_name": "Quad",
        "stop_lat": 42.381867,
        "stop_lon": -71.125325
      },
      ...
    ],
    -> Which days does this trip operate.
    "days": [
      "saturday",
      "sunday"
    ]
  },
  ... lots more trips for this route probably
}
```

## Plain

```JSON
"route_id": 777,
"route_short_name": "1636",
"route_long_name": "1636'er",
"route_color": "0099FF",
"route_text_color": "FFFFFF",
"shapes": {
  "48686": {
    "points": [
      {
        "shape_pt_lat": 42.381867,
        "shape_pt_lon": -71.125325,
        "shape_pt_sequence": 1
      },
      {
        "shape_pt_lat": 42.380436,
        "shape_pt_lon": -71.12435,
        "shape_pt_sequence": 2
      },
      ...
    ]
  }
}
"trips": {
  "670294": {
    "service_id": 48686.126106,
    "trip_id": 670294,
    "trip_headsign": "",
    "trip_short_name": "",
    "shape_id": 48686,
    "stops": [
      {
        "arrival_time": "16:30:00",
        "departure_time": "16:30:00",
        "stop_id": 5049,
        "stop_sequence": 1,
        "stop_code": 5049,
        "stop_name": "Quad",
        "stop_lat": 42.381867,
        "stop_lon": -71.125325
      },
      ...
    ],
    "days": [
      "saturday",
      "sunday"
    ]
  },
  ...
}
```


