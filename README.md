# [Developer's Log, Supplemental](https://dircodt.github.io/)

## Overview

This is the *Data Visualisation* portion of my (unfinished) solution to the City of Cape Town's Data Science Unit Code Challenge.

* [Open the interactive demo](https://dircodt.github.io/coct/index.html)

Unfortunately I was not able to complete all the features I had envisioned. I might finish it later for my own benefit. I don't actually use any of these libraries at my current job, but I enjoyed using Vanilla JS again.

## Data File

The data preparation was done in this related repo:

* [https://github.com/DircoDT/ds_code_challenge](https://github.com/DircoDT/ds_code_challenge)

That repo could use a proper write-up of its own, but here I will only focus on the output required for the data visualisation task.

The download size is kept small by filtering out all the data not needed for this exercise. That includes:

* All rows other than the Water and Sanitation directorate
* All rows without a valid location (h3 hexagon ID)
* All hexagons with zero service requests

In addition, the SR count was aggregated by month for each area, instead of keeping the individual entries. It is not strictly necessary, but having *tens* of thousands of rows gives us better interactivity than we could get with *hundreds* of thousands of rows. (If we wanted more temporal resolution at the expense of spatial resolution, we could aggregate by week and suburb, leaving out the individual hexagons.)

The final dataset now contains the following columns:

* **h3_id** - H3 hexagon ID
* **suburb** - Name of the suburb
* **month** - Month (and year)
* **sr_count** - Number of service requests

I considered including "Typical Time To Completion" in the plot, but the timestamp columns had a very wide range and many outliers, so I will leave that for a future analysis. A column to indicate the severity of each service request could also be useful.

## Screen Layout

The plan was for the app to have three main parts:

* **Map** - to focus on the spatial aspect
* **Chart** - to focus on the temporal aspect
* **Table** - to act as data source for the above, including advanced filtering

The data would be loaded into the table first, where the user could filter by any of the columns. The remaining rows would then be used to populate both the map and the chart. With this workflow, we can let the user toggle between the map view and the chart view, because they do not depend on each other.

Although, with hindsight, it may have been better to leave out the advanced filtering and just populate the map directly with a `.geojson` file, with a simple drop-down to filter by suburb and a range slider for start and end date.

## Data Storytelling

*Coming soon...*

## Design Principles

*Coming soon...*

## Libraries / Includes

* [deck.gl](https://github.com/visgl/deck.gl)
  For the map control
* [MapLibre GL JS](https://github.com/maplibre/maplibre-gl-js/)
  Integrated with the above
* [h3-js](https://github.com/uber/h3-js)
  To get hexagon coordinates from the H3 ID
* [pako](https://github.com/nodeca/pako)
  To decompress gzipped files in the browser
* [PapaParse](https://github.com/mholt/PapaParse)
  To parse the downloaded CSV or JSON data
* [chroma.js](https://github.com/gka/chroma.js)
  Utility functions for gradient colourmaps
* ~~[Tabulator](https://github.com/olifolkerd/tabulator)~~
  *Not as feature-rich as expected. Try AG Grid instead.*
* [AG Grid](https://github.com/ag-grid/ag-grid)
  Datatable with sorting/filtering/grouping
* [amCharts](https://github.com/amcharts/amcharts5)
  Nice interactive charts

[MapTiler](https://www.maptiler.com/) is currently used for the map tiles, but that could be switched out for a self-hosted solution, especially if we only require a small portion of the globe.
