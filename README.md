# geojson-events
Extending [RFC 7649](https://tools.ietf.org/html/rfc7946) GeoJSON with
event-like features

## In a nutshell

- Defines a "when" member analogous to GeoJSON's existing "geometry".
- Defines two types of temporal objects: "Instant" and "Interval".
- Values of these objects are ISO-8601 or RFC 3339 date/time strings.

## Examples

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
    "at": "2014-04-24",
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
