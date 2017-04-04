Thematic Apps
=============

Pre-defined apps
----------------

A *Thematic App* is a specific version of the geobrowser, in which specific parameters are pre-defined, in order to serve a specific thematic.
A list of pre-defined thematic apps can be accessed from the *Thematics* page.

.. figure:: ../includes/thematic_apps.png
	:figclass: img-border img-max-width
	:scale: 80%

The pre-defined thematics are:

	- Urban global thematic application
	- Global Urban Footprint

Urban global thematic application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: ../includes/thematic_apps_global.png
	:figclass: img-border img-max-width
	:scale: 80%

This is the general Urban thematic application for demonstration purpose, containing all main functionalities of the geobrowser.

Global Urban Footprint
~~~~~~~~~~~~~~~~~~~~~~

The Global Urban Footprint application allows subsetting of a GUF dataset and the subsequent combination of this GUF subset in an analysis, e.g. for statistics.

.. figure:: ../includes/thematic_apps_guf.png
	:figclass: img-border img-max-width
	:scale: 80%

First select "Urban TEP subsetting". This will lead to the form to generate the desired subset in an Urban TEP processing centre. Parameters you can choose for this step are:

- The GUF input, either a 12m GUF of Europe (tiled), provided by DLR, or a 300m GUF with global coverage (tiled or not), derived from ESA Land Cover CCI
- The bounding box of the region: Use the map to draw the region

Note that in case of tiled input you may get several tile subsets as result in case your region intersects tile boundaries.

Second, select "Analyse in PUMA". 


User's apps
-----------

A user is able to define its own *Thematic App* by selecting widget amongst:

- Dataset search widget defining series, collection or data packages OpenSearch endpoint
- processing Service widget defining service series OpenSearch endpoint
- Map description (background, layers)
- Data package widget defining the data packages OpenSearch endpoint
The application shall be defined using OGC OWS Context.

.. req:: TS-FUN-500
	:show:

	This section describes how a user can create its own thematic application.
