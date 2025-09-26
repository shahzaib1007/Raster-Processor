![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)
# RiverObs

This is a package written initially by
[Ernesto Rodriguez](mailto:ernesto.rodriguez@jpl.nasa.gov) to estimate
various river parameters starting from remote sensing data.
[Alex Fore](mailto:alexander.fore@jpl.nasa.gov), [Brent Williams](mailto:brent.a.williams@jpl.nasa.gov), 
[Cassie Stuurman](mailto:cassie.stuurman@jpl.nasa.gov), [Rui Wei](mailto:rui.wei@jpl.nasa.gov), 
and [Renato P.M. Frasson](mailto:renato.prata.de.moraes.frasson@jpl.nasa.gov) have also provided code 
to reflect the evolving SWOT project.
The code is currently maintained by the SWOT Algorithm Definition Team.

Detailed installation instructions are in the Install.md file.

# Usage

For generating data products are most similar to the SWOT project's data products, the following script is recommended (found in src/bin):
```
usage: swot_pixc2rivertile.py [-h] [--shpbasedir SHPBASEDIR] [-l LOG_LEVEL]
                              [--gdem-file GDEM_FILE]
                              pixc_file out_riverobs_file out_pixc_vector_file
                              rdf_file
```
where ```pixc_file``` is the SWOT high-resolution pixel cloud data product, ```out_riverobs_file``` is the filename of the output rivertile data product, ```out_pixc_vector_file``` is the filename of the output pixel cloud vector data product, ```rdf_file``` is the configuration file (see [this link](https://github.com/SWOTAlgorithms/RiverObs/blob/develop/src/bin/swot_pixc2rivertile.py#L13)) for the recommended configuration). Additionally there are some optional arguments: ```--shpbasedir SHPBASEDIR``` will write out the nodes and reaches as shapefile format (written as netCDF to ```out_riverobs_file```), ```-l LOG_LEVEL``` controls the verbosity of the logging, and ```--gdem-file GDEM_FILE``` will create a pixc_file from the GDEM file and run RiverObs on that as a type of truth processing.

# Prior Reach Database
RiverObs requires a prior reach and node database. The database contains fixed node locations, reach boundaries, and high-resolution reach centerlines. It is distributed as a set of netcdf files, broken by continent (first two characters in the file name) and "major basins" in the continent (3rd and 4th characters in the file name). Metadata describing the database fields and the current version of the database is available [here](http://gaia.geosci.unc.edu/SWORD/). 

## Summary of packages provided

**RiverObs**: This is the main package for associating data with river
reaches, and estimating hydrology parameters base on reach
averaging (or not...). In addition to the homegrown packages listed
below, this package requires the following open source packages:

* [scipy](http://www.scipy.org/): Science algorithms swiss army knife.
* [numpy](http://www.scipy.org/): Numerics swiss army knife.
* [netCDF4](code.google.com/p/netcdf4-python): Reading netcdf4 files,
  including SWOT L2 data files.
* [StatsModels](http://statsmodels.sourceforge.net): Fitting and
  estimation tools.
* [pysal](http://pysal.org): nice interface to shapefiles and
      shapely bridge.  
* [pyproj](http://code.google.com/p/pyproj): Cartographic
      projections swiss army knife.
* [pandas](http://pandas.pydata.org): The Python Data Analysis
  Library for DataFrames and HDFStore.
* [pytables](http://www.pytables.org): easy HDF5 support, required for
  pandas HDFStore.

**Centerline**: Provides a class that can be used to project data
   or refine a river center line. Requires the following packages:

* [scipy](http://www.scipy.org/): Science algorithms swiss army knife.
* [numpy](http://www.scipy.org/): Numerics swiss army knife.

**GeometryDataBase**: Find quickly which reach intersects with a
   geometry of interest. The geometries are assumed to be stored in a
   shapefile. Requires the following packages:

* [Rtree](https://github.com/Toblerity/rtree): Fast bounding box queries.
* [libspatialindex](http://libspatialindex.github.io): Required by Rtree.
* [pysal](http://pysal.org): nice interface to shapefiles and
      shapely bridge.
* [shapely](https://github.com/sgillies/shapely): geometry
      calculations.

**SWOTRiver**: This package contains classes that use the RiverObs
capabilities to produce hydrology outputs from SWOT (simulated) data.

* [numpy](http://www.scipy.org/): Numerics swiss army knife.
* [netCDF4](code.google.com/p/netcdf4-python): Reading netcdf4 files,
  including SWOT L2 data files.
* [pyproj](http://code.google.com/p/pyproj): Cartographic
      projections swiss army knife.
* [pandas](http://pandas.pydata.org): The Python Data Analysis
  Library for DataFrames and HDFStore.
* [pytables](http://www.pytables.org): easy HDF5 support, required for
  pandas HDFStore.

**GDALOGRUtilities**: Provides homegrown utilities for reading and writing
   various GIS files. Requires the following packages:

* [gdal](http://www.gdal.org): GIS files swiss army knife.
* [pyproj](http://code.google.com/p/pyproj): Cartographic
      projections swiss army knife.

**GWDLR**: This is an optional package to convert Global Width
   Database-Large Rivers raster data provided by
   [Dai Yamazaki](mailto:bigasmountain1022@gmail.com)  to vectors that can be used as
   centerlines. Requires:

* [grass](http://grass.osgeo.org): for raster to vector program.
* [scikit-image](http://scikit-image.org): for skeletonize.

![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)
# Raster

This is a package written by [Alexander Corben](mailto:alexander.t.corben@jpl.nasa.gov) (JPL) and Shuai Zhang (UNC) to produce a raster image product from SWOT pixel-cloud data. The code is currently maintained by the SWOT Algorithm Definition Team.

# Usage

For generating data products that are most similar to the SWOT project's data products, the following script is recommended (found in src/bin). Note that this script will generate a raster product corresponding to a single pixel cloud product tile, not a raster scene like the official SWOT project's data products:
```
usage: swot_pixc2raster.py [-h] [-pv PIXCVEC_FILE] [-id INTERNAL_FILES_DIR]
                           [-mp MAX_WORKER_PROCESSES] [-l LOG_LEVEL]
                           [--crid CRID] [--contact CONTACT]
                           [--product_counter PRODUCT_COUNTER]
                           pixc_file alg_config_file runtime_config_file
                           output_file
```
where ```pixc_file``` is the SWOT high-resolution pixel-cloud data product, ```alg_config_file``` is the algorithmic configuration file, ```runtime_config_file``` is the runtime configuration file, and ```output_file``` is the filename of the output raster data product. See [this_link](https://github.com/SWOTAlgorithms/Raster-Processor/blob/develop/src/bin/swot_pixc2raster.py) for an example configuration. Additionally there are some optional arguments: ```-pv PIXCVEC_FILE``` will specify a pixel-cloud vector data product to use for aggregation of ice flags and improved height-constrained geolocation if commanded in the algorithmic configuration file, ```-id INTERNAL_FILES_DIR``` will specify the directory in which internal files will be written, ```-mp MAX_WORKER_PROCESSES``` will specify the maximum number of worker processes to spawn for multithreading, ```-l LOG_LEVEL``` will specify the level of log messages to report, ```--crid CRID``` will specify a command reference id to report in the output product attributes, ```--contact CONTACT``` will specify contact information to report in the output product attributes, and ```--product_counter PRODUCT_COUNTER``` will specify a product counter to report in the output product attributes.

The software is dependent on the open source RiverObs code at https://github.com/SWOTAlgorithms/RiverObs and the SWOT Hydrology Toolbox at https://github.com/CNES/swot-hydrology-toolbox.

# Processing Information

![alt text](img/Fig1.png)

Fig. 1. Flowchart

The first step to convert pixel-cloud product to raster is re-projection (Fig. 1). Pixels under GEO lat/lon are re-projected to the appropriate UTM projection. Since each raster grid may contain multiple pixel-cloud pixels, an aggregation operation is needed specific to each output variable layer. The aggregation operations for water surface elevation and water area are provided here.

## Water surface elevation and water area

The equation for calculating water surface elevation in raster product is in equation (1), where wse_i is the water surface elevation of the ith grid in raster product. wse(x) is the water surface elevation for pixel-cloud pixel x, which is assigned to the ith grid in raster product. N is total number of pixel-cloud pixels which are assigned to the ith grid of raster product (N can be calculated through re-projection).

wse_i=(∑_x wse(x))/N
	(1)
The aggregations of water area are different for interior water pixels and edge pixels (Williams 2018). The water areas of interior water pixels are aggregated directly over a raster grid. The areas of water pixels near land and land pixels near water are calculated using a water-fraction based approach. The calculation can be expressed as equation (2),

A_i=∑_x A(x)(I_(dw,in) (x)+α(x)I_de (x))
	(2)

where Ai is the water area of the ith raster grid. Idw,in(x) stands for interior water pixels from pixel-cloud products, and Ide(x) indicates edge pixels of pixel-cloud products. A(x) is the area of pixel-cloud pixel, α(x) is the water fraction of edge pixel in pixel-cloud product. An example of water fraction over Sacramento river in Fig. 2 shows the water fractions of the river centerline are usually higher than pixels along river edge. Note that water faction of some pixels may exceed 1 due to noise in the SWOT pixel cloud inundation extent calculation. At the current stage, we retain these values in the raster product so that the summation across many raster cells will remain unbiased.

![alt text](img/Fig2.png)

Fig. 2 Water fraction on SWOT raster image over Sacramento river

## Uncertainty estimates

The uncertainty of water fraction and water surface elevation are quantified in the raster product by using the algorithm proposed by Williams (2018). The input variable needed for estimating the water surface elevation and water area uncertainties (e. g. probability of detecting water when there is no water, missed detection rate, correct detection rate) are provided in the pixel-cloud product.

## References

B. Williams, “SWOT Hydrology Height and Area Uncertainty Estimation,” Jet Propulsion Lab, Tech. Rep., 2018.
