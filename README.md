# owf-data-co-breweries #

This repository contains the [Open Water Foundation (OWF)](http://openwaterfoundation.org) dataset for Colorado breweries.  According to the [Brewers Association](https://www.brewersassociation.org/directories/breweries/), there are 434 breweries in Colorado.  The beer industry is one of the major commercial water users in the state.  The goal of this dataset is to provide data about breweries, particularly data about water use, with the ultimate goal of gaining knowledge about water efficiency in the beer industry.  There is an increasing interest in understanding local water issues and water quality protection, from groups such as [BreWater](https://brewater.com/) in Northern Colorado, as well as using sustainable brewing practices (see the Brewers Association's Best Practices for [Sustainability](https://www.brewersassociation.org/best-practices/sustainability/)).
This is a foundational dataset that provides unique identifiers and other data for breweries and the identifiers can be used to link other datasets, such as municipal water providers.
OWF has created and is maintaining this dataset to facilitate work on various data analysis and visualization projects in Colorado.  **Note that this work is initially focused on the South Platte Basin and, in particular, the City of Fort Collins.  The dataset will continue to be filled in as time and resources permit.** 

## Repository Contents ##

The repository contains the following:

```text
analysis/                                   TSTool software command files to process data into useful forms.
  Process-xlsx-to-csv.TSTool                TSTool command file that processes the core dataset from .xlsx to .csv.
  Process-xlsx-to-geojson.TSTool            TSTool command file that processes the core dataset from .xlsx to .geojson.  
data-orig/                                  Folder containing original data files downloaded from agency websites.
  Business-Entities-in-Colorado.csv         The data file containing original data download from the Colorado Information Marketplace containing Business Entity IDs for entities registered with the Colorado Department of State.  May be used to fill in the dataset in future versions. 
data/                                       Folder containing data files.        
  Brewery-WaterUse-Relate.csv               The Excel file contents from the Brewery_WaterUse_Relate worksheet converted to a csv file, useful for automated processing.  **IN INITIAL STAGES**
  Colorado-Breweries.csv                    The Excel file contents from the Brewery worksheet converted to a csv file, useful for automated processing.
  Colorado-Breweries.geojson                Spatial data file of the locations of breweries.
  Colorado-Breweries.xlsx                   Simple Excel file containing core data.
doc/
  ?                                         Additional documentation for the dataset.
.gitattributes                              Git configuration file indicate repository configuration, in particular handling of line-ending and binary files.
.gitignore                                  Git configuration file to ignore files that should not be committed to the repository.
README.md                                   Explanation of repository contents, data files and sources and TSTool command files used to process the core data into other products.
```

### Colorado-Breweries.xlsx Contents ###

The core Excel workbook that serves as the master data contains the following data columns within the **Brewery** worksheet.

* **BreweryName** - name of the brewery as stated on the brewery's website
* **OWF_ID** - unique text identifier created by OWF to ensure that one type of ID contains values for every brewery
* **OWF_ID_Flag** - data status of OWF_ID values; see more detail below
* **BusinessEntity_ID** - state-assigned identification number for a business entity, from the Colorado Information Marketplace's [Business Entities in Colorado](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) dataset, to link state datasets
* **BusinessEntity_ID_Flag** - data status of BusinessEntity_ID values; see more detail below
* **Physical_Address** - street address of the physical location of the brewery; from the "Business Entities in Colorado" dataset or the brewery's website
* **Municipality** - municipality in which the brewery is located; from the "Business Entities in Colorado" dataset or the brewery's website
* **State** - state in which the brewery is located
* **ZipCode** - zip code in which the brewery is located; from the "Business Entities in Colorado" dataset or the brewery's website
* **Municipality_DOLA_LG_ID** - 5-digit identifier used by Colorado's [Department of Local Affairs (DOLA)](https://dola.colorado.gov/lgis/municipalities.jsf) for the municipality in which the brewery is located, to link DOLA datasets
* **Municipality_DOLA_LG_ID_Flag** - data status of Municipality_DOLA_LG_ID values; see more detail below
* **Municipal_WaterProvider_OWF_ID** - unique text identifier of the municipal water provider that provides water to the brewery; created by OWF to ensure that one type of ID contains values for every brewery
* **Municipal_WaterProvider_OWF_ID** - data status of Municipal_WaterProvider_OWF_ID values; see more detail below
* **Latitude** - latitude of brewery's point location in decimal degrees
* **Longitude** - longitude of brewery's point location in decimal degrees
* **Lat_Long_Flag** - indication of how latitude and longitude were determined; g1 = coordinates are based on the physical address of the brewery
* **WaterSource_GNIS_Name** - [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) name of the stream from which the brewery receives water, to link federal datasets
* **WaterSource_GNIS_Name_Flag** - data status of WaterSource_GNIS_Name values; see more detail below
* **WaterSource_GNIS_ID** - [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) identifier of the stream from which the brewery receives water, to link federal datasets
* **WaterSource_GNIS_ID_Flag** - data status of WaterSource_GNIS_ID values; see more detail below
* **Website** - website URL of the brewery; found by manual search
* **Website_Flag** - data status of Website values; see more detail below
* **Formation_Year** - year the brewery began operation or was incorporated
* **Formation_Year_Flag** - data status of Formation_Year values; see more detail below; G1 = from the "Business Entities in Colorado" dataset, G2 = from the [Fort Collins Coloradoan article](https://www.coloradoan.com/story/life/food/beer/2017/12/30/fort-collins-brewery-scene-still-growing-2018/966966001/) 

#### Data Flags ####
For many data columns, a second column of the same name with the word "_Flag" added to the column name is present.  These columns are an indication of data status as it relates to missing data.  The following conventions are used:
* G = Value is a known/good value.  
* g = Value is an estimated (but good) value.  The associated cell is also highlighted in yellow.
* N = Value is not applicable for the municipality and a blank cell is expected.
* I = Incomplete values; cell has been populated but may not yet contain all values or may need to be further verified
* M = Value is known to be missing in original source and therefore a blank cell indicates that a value cannot be provided.
* m = Value is estimated to be missing.  The associated cell is also highlighted in gray.
* z = Value is unable to be confirmed.  A value is possible but cannot be confirmed one way or the other.  The associated cell is also highlighted in orange.
* x = OWF has not made an attempt to populate the cell at this time.  The value is missing because OWF has not attempted to find the value.  The associated cell is also highlighted in black.

*Note that colors are visible only in xlsx files and not csv files.*

Single-character flags may also be followed with a number, as in g1.  These flags are specific to certain columns and are detailed above in the descriptions of the data columns.  

Column names are taken from original sources if possible.  For clarity and attribution, agency abbreviations may be added to the original column name.  Column name length is not restricted, therefore, some data representations such as Esri shapefiles may contain truncated column names.  In such cases, alternative formats such as GeoJSON are recommended.

Descriptions of identifiers are also provided in the **Notes** worksheet within the workbook.  This worksheet also details how the original data were downloaded and where to find those files.


Other worksheets within the workbook contain the following:

* **Brewery_WaterUse_Relate** worksheet lists annual water use data associated with breweries.  **This worksheet is in the initial stages.**  OWF envisions that this worksheet could contain information such as the following:
	* Beer Production, in gallons or barrels
	* Water Deliveries - amount of water delivered by the municipal water provider (water utility)
	* Wastewater - amount of water returned to the stream
	* Consumptive Use - Water Deliveries subtracted by Wastewater
	* Efficiency - Consumptive Use divided by Beer Production
This worksheet is organized so that each year of data associated with a brewery is its own record.  Therefore, the same brewery may be listed in more than one row and be associated with a different year of data.  This will allow for the establishment of one-to-many relationships when linking to and processing other datasets.

* **ChangeLog** worksheet indicates any changes made to the dataset, the date they occurred and who made the changes.

* **Metadata_Brewery** worksheet serves as the metadata for data columns in the **Brewery** worksheet.


### Colorado-Breweries.csv Contents ###
This file is the **Brewery** worksheet saved in csv format.  Warning:  if this file is opened directly in Excel, IDs that contain leading zeroes will not show those zeroes.  Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.


### Colorado-Breweries.geojson Contents ###
This file is the **Brewery** worksheet saved in GeoJSON format.  This file should be viewable as a map in the GitHub repository.  It can also be used in GIS and mapping applications.


### Brewery-WaterUse-Relate.csv Contents ###
This file is the **Brewery_WaterUse_Relate** worksheet saved in csv format.  Warning:  if this file is opened directly in Excel, IDs that contain leading zeroes will not show those zeroes.  Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.


## Attribution ##

The data sources for this dataset are listed below.

* This dataset began as a list of breweries operating in or near Fort Collins, provided by an [article](https://www.coloradoan.com/story/life/food/beer/2017/12/30/fort-collins-brewery-scene-still-growing-2018/966966001/) from the Fort Collins Coloradoan newspaper.  The article also listed the year in which the brewery opened, which was used for breweries without a BusinessEntity_ID and the Anheuser-Busch and C.B. and Potts breweries, since this information was not clear from the other sources described below.
* The BusinessEntity_ID is from the Colorado Information Marketplace's [Business Entities in Colorado](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) dataset and is a state-assigned identification number.  Because this dataset was initialized from a small number of breweries, OWF manually searched for each brewery within the dataset to find the identifier.  This dataset is also the source for the Physical_Address, Municipality, State, ZipCode and Formation_Year data columns.
* The Colorado Department of Local Affairs (DOLA)'s [Local Government Information System](https://dola.colorado.gov/lgis/counties.jsf) uses a local government ID (LG ID) for municipalities.  OWF is using DOLA_LG_ID instead of LG ID to add more description to the identifier.  DOLA_LG_IDs come from the [Colorado Municipalities](https://github.com/OpenWaterFoundation/owf-data-co-municipalities) dataset created by OWF.
* OWF created municipal water provider IDs in its [Colorado Municipal Water Providers](https://github.com/OpenWaterFoundation/owf-data-co-municipal-water-providers) dataset, to be able to link water provider data, such as water use.
* Each brewery has a physical address listed in the dataset, but not latitude/longitude coordinates.  To obtain coordinate data, the dataset was opened in [Google Sheets](https://www.google.com/sheets/about/).  An add-on named Geocode by Awesome Table can take a physical address and convert it to coordinates, as long as the street address, city, state and zip code are provided.
* The U.S. Geological Survey (USGS)'s [Geographic Names Information System (GNIS)](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) is the Federal and national standard for geographic nomenclature.  The USGS developed the GNIS in support of the U.S. Board on Geographic Names as the official repository of domestic geographic names data.  Most streams in Colorado have a GNIS Name and GNIS ID.
* Website URLs were found by manually searching for brewery websites.  If the brewery does not have a BusinessEntity_ID, then the website was also the source of data for the Physical_Address, Municipality, State and ZipCode data columns.


## Data Workflow ##
The general workflow is as follows once the basic dataset is created:
1. Data flags are created for many of the data columns that indicate data status as described above.
2. The data are formatted as a table to allow for data filtering.
3. The dataset is saved in .xlsx format.
4. The xlsx-formatted file is opened in TSTool and a short command file [(Process-xlsx-to-csv.TSTool)](https://github.com/OpenWaterFoundation/owf-data-co-breweries/blob/master/analysis/Process-xlsx-to-csv.TSTool) converts the dataset into CSV format, to be used in additional data-processing steps.
5. The xlsx-formatted file is opened in TSTool and a short command file [(Process-xlsx-to-geojson.TSTool)](https://github.com/OpenWaterFoundation/owf-data-co-breweries/blob/master/analysis/Process-xlsx-to-geojson.TSTool) converts the dataset into GeoJSON format.  This step is optional and applicable for datasets in which a map will be created or if further processing will occur in GIS application such as QGIS.

	
## How to Use the Data ##

The Colorado Breweries dataset intends to provide a complete statewide list of breweries assembled from multiple sources.  There are identifiers for each brewery and the dataset allows cross-referencing the identifiers so that other datasets can be joined.  For example, the [Colorado Municipal Water Providers dataset](https://www.github.com/OpenWaterFoundation/owf-data-co-municipal-water-providers) uses municipal water provider identifiers and can be used to link to this dataset to provide information about water use or water quality.  

The Excel and csv files can be used as tabular datasets as is, to create filtered lists or to link to other datasets.  Data-processing software such as TSTool can be used to link this dataset to other datasets.  Datasets can be used within GIS software to create maps, which can indicate where beer production is concentrated.

The format and contents of the dataset will change over time.  It is recommended to save a copy of the dataset.


## Additional Resources ##
* [Brewers Association](https://www.brewersassociation.org/)
* [Colorado Brewers Guild](https://coloradobeer.org/)
* [BreWater](https://brewater.com/)
* [Colorado Craft Brews](http://www.coloradocraftbrews.com/)


## Disclaimer ##

OWF has created this initial dataset of Colorado breweries.  OWF will attempt to fill data gaps as the dataset is used for analysis and funding allows for more data review.  OWF provides no guarantee as to the accuracy of the data.  **Use this dataset at your own risk.**  OWF welcomes feedback to improve the dataset.

## License ##

The license is being determined.  All the data are public so there are not really any restrictions on use.

## Contributing ##

The Open Water Foundation created this dataset as a general resource with simple analyses.
If you use the dataset and have comments, please contact the maintainers and/or use the GitHub issues to provide feedback.

## Maintainers ##

Kristin Swaim (@kswaim, kristin.swaim@openwaterfoundation.org) is the primary maintainer at the Open Water Foundation.

Steve Malers (@smalers, steve.malers@openwaterfoundation.org) is the secondary contact.

## Contributors ##

None yet, other than OWF staff.
