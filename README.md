<p align="center">
  <img src="assets/triage-logo.png" alt="DARPA Triage Challenge" width="300">
</p>

<h1 align="center">DARPA Triage Challenge — Course Files</h1>

Geospatial course files (CSV + KML) for each course in the
**DARPA Triage Challenge Final Event**. This repository publishes the geofence,
starting zone, and fiducial geometry for every course so teams can load them into
mapping, planning, and ground-control software.

---

## About the Challenge

*The following is quoted from the
[DARPA Triage Challenge Finals](https://www.darpa.mil/research/challenges/darpa-triage-challenge/finals) page.*

### The Most Complex Environments Yet

Building on Events 1 and 2, the DARPA Triage Challenge Finals will take place in
Disaster City, Texas – a purpose-built testbed near College Station designed to be
realistic, rigorous, and outcome-focused.

Teams will have to operate in challenging conditions, including darkness, smoke,
fire, varied terrain, buildings, and rubble.

Scenarios will emphasize human-machine teaming, lives saved, and standardized medic
performance.

**Data** — Using limited clinical data, algorithms must not only identify injuries
but also predict any life-saving procedures that a casualty will need hours later.

**Systems** — Autonomous or partially autonomous uncrewed aerial vehicles (UAVs) and
uncrewed ground vehicles (UGVs) must accurately locate casualties, identify
life-threatening injuries, conduct trauma assessments, capture vital signs from a
standoff distance, and share information with human medic teams.

### How Teams Win

Teams earn points for passing specific “gates,” such as finding a casualty and making
a diagnosis. Scores reflect the speed and accuracy of results, with bonus points
awarded for reporting casualties within the “golden window,” the period after injury
when medical treatment is most likely to prevent death.

### Timeline

Data and systems teams compete in separate finals events in 2026.

| | Date |
| --- | --- |
| Data competition | Oct. 10 |
| Systems competition | Nov. 5-13 |
| Awards ceremony | Nov. 13 |

Learn more:
[Finals](https://www.darpa.mil/research/challenges/darpa-triage-challenge/finals) ·
[Systems Competition](https://www.darpa.mil/research/challenges/darpa-triage-challenge/events/event-3/systems-competition) ·
[Teams](https://www.darpa.mil/research/challenges/darpa-triage-challenge/resources/teams)

---

## Repository Structure

The repository is organized as **one folder per course**. Each folder holds a single
CSV and KML describing that course's geometry.

```
Course-Files/
├── assets/
│   └── triage-logo.png
├── parking-lot/
│   ├── parking-lot.csv   
│   └── parking-lot.kml   
├── team-tent-fiducials/
│   ├── team-tent-fiducials.csv   
│   └── team-tent-fiducials.kml   
├── practice-1/
│   ├── practice-1.csv   
│   └── practice-1.kml   
├── practice-2/
│   ├── practice-2.csv   
│   └── practice-2.kml   
├── gate-1/
│   ├── gate-1.csv   
│   └── gate-1.kml   
├── gate-2/
│   ├── gate-2.csv   
│   └── gate-2.kml   
├── gate-3/
│   ├── gate-3.csv   
│   └── gate-3.kml   
├── gate-4/
│   ├── gate-4.csv   
│   └── gate-4.kml   
├── hmt-day/
│   ├── hmt-day.csv   
│   └── hmt-day.kml   
├── hmt-night/
│   ├── hmt-night.csv   
│   └── hmt-night.kml   
├── championship/
│   ├── championship.csv   
│   └── championship.kml   
```

### What's in each course file

| Feature | Geometry | KML color | Description |
| --- | --- | --- | --- |
| **Course Boundary** | Polygon | 🔴 Red | The geofence for the course |
| **Start** | Polygon | 🟢 Green | The starting zone for the course (supplied per course) |
| **Fiducial &lt;number&gt;** | Point | 🔵 Blue | Fiducial location, provided as a single point (see below) |
| **POI &lt;number&gt;** | Point | 🟠 Amber | *Optional.* Points of interest for the course (see below) |

#### Fiducials

Each fiducial is named with a number, e.g. `Fiducial 100`. Every distinct physical
fiducial location has its own unique number. If a fiducial appears in more than one
course file, it keeps the same number in each.

#### Points of interest (optional)

A course may optionally include one or more points of interest, each provided as a
single point and named sequentially: `POI 1`, `POI 2`, and so on. Courses without
points of interest simply omit these features. A description of what these POIs
represent will be provided in a future update.

> The `parking-lot` course includes an example `POI 1` placed at the centroid of the
> course boundary.

### File formats

- **`<course>.csv`** — three columns: `WKT`, `Name`, `Description`. Geometry is stored
  as [OGC Well-Known Text](https://en.wikipedia.org/wiki/Well-known_text_representation_of_geometry)
  (`POLYGON`/`POINT`) in **WGS 84 (EPSG:4326)**, with coordinates in **`longitude latitude`**
  order. Ideal for spreadsheets, GIS imports, and scripting.
- **`<course>.kml`** — the same features as styled placemarks, ready to open directly in
  **Google Earth**, **QGIS**, or **ArcGIS**. Each feature is color-coded per the table above.

### Coordinate reference

All geometry uses the **WGS 84** datum (EPSG:4326). CSV WKT lists coordinates as
`longitude latitude`; KML uses `longitude,latitude,0`.

---

## Using the files

- **Google Earth:** open any `<course>.kml` to view the geofence, starting zone, and fiducial on the map.
- **QGIS / ArcGIS:** add the `.kml` directly, or import the `.csv` as delimited text using the `WKT` field as the geometry.
- **Scripting (Python):** parse the `WKT` column with `shapely.wkt.loads` for analysis or format conversion.
