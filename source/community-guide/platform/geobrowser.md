---
substitutions:
  geobrowser_button_fullscreen.png: |-
    ```{image} ../../includes/geobrowser_button_fullscreen.png
    ```
  geobrowser_button_geocoding.png: |-
    ```{image} ../../includes/geobrowser_button_geocoding.png
    ```
  geobrowser_button_layers.png: |-
    ```{image} ../../includes/geobrowser_button_layers.png
    ```
  geobrowser_button_meter.png: |-
    ```{image} ../../includes/geobrowser_button_meter.png
    ```
  geobrowser_button_minus.png: |-
    ```{image} ../../includes/geobrowser_button_minus.png
    ```
  geobrowser_button_placemark.png: |-
    ```{image} ../../includes/geobrowser_button_placemark.png
    ```
  geobrowser_button_plus.png: |-
    ```{image} ../../includes/geobrowser_button_plus.png
    ```
  geobrowser_button_polygon.png: |-
    ```{image} ../../includes/geobrowser_button_polygon.png
    ```
  geobrowser_button_query.png: |-
    ```{image} ../../includes/geobrowser_button_query.png
    ```
  geobrowser_button_recbox.png: |-
    ```{image} ../../includes/geobrowser_button_recbox.png
    ```
  geobrowser_button_search.png: |-
    ```{image} ../../includes/geobrowser_button_search.png
    ```
  geobrowser_button_search_area.png: |-
    ```{image} ../../includes/geobrowser_button_search_area.png
    ```
  geobrowser_button_wkt.png: |-
    ```{image} ../../includes/geobrowser_button_wkt.png
    ```
  geobrowser_disaster_big_group.png: |-
    ```{image} ../../includes/geobrowser_disaster_big_group.png
    ```
  geobrowser_disaster_event.png: |-
    ```{image} ../../includes/geobrowser_disaster_event.png
    ```
  geobrowser_disaster_small_group.png: |-
    ```{image} ../../includes/geobrowser_disaster_small_group.png
    ```
  get_param_from_map_button.png: |-
    ```{image} ../../includes/get_param_from_map_button.png
    ```
---

# GeoBrowser area for data and Cloud processing services

## GeoBrowser

:::{figure} ../../includes/geobrowser.png
:figclass: img-border img-max-width
:::

The GeoBrowser differ from one thematic application to another. It can be composed of:

> - a [Map], where the user can make search query and see results
> - layers that can be displayed on the map
> - [Contexts] links
> - [Results] tab (initialy hidden)
> - [Processing services tab] (initialy hidden)

### Map

The map is just a simple map, on which you can zoom in, zoom out and navigate.

Some buttons maybe used to interact with the map:

- {{ geobrowser_button_search.png }} search area
- {{ geobrowser_button_plus.png }} Zoom in
- {{ geobrowser_button_minus.png }} Zoom out
- {{ geobrowser_button_query.png }} Open query search tab
- {{ geobrowser_button_polygon.png }} Edit the search bbox by drawing a polygon on the map
- {{ geobrowser_button_recbox.png }} Edit the search bbox by drawing a rectangle on the map
- {{ geobrowser_button_fullscreen.png }} Put the map in full screen
- {{ geobrowser_button_wkt.png }} Allow to enter a WKT to be displayed on the map as bounding box
- {{ geobrowser_button_meter.png }} Measure an area
- {{ geobrowser_button_geocoding.png }} Geocoding tool
- {{ geobrowser_button_layers.png }} Change the background of the map | Select layers to be displayed.

#### Search area

From the geobrowser, a search area can be accessed by clicking on the {{ geobrowser_button_search.png }} button. This expands a view containing all search parameters associated to the current catalogue on which the search will be performed.
Some parameters are just free text, others can be chosen from a list, and some parameters can be filled from the geobrowser. This is the case of:

- the temporal parameter which can be filled by moving the temporal bar present on the geobrowser.

:::{figure} ../../includes/geobrowser_timebar.png
:figclass: img-border img-max-width
:::

- the geographical area which can be filled either from the bbox drawn on the map using {{ geobrowser_button_polygon.png }}, {{ geobrowser_button_recbox.png }}, {{ geobrowser_button_placemark.png }} or by uploading a shapefile, a kml or geojson file, using the import button {{ geobrowser_button_wkt.png }}.

