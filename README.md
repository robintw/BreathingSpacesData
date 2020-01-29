# Breathing Spaces Data Store
This is the store of processed air quality data for the [Breathing Spaces](https://breathingspaces.org.uk/) project.

Data here comes from various sources, and has all been processed to bring into the same projection, similar extents etc.

Brief descriptions and explanations of the data are shown below, organised by folder name.

## AURN
Contains code for plotting and getting statistics from the AURN sites in Southampton. This code is not used any more - as data is fetched live via the KCL API for plotting on the webmap - but the code and data is kept in case it is useful in the future.

Both Jupyter notebooks use Robin Wilson's [PyAURN](https://github.com/robintw/pyaurn) module for accessing AURN data. `AURN data plotting.ipynb` contains old plotting code which will output single HTML files for each site with interactive plots. The CSV files contain site locations and statistics, both produced as outputs from the Jupyter notebooks.

## BS Sensors
Contains data from the Breathing Spaces sensors. These are not the 'one source of truth' for this data - that should be the Azure Table that Steven/Flo maintain and the OpenNMS/InfluxDB databases. However, these files are useful - and some are used by the analytics code in [BreathingSpacesCode](https://github.com/robintw/BreathingSpacesCode).

 - `Back data as of Jan 2019` - Back data from the sensors as of January 2019, provided by Flo as exports from the Azure Table (`aq.csv` and `schools.csv`) and as data manually corrected by Flo (`20190307 to 20190823_15min averages_StDenys_6sensors_1.csv`). These data are used by the code to pre-process data before import to InfluxDB in the [BreathingSpacesCode](https://github.com/robintw/BreathingSpacesCode) repository.
 - `Back data for 6hrs missing data - Jan 2019` - The same as above, but including the period of 6hrs missing data caused by an error when administering the InfluxDB server. Used by code in the [BreathingSpacesCode](https://github.com/robintw/BreathingSpacesCode) repository.
 - `2020-01-23_6hrsMissingDataForImport.csv` - Processed data from the sensors during the 6hrs of missing data, ready for import into InfluxDB.
 - `20190307 to 20190823_15min averages_StDenys_6sensors.csv` - raw data from sensors for the early part of the study period. This is the data loaded by the `get_flo_data()` function in `get_aq_data.py` in [BreathingSpacesCode](https://github.com/robintw/BreathingSpacesCode).
 - `BS Sensors - Back Data.csv` - very early data for just a couple of months. Ignore.
 - `DataForImportToInflux_2019-01-22` and `DataForImportToInflux_2019-01-22_Sample.csv` - data for the whole back data period, ready for import into InfluxDB, and a small sample of 50 rows of this data.
 - `MaskedData_NotImportedToInflux_KnownIncorrect_Extracted2019-01-22.csv` - data excluded from the file to be imported into InfluxDB because it is known to be bad. Waiting for manual correction.

## Diffusion Tubes
Data provided by Southampton City Council on measurements from their diffusion tubes located across Southampton. The data was provided in a very poor format, with location data in one file and measurement data in another file, with location information that didn't match. A fuzzy matching technique was used to match them, hence the large number of files.

 - `2017-diffusion-tube-results-summary-reordered_tcm63-392929.xlsx` - original data file from Southampton City Council
 - `ASR 2019 OS References.xlsx` - file provided after first analysis of the data had taken place, with OS grid reference locations for each site. Unused currently.
 - `Current Tubes.csv` - location data for each site extracted from the `NO2 Diffusion Tubes.kmz` file, which was in turn extracted from a Google My Maps map which showed the diffusion tubes
 - `DiffusionTubeMeasurements_MergedAndFixed.csv` - Final merged result with location and measurement data, used in the webmap.
 - `Link Table*.csv` - Linking table used to match up location data and measurement data, created by and used by the Jupyter notebook
- `Merged Diffusion Tube data.ipynb` - code to merge the location and measurement data using the [fuzzymatcher](https://github.com/RobinL/fuzzymatcher) Python package

## PCM
Modelled background pollution data from Defra under their 'Pollution Concentration Modelling' scheme. All raw data obtained from Defra at https://uk-air.defra.gov.uk/data/pcm-data.

 - `AllPCMData_*_Joined.csv` - merged PCM datasets for the year specified. Contains a column for each of the pollutants we're interested in, with the data taken from the raw files (see below). Merging was performed by `Merge PCM data files.ipynb`.
 - `map*.csv` - raw data downloaded from the Defra website for 2016 and 2017
 - `Merge PCM data files.ipynb` - Python code to merge data for each individual pollutant
 - `PCM_2016_Grid_Clipped.gpkg` - GeoPackage, clipped version of `PCM_Grid.gpkg`
 - `PCM_Grid_*.*` - various versions of the gridded PCM data. Clipped versions are clipped to an area around Southampton to reduce the size of the file. Low precision versions have lower precision GeoJSON co-ordinates to also reduce file size.

## Perceptions
Air quality perceptions data from the community, digitised from post-it notes collected on maps at community engagement events.

The [FacilMap website](www.facilmap.org) was used to digitise this data. See the [admin panel] for this data collection campaign for more details here: https://facilmap.org/aqperceptions_admin#16/50.9278/-1.3801/Mpnk

 - `Air quality perceptions.geojson` - export of the raw data from FacilMap

## School Sensors
Data on the location (not actual measurement data) for the schools sensors, run as part of a parallel project.

 - `school notes.*` - location data for each of the school sensors, in Shapefile format.
 - `SchoolSensors.geojson` - same as above, but converted to GeoJSON format for use with the webmap

## Sensor Locations
Breathing Spaces sensor locations - mostly out of date now, use the GeoJSON data in the webmap instead.

## Weather
Weather data for the study area, used in some analytics in code in the [BreathingSpacesCode](https://github.com/robintw/BreathingSpacesCode) repository.

 - `20CR_1871-1947_ncep_1948-2019_12hrs_UK.csv` - Lamb Weather types data for the UK, for use in analysis of weather patterns affecting pollution levels.

