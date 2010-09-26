******************
Creating first map
******************

The process of creating map involves applying rules and styles to
spatial datasets which produces a final raster image. To get started
you should first :doc:`install Mapnik library </getting_started>`.

This tutorial will focus on creating a simple Python script in which
we will use Mapnik library to render a map. Although you can use any
text file editor to edit Python scripts, you should use one which you
feel most comfortable with. If you never used Python, you should read
some `introductory tutorial <http://diveintopython.org/>`_.

.. note:: 
   
   Create a single directory which will contain all of tutorial
   files, i.e **mapnik_tutorial**


Spatial data
============

There can be no map without data, fortunately there are a large number
of resources available online.  For this tutorial we are going to use
a simple dataset available for download at
http://mapnik-utils.googlecode.com/svn/data/world_borders.zip. You
should download this file and unpack it to your tutorial directory.

After unpacking you should have 4 new files which define a Shape file
dataset:

* world_borders.shp - actual geometry of the features
* world_borders.shx - positional index of feature geometry
* world_borders.dbf - attributes of features
* world_borders.prj - optional file, defines projection in `well-known
  text <http://en.wikipedia.org/wiki/Well-known_text>`_ format

.. hint::

   Mapnik comes with a *shapeindex* utility which creates spatial
   index for Shape file datasets. Spatial index speeds up data access,
   especially for large datasets.  `shapeindex reference <index.html>`_

Additional free datasets are provided on this services:

* some service
* some other service


First steps
===========

Step 1
______

Open up your text editor and start editing a new file. For now just
copy/paste following code and save your file, i.e. ``tutorial01.py``.

.. code-block:: python
   :linenos:

   import mapnik

   map = mapnik.Map(600,300,"+proj=latlong +datum=WGS84")
   map.background = mapnik.Color('steelblue')

   mapnik.render_to_file(map,'world.png', 'png')

After you saved the file you should execute it. Open up a terminal, 
navigate to the folder with saved file and spatial data and run:
::

   $ python tutorial01.py

Running this Python script should produce a new image file
``worild.png`` which can be viewed in any image viewer. Now let's
examine what have we done in more detail.

On the first code line we ``import mapnik`` module to current Python
interpreter environment. This enables us to access Mapnik library in
Python code. To create a map we need to create a new ``mapnik.Map``
object (insert link to reference). So on the line 3 we create a
mapnik.Map object with 3 parameters: *width*, *height* and spatial
reference system (*SRS*) definition, and assign it a name ``map``.

.. note ::

  Mapnik accepts any projection that Proj.4 handles. See
  http://spatialreference.org for the proj4 strings for various
  projections. For `example
  <http://spatialreference.org/ref/epsg/4326/mapnikpython/>`_ will
  give you the exact parameters for EPSG 4326.

  You can read more about spatial reference systems and projections in
  :doc:`introducition to GIS </introduction_to_GIS>`


In our case data is in **EPSG 4326** spatial reference system and
matching *Proj.4* string is ``+proj=latlong +datum=WGS84``. On the
next line we assign map object attribute ``background`` (insert link
to reference) a new ``mapnik.Color`` object (insert link to
reference). 

Color object accepts 'named' colours, #rrggbb, #rgb,
rgb(r%,g%,b%) or rgba(r%,g%,b%,a%) format. Named color *steelblue* is
equivalent to hex triplet *#4682b4* or *rgb(70, 130, 180)*.

Last step, on the line 6, saves current map object to file
``world.png`` of type ``png`` using ``mapnik.render_to_file`` function
(insert link to reference). Final result should be a blank image with
steelblue background, 600px width and 300px height in PNG format,
similar to this one:

.. image :: images/tut01.png
   :align: center
   :scale: 75%
   :alt: tutorial01.py resulting image 

And that's it you've just created your first map, even though it
doesn't actually use any spatial data.

Step 2
______