```{eval-rst}
.. req:: TS-FUN-280
        :show:

        This section describe the area of interest definition by geometry.
```

```{eval-rst}
.. req:: TS-FUN-300
        :show:

        This section describe the area of interest definition by uploading a vector based file.

```

:::{tip}
in the *Search Term* field supported wildcards are '\*', which matches any character sequence (including the empty one), and '?', which matches any single character.
:::

It is also possible to add layers on the map:

#### Data Results layer

Display the results (orange polygons) of the current search or context.

:::{figure} ../../includes/geobrowser_results_layer.png
:figclass: img-border
:::

#### Area of interest

:::{figure} ../../includes/aoi.png
:align: center
:figclass: img-container-border
:scale: 80%
:::

Area of interest may be defined by the user using the tools to draw a polygon or a rectangle on the map (see [Map]). Once set, the search will be automatically updated with data corresponding to this AOI.

##### Area of interest external definition

Complex Area of interest can be defined by uploading or referencing a vector based file:

- shapefile (limited to 1MB)
- kml (limited to 1MB)

##### Area of Interest according to processing service

Area of Interest may be directly used to fill bounding box parameters exposed by Processing services.
For that, you can use the {{ get_param_from_map_button.png }} button, displayed along the parameter input field. Clicking on it will allow directly to fill the input with the value of the current search bounding box.

#### Geocoding tool

:::{figure} ../../includes/geobrowser_geocoding_1.png
:align: center
:figclass: img-container-border
:scale: 80%
:::

Users can use the Geocoding tool to perform a search by a location (like a city, a region, a place, and so on), see the location on the map, and perform a spatial filter on that location.

By writing a location, a first search produces a list of possible results in a dropdown list. Users can click on a result, and the relative footprint is shown on the map (or a bounding box if the footprint is not available).

The popup of the location footprint offers the way to perform a search in the catalog with the location used as a spatial filter. Users can also decide to perform a bounding box spatial filter or a polygon spatial filter. Note that, for search performance reasons, the searching polygon is simpler than the original footprint polygon (in matter of polygon points).

:::{figure} ../../includes/geobrowser_geocoding_2.png
:align: center
:figclass: img-container-border
:scale: 80%
:::

### Contexts

:::{figure} ../../includes/geobrowser_contexts.png
:figclass: img-border
:::

Some pre-defined context are accessible on the top of the map.
One context is the result of a query on a specific catalog with pre-defined search parameters.
The existing pre-defined contexts are:

- EO data
- EO processing
- Publications
- Community

### Results

:::{figure} ../../includes/geobrowser_resulttab.png
:figclass: img-border img-max-width
:::

The result tab is divided in two parts:

- On the left, the **Results Table** showing the list of current results displayed on the map. Results are paginatd, only 20 items are displayed, select another page to discover more products.
- On the right, the **Features Basket** showing all data in the current basket as well as the data package view, showing all available data packages for the current user with the possibility to load it / use as search.

```{eval-rst}
.. req:: TS-ICD-110
        :show:

        This section describes the data package web widget.
```

Results can be dragged fron the left table to the basket. Then the basket can be saved as a new data package and shared with other users.
Saved Data packages can then be loaded into the basket. (see {doc}`data <../data>` for more details)

## Cloud Processing

Processing services tab can be expanded by clicking on *Processing Services* on the right of the map.
It is composed of two sub tabs.

### Processing services tab

This tab contains the list of available Processing Services. Usually, only 20 Processing services are displayed. If you are looking for a specific one, you can filter the results using the **Filter services** input. Each Processing Service can be opened to display more information such as: name, service description, publisher name, classification, output description but also the list of parameters to fill in order to create a new job associated to this service.

```{eval-rst}
.. req:: TS-FUN-250
        :show:

        This section describes the processing service discovery web widget.
```

```{eval-rst}
.. req:: TS-ICD-030
        :show:

        This section describes the processing service discovery web widget.
```

### Jobs tab

This tab contains the list of available jobs associated to your user.
Details on jobs can be accessed by clicking on the title of the job.

:::{figure} ../../includes/geobrowser_jobs.png
:figclass: img-border
:::

```{eval-rst}
.. req:: TS-ICD-030
        :show:

        This section describes how to access information on a succesful job.

```
