# Wildfires-Angola
Code for the project "Largest Wildfires in Angola: Correlation of vegetation and meteorological variables with wildfire intensity", led by Karapetian et al., during the Climatematch Summer School (2023).

# NDVI_DNBR_Micropublication.ipynb

This code uses the Globfire (Artés et al., 2019) and MODIS Surface Reflectance 8-Day product (Vermote, 2021) data to calculate the NDVI and dNBR for the largest fires of Angola in 2020.

0. Data acquisition 

Prior to running this code, the following datasets should be downloaded: 

1) Globfire (Artés et al., 2019), available here: https://gwis.jrc.ec.europa.eu/apps/country.profile/downloads

   *Note: the dataset used here is a subset of the Globfire dataset, created by Brittany Engle, containing only 
   fires of category F (1000 acres) or greater. This dataset was graciously provided to us by the Climatematch    organizers, saved here: "~/shared/Data/Projects/Wildfires/ClimateAction_countries.shp".


2) MODIS Surface Reflectance 8-Day product (Vermote, 2021) data (more information here https://lpdaac.usgs.gov/products/mod09a1v061/), available here: https://search.earthdata.nasa.gov/search/granules?p=C2343111356-LPCLOUD!C2343111356-LPCLOUD&pg[1][v]=t&pg[1][dnf]=DAY&pg[1][id]=MOD09A1*h19v09*&pg[1][ecd]=2020-01-01T00%3A00%3A00.000Z%2C2020-12-31T23%3A59%3A59.999Z&pg[1][gsk]=-start_date&pg[1][m]=download&pg[1][cd]=f&fi=MODIS&tl=1704799757!3!! (need to register to have access to data)
 
  - we selected the entire 2020 year and tiles (19,09), (20,09), (19,10) and (20,10), which cover Angola, by searching for filenames "MOD09A1*h19v09*", "MOD09A1*h19v10*", "MOD09A1*h20v09*" "and MOD09A1*h20v10*" and all dates in the 2020 year  
  - this resulted in 187 .hdf files (46 or 47 per tile)
  - these images are saved under ~/shared-public/Jintasaurus_Skip_Energico/modis_images 

1. Using the data in the Globfire dataset (Artés et al., 2019), select 50 largest fires per vegetation type (Forest, Shrub and Herbaceous vegetation)

2. For each vegetation type and each fire:

    2.1 Get fire start and end dates 
    
    2.2 Get polygon of fire
    
    2.3 For each fire, get the closest pre and closest post images from the pre-downloaded MODIS images
    
    2.4 Get the latitude and longitude extent of MODIS image
    
    2.5 Load pre and post fire images
    
    2.6 Compute and apply cloud masks
    
    2.7 Calculate pre-fire NDVI for polygon
    
        2.7.1 Calculate NDVI for whole image
        
        2.7.2 Remap NDVI to a different color scheme
        
        2.7.3 Plot NDVI 
        
        2.7.4 Select NDVI values for the fire polygon 
        
        2.7.5 Average over fire polygon 
        
    2.8 Calculate dNBR for polygon 
    
        2.8.1 Calculate dNBR for whole image
        
        2.8.1 Remap dNBR to a different color scheme
        
        2.8.3 Plot dNBR
        
        2.8.4 Select dNBR values for the fire polygon
        
        2.7.5 Average over fire polygon

# CorrelationMatrix.ipynb

This code uses the Globfire, a subset of the Global Wildfire Information System (GWIS) including the MODIS burned area product (Antès et al., 2019); 2) ERA5-Land (Muñoz-Sabater et al., 2021) for temperature and wind data; and 3) CHIRPS for precipitation (Funk, 2015) for the largest fires of Angola in 2020.

0. Data acquisition 

The following datasets were used: 

1) Globfire (Antès et al., 2019), available here: https://gwis.jrc.ec.europa.eu/apps/country.profile/downloads

   *Note: the dataset used here is a subset of the Globfire dataset, created by Brittany Engle, containing only 
   fires of category F (1000 acres) or greater. This dataset was graciously provided to us by the Climatematch organizers, saved here: "~/shared/Data/Projects/Wildfires/ClimateAction_countries.shp".

2) Climate Hazards Group InfraRed Precipitation with Station data (CHIRPS) were used for daily precipitation values (more information here https://www.chc.ucsb.edu/data/chirps), available here: https://data.chc.ucsb.edu/products/CHIRPS-2.0/global_daily/netcdf/p25/

	
3) ERA5-Land data for temperature and wind data (more information here https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels) available here https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels?tab=form 
	- the 2m montly temperature data were provided to us by the Climatematch organizers, saved here ~/shared/Data/Projects/Albedo/ERA/Temperature-003.nc		
	- the wind data were downloaded by us and saved here ~/shared-public/Jintasaurus_Skip_Energico/era_data/monthlywind_ang2020.grib

4) MODIS Surface Reflectance 8-Day product (Vermote, 2021) data as explained in ReadMe_NDVI_DNBR_Micropublication.txt 
	
1. Using the data in the Globfire dataset, select 50 largest fires per vegetation type (Forest, Shrub and Herbaceous vegetation)

2. Load the pre-downloaded CHIRPS and ERA-5 data with the precitipation, temperature and wind speed values

3. Load the NDVI and dNBR values stored separately in NDVI_DNBR_Micropublication.ipynb

4. define functions

5. For each vegetation type and each fire:

    5.1 Get fire start and end dates 
    
    5.2 Get polygon of fire
    
    5.3 For each fire, combined the all types of data (wildfire data, temperature, precipitation, wind speed, NDVI, dNBR) into one pandas dataframe   
   
    5.5 Compute the correlation matrix and significance matrix, excluding all values with p>=0.05
    
    5.6 Plot the scatter plots for significant correlations
	    
    5.7 Plot the correlation matrix
    
        

