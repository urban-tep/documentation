# Global Urban Footprint

The Global Urban Footprint application allows subsetting of a GUF dataset and the subsequent combination of this GUF subset in an analysis, e.g. for statistics.

:::{figure} ../includes/thematic_apps_guf.png
:figclass: img-border img-max-width
:scale: 80%
:::

First select "Urban TEP subsetting". This will lead to the form to generate the desired subset in an Urban TEP processing centre. Parameters you can choose for this step are:

- The GUF input, either a 12m GUF of Europe (tiled), provided by DLR, or a 300m GUF with global coverage (tiled or not), derived from ESA Land Cover CCI
- The bounding box of the region: Use the map to draw the region
- The Parameters for spatio-temporal aggregation: The default XML in it lists all options but switches off mosaicing by default. You can simply replace the complete xml by either the string "true" or a resolution, e.g. 75 if you do not need the detailed parameters.

Note that in case of tiled input you may get several tile subsets as result in case your region intersects tile boundaries.

Second, select "Analyse in PUMA".
