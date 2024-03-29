# simple_rsf
Repository for doing simple resource selection analysis in Moveapps 
Github repository: https://github.com/nilanjanchatterjee/basic_rsf

## Description
The app models the *used* and *available* points generated in the **Background point generator** app into a resource selection function for a population or each individual from a tracking dataset.

## Documentation
   
This app models the data for resource selection analysis. For the analysis, *used* points are the locations from the radio-telemetry data and *background* points are randomly generated locations to model the habitat selection. The analysis can be carried out for each individual or for the population in this app and the number of background points can also be defined by the user as a ratio between *used* and *background* points in the `Background Point Generator` app. 

Environmental variables (**Raster file**) need to be projected in the **lat-long** format. Other projection formats will lead to an error in the modelling. The app includes a fall-back file of elevation layer (`elevatR` package), percentage forest cover(https://lpdaac.usgs.gov/products/gfcc30tcv003/), landuse-landcover data (https://modis.gsfc.nasa.gov/data/dataprod/mod12.php) and global human modification (https://data.nasa.gov/dataset/Global-Human-Modification-of-Terrestrial-Systems/4t8v-e7f3/about_data) for the habitat selection analysis. 

Also, users need to be careful about the raster type while uploading. If you are uploading a categorical raster (Landuse-landcover etc.) then change the app settings to be `TRUE` for the categorical settings.

The output file includes a coefficient plot of the variables used in the resource selection function and a data frame of regression coefficients. Coefficients overlapping zero shows non-significance whereas coefficients greater than 0 shows preference and less than 0 signifies avoidance of the environmental variable. 

## Input data

*move/moveStack* in Movebank format 

## Output data

*move/moveStack* in Movebank format 

### Artefacts

*.csv* with the regression coefficients   

The landuse data has 17 classes and the coefficient refers the specific habitat with respect to first habitat class. Detailed classification of the different landuse-landcover classes can be found here (LC_Type1), https://developers.google.com/earth-engine/datasets/catalog/MODIS_061_MCD12Q1

- `trackId` denotes the individual id if the resource selection analysis is done for individual wise
- `term` stands for the environmental variable used in the analysis
- `estimate` represents the coefficient estimate of the habitat variables
- `std.error` represents the standard error 
- `statistic` represents the value of the z-statistic
- `p.value` represents whether the coefficient estimate is significantly different from 0 or not
- `conf.low` shows the lower confidence limit of the coefficient estimate (95% CI)
- `conf.high` shows the higher confidence limit of the coefficient estimate (95% CI)

*.jpeg* with the coefficient plot
- `delx` represent the affinity towards the centroid location of the individual/population for longitude
- `dely` represent the affinity towards the centroid location of the individual/population for latitude
- `delxy` represent the affinity towards the centroid location of the individual/population for both the axes
- other environmental variables with their respective preference/avoidance

and another *.jpeg* with the environmental raster(s) plotted with the species presence locations