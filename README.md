# Instants and Intervals for event-like GeoJSON features

Extends [RFC 7649](https://tools.ietf.org/html/rfc7946) GeoJSON with
instants and intervals of time

## In a nutshell

- Defines a "when" member analogous to GeoJSON's existing "geometry".
- Defines two types of temporal objects: "Instant" and "Interval".
- Values of these objects are ISO-8601 or RFC 3339 date/time strings.

The "when" object describes the temporal extent of a feature in the same sense
that a GeoJSON "geometry" object describes its spatial extent. A common
representation of time allows us to more readily mix GeoJSON from different
sources in spatio-temporal visualizations.

## Hypothetical examples

### Instantaneous event-like feature

For a thing that exists at a certain time.

```json
{
  "geometry": {
    "coordinates": [
      0.0,
      0.0
    ],
    "type": "Point"
  },
  "id": "1",
  "properties": {"foo": "bar"},
  "type": "Feature",
  "when": {
    "start": "2014-04-24",
    "type": "Instant"
  }
}
```

### Non-instaneous event-like feature

For a thing that exists during a certain interval.

```json
{
  "geometry": {
    "coordinates": [
      0.0,
      0.0
    ],
    "type": "Point"
  },
  "id": "1",
  "properties": {"foo": "bar"},
  "type": "Feature",
  "when": {
    "start": "2014-04-24",
    "end": "2014-04-25",
    "type": "Interval"
  }
}
```

### Open-ended event-like feature

For a thing that exists *since* a certain time.

```json
{
  "geometry": {
    "coordinates": [
      0.0,
      0.0
    ],
    "type": "Point"
  },
  "id": "1", 
  "properties": {"foo": "bar"},
  "type": "Feature",
  "when": {
    "type": "Interval",
    "start": "2014-04-24"
  }
}
```

## Real world example

The USGS publishes [GeoJSON feeds of recent earthquake
data](http://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php). These
feeds record the time of earthquake events in a manner unique to these feeds
(milliseconds since the epoch). Below is an example of the [Past 7 Days
Significant
Earthquakes](http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/significant_week.geojson),
retrieved 2016-08-14, converted to use geojson-events instants.

```json
{
  "type": "FeatureCollection", 
  "features": [
    {
      "geometry": {
        "type": "Point", 
        "coordinates": [
          173.1114, 
          -22.4953, 
          9.95
        ]
      }, 
      "when": {
        "type": "Instant", 
        "start": "2016-08-12T01:26:35.140000+00:00"
      }, 
      "type": "Feature", 
      "properties": {
        "rms": 0.94, 
        "code": "10006d5h", 
        "cdi": 6.2, 
        "sources": ",pt,at,us,gcmt,", 
        "nst": null, 
        "tz": 720, 
        "title": "M 7.2 - 109km E of Ile Hunter, New Caledonia", 
        "magType": "mww", 
        "detail": "http://earthquake.usgs.gov/earthquakes/feed/v1.0/detail/us10006d5h.geojson", 
        "sig": 799, 
        "net": "us", 
        "type": "earthquake", 
        "status": "reviewed", 
        "updated": 1471043352566, 
        "felt": 2, 
        "alert": "green", 
        "dmin": 4.822, 
        "mag": 7.2, 
        "gap": 21, 
        "types": ",cap,dyfi,finite-fault,general-link,general-text,geoserve,impact-link,losspager,moment-tensor,origin,phase-data,poster,shakemap,", 
        "url": "http://earthquake.usgs.gov/earthquakes/eventpage/us10006d5h", 
        "ids": ",pt16225050,at00obrw0f,us10006d5h,gcmt20160812012635,", 
        "tsunami": 1, 
        "place": "109km E of Ile Hunter, New Caledonia", 
        "time": 1470965195140, 
        "mmi": 0
      }, 
      "id": "us10006d5h"
    }, 
    {
      "geometry": {
        "type": "Point", 
        "coordinates": [
          -122.8018333, 
          39.3293333, 
          14.45
        ]
      }, 
      "when": {
        "type": "Instant", 
        "start": "2016-08-10T02:57:17.510000+00:00"
      }, 
      "type": "Feature", 
      "properties": {
        "rms": 0.15, 
        "code": "72672610", 
        "cdi": 5, 
        "sources": ",at,nc,us,", 
        "nst": 120, 
        "tz": -420, 
        "title": "M 5.1 - 19km NNE of Upper Lake, California", 
        "magType": "mw", 
        "detail": "http://earthquake.usgs.gov/earthquakes/feed/v1.0/detail/nc72672610.geojson", 
        "sig": 899, 
        "net": "nc", 
        "type": "earthquake", 
        "status": "reviewed", 
        "updated": 1471176057699, 
        "felt": 1062, 
        "alert": "green", 
        "dmin": 0.155, 
        "mag": 5.09, 
        "gap": 32, 
        "types": ",cap,dyfi,focal-mechanism,general-link,geoserve,impact-link,losspager,moment-tensor,nearby-cities,origin,phase-data,scitech-link,shakemap,", 
        "url": "http://earthquake.usgs.gov/earthquakes/eventpage/nc72672610", 
        "ids": ",at00oboavh,nc72672610,us10006chu,", 
        "tsunami": 1, 
        "place": "19km NNE of Upper Lake, California", 
        "time": 1470797837510, 
        "mmi": 3.74
      }, 
      "id": "nc72672610"
    }
  ], 
  "metadata": {
    "status": 200, 
    "count": 2, 
    "title": "USGS Significant Earthquakes, Past Week", 
    "url": "http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/significant_week.geojson", 
    "generated": 1471184780000, 
    "api": "1.5.2"
  }
}
```
