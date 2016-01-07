# geojson-events
Extending GeoJSON with event-like features

## Proposal in a nutshell

- A "when" object analogous to GeoJSON's existing "geometry".
- The values of items in "when" are ISO-8601 or RFC 3339 date/time strings.
- The keys of those items are "instantTime", "startTime", "endTime".
- A "circa" object with the same structure as "when" can be used to communicate
  fuzziness or imprecision.

## Instantaneous event-like feature

For a thing that exists at a certain time.

```
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
    "instantTime": "2014-04-24"
  }
}
```

## Non-instaneous event-like feature

For a thing that exists during a certain interval.

```
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
    "startTime": "2014-04-24",
    "endTime": "2014-04-25",
  }
}
```

## Open-ended event-like feature

For a thing that exists *since* a certain time.

```
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
    "startTime": "2014-04-24"
  }
}
```

## Fuzzy instant

For a thing that exists at a certain time with fuzzy bounds. Displaying such
things is a feature of Simile's Timeline.

```
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
  "circa": {
    "startTime": "2014-04-23",
    "endTime": "2014-04-25"
  },
  "when": {
    "instantTime": "2014-04-24"
  }
}
```

## Open-ended interval with a fuzzy start

For a thing that exists since an approximately known time.

```
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
  "circa": {
    "startTime": "2014-04-23"
  },
  "when": {
    "startTime": "2014-04-24"
  }
}
```
