# owf-data-co-breweries #

This repository contains the [Open Water Foundation (OWF)](http://openwaterfoundation.org) dataset for Colorado breweries.  According to the [Brewers Association](https://www.brewersassociation.org/directories/breweries/), there are 434 breweries in Colorado.  The beer industry is one of the major commercial water users in the state.  The goal of this dataset is to provide data about breweries, particularly data about water source and use, with the ultimate goal of gaining knowledge about water efficiency in the beer industry and relationships to local water supplies.  There is an increasing interest in understanding local water issues and water quality protection, from groups such as [BreWater](https://brewater.com/) in Northern Colorado, as well as using sustainable brewing practices (see the Brewers Association's Best Practices for [Sustainability](https://www.brewersassociation.org/best-practices/sustainability/)).
This is a foundational dataset that provides unique identifiers and other data for breweries and the identifiers can be used to link other datasets, such as municipal water providers.
OWF has created and is maintaining this dataset to facilitate work on various data analysis and visualization projects in Colorado.  **Note that this work is initially focused on the South Platte Basin and, in particular, the City of Fort Collins.  The dataset will continue to be filled in as time and resources permit.** 

The following sections provide a summary of the project repository:

* [Connections to the Colorado Water Plan and the Statewide Water Supply Initiative 2010](#connections-to-the-colorado-water-plan-and-the-statewide-water-supply-initiative-2010)
* [How to Use the Data](#how-to-use-the-data)
* [Repository Contents](#repository-contents)
* [Attribution](#attribution)
* [Data Workflow](#data-workflow)
* [Data Issues](#data-issues)
* [Additional Resources](#additional-resources)
* [Disclaimer](#disclaimer)
* [License](#license)
* [Contributing](#contributing)
* [Maintainers](#maintainers)
* [Contributors](#contributors)

## Connections to the Colorado Water Plan and the Statewide Water Supply Initiative 2010 ##
The [Colorado Water Plan (CWP)](https://www.colorado.gov/cowaterplan), completed in 2015, is "a roadmap that leads to a productive economy, vibrant and sustainable cities, productive agriculture, a strong environment and a robust recreation industry."  The plan lays the groundwork for the measurable outcomes, goals and actions required to ensure that the State's municipal, industrial, agricultural, environmental and recreational needs are preserved.  Beer brewing is one of Colorado's "large industries", along with manufacturing, mining and food processing.  Large industries are, in turn, a subsector of self-supplied industrial (SSI) water demands.  SSI demands include water use by self-supplied and municipal-provided industries.  Other subsectors of SSI include snowmaking, thermoelectric power generation at coal- and natural gas-fired facilities, and energy development, including the extraction and production of natural gas, coal, uranium and oil shale.
The [Statewide Water Supply Initiative 2010 (SWSI 2010)](http://cwcb.state.co.us/water-management/water-supply-planning/pages/swsi2010.aspx) provides an analysis of consumptive and nonconsumptive water needs, as well as projects and methods to meet those needs.  When describing municipal and industrial water use projections, only Coors Brewing Company is mentioned regarding the brewing industry (Appendix H, p.4-1).  This leaves a lot of room for improvement in understanding water use within the brewing industry.  Furthermore, while SSI demands are approximately only 10% of that demanded by municipal and industrial (M&I) demands in the South Platte basin, the demand is predicted to increase in the future (SWSI p.4-18).


## How to Use the Data ##

The Colorado Breweries dataset intends to provide a complete statewide list of breweries assembled from multiple sources.  There are identifiers for each brewery and the dataset allows cross-referencing the identifiers so that other datasets can be joined.  For example, the [Colorado Municipal Water Providers dataset](https://www.github.com/OpenWaterFoundation/owf-data-co-municipal-water-providers) uses municipal water provider identifiers and can be used to link to this dataset to provide information about water use or water quality.
Other potential uses of this dataset include the following.  Note that this largely requires the use of additional data that are not currently in the dataset.  Data issues are discussed in the Data Issues section.
* Creating a point map of breweries to indicate where beer production is concentrated.
* Creating a network graph of breweries and municipal water providers.  This can serve to help understand where breweries get their water and which municipal water providers are the largest suppliers to water to breweries.
* Creating a network graph of breweries and water sources (streams).  This can serve to help understand the rivers and creeks that supply water to breweries and can assist breweries in determining which streams they should support through conservation efforts.
* Creating a point map of breweries in which points are color-coded based on some measure of water quality.  This can assist breweries in determining which streams they should support through conservation or restoration efforts.
* Creating county choropleth maps that indicate annual beer production or sales totals.  This can serve to illustrate how the beer industry contributes to the economies of each county and the South Platte basin as a whole.
* Creating a [Gapminder-like bubble plot](https://www.gapminder.org/tools/#_chart-type=bubbles) of beer production and water use over time for each brewery.  This can serve to illustrate how beer production, water use and water efficiency have changed over time.  It can also highlight the number of breweries formed in recent years.
 
The Excel and csv files can be used as tabular datasets as is, to create filtered lists or to link to other datasets.  Data-processing software such as TSTool can be used to link this dataset to other datasets.

The format and contents of the dataset will change over time.  It is recommended to save a copy of the dataset.


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
* **OWF_ID** - unique text identifier created by OWF to ensure that a unique ID is available for every brewery
* **OWF_ID_Flag** - data status of OWF_ID values; see more detail below
* **BusinessEntity_ID** - state-assigned identification number for a business entity, from the Colorado Information Marketplace's [Business Entities in Colorado](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) dataset, to link state datasets
* **BusinessEntity_ID_Flag** - data status of BusinessEntity_ID values; see more detail below
* **Physical_Address** - street address of the physical location of the brewery; from the "Business Entities in Colorado" dataset or the brewery's website
* **Municipality** - municipality in which the brewery is located; from the "Business Entities in Colorado" dataset or the brewery's website
* **State** - state in which the brewery is located
* **ZipCode** - zip code in which the brewery is located; from the "Business Entities in Colorado" dataset or the brewery's website
* **Municipality_DOLA_LG_ID** - 5-digit identifier used by Colorado's [Department of Local Affairs (DOLA)](https://dola.colorado.gov/lgis/municipalities.jsf) for the municipality in which the brewery is located, to link DOLA datasets
* **Municipality_DOLA_LG_ID_Flag** - data status of Municipality_DOLA_LG_ID values; see more detail below
* **Municipal_WaterProvider_OWF_ID** - unique text identifier of the municipal water provider that provides water to the brewery; created by OWF
* **Municipal_WaterProvider_OWF_ID_Flag** - data status of Municipal_WaterProvider_OWF_ID values; see more detail below
* **Latitude** - latitude of brewery's point location in decimal degrees
* **Longitude** - longitude of brewery's point location in decimal degrees
* **Lat_Long_Flag** - indication of how latitude and longitude were determined; g1 = coordinates are based on the physical address of the brewery
* **WaterSource_GNIS_Name** - [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) name of the stream from which the brewery receives water, to link federal and state datasets
* **WaterSource_GNIS_Name_Flag** - data status of WaterSource_GNIS_Name values; see more detail below
* **WaterSource_GNIS_ID** - [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) identifier of the stream from which the brewery receives water, to link federal and state datasets
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
* The BusinessEntity_ID is from the Colorado Information Marketplace's [Business Entities in Colorado](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) dataset and is a state-assigned identification number.  Because this dataset was initialized from a small number of breweries, OWF manually searched for each brewery within the dataset to find the identifier.  This dataset is also the source for the Physical_Address, Municipality, State, ZipCode and Formation_Year data columns.  Note that the "Business Entities in Colorado" dataset also contains records for breweries that have dissolved, which is listed within the brewery's name.  This OWF dataset focuses only on active breweries.
* The Colorado Department of Local Affairs (DOLA)'s [Local Government Information System](https://dola.colorado.gov/lgis/counties.jsf) uses a local government ID (LG ID) for municipalities.  OWF is using DOLA_LG_ID instead of LG ID to add more description to the identifier.  DOLA_LG_IDs come from the [Colorado Municipalities](https://github.com/OpenWaterFoundation/owf-data-co-municipalities) dataset created by OWF.
* OWF created municipal water provider IDs in its [Colorado Municipal Water Providers](https://github.com/OpenWaterFoundation/owf-data-co-municipal-water-providers) dataset, to be able to link water provider data, such as water use.
* Each brewery has a physical address listed in the dataset, but not latitude/longitude coordinates.  To obtain coordinate data, the dataset was opened in [Google Sheets](https://www.google.com/sheets/about/).  An add-on named Geocode by Awesome Table can take a physical address and convert it to coordinates, as long as the street address, city, state and zip code are provided.
* The U.S. Geological Survey (USGS)'s [Geographic Names Information System (GNIS)](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) is the Federal and national standard for geographic nomenclature.  The USGS developed the GNIS in support of the U.S. Board on Geographic Names as the official repository of domestic geographic names data.  Most streams in Colorado have a GNIS Name and GNIS ID.  GNIS names and identifiers are also used within the [Source Water Route Framework](http://cdss.state.co.us/GIS/Pages/AllGISData.aspx), a spatial data layer that contains measured, named streams from the National Hydrography Dataset.
* Website URLs were found by manually searching for brewery websites.  If the brewery does not have a BusinessEntity_ID, then the website was also the source of data for the Physical_Address, Municipality, State and ZipCode data columns.


## Data Workflow ##
The general workflow is as follows once the basic dataset is created:
1. Data flags are created for many of the data columns that indicate data status as described above.
2. The data are formatted as a table to allow for data filtering.
3. The dataset is saved in .xlsx format.
4. The xlsx-formatted file is opened in TSTool and a short command file [(Process-xlsx-to-csv.TSTool)](https://github.com/OpenWaterFoundation/owf-data-co-breweries/blob/master/analysis/Process-xlsx-to-csv.TSTool) converts the dataset into CSV format, to be used in additional data-processing steps.
5. The xlsx-formatted file is opened in TSTool and a short command file [(Process-xlsx-to-geojson.TSTool)](https://github.com/OpenWaterFoundation/owf-data-co-breweries/blob/master/analysis/Process-xlsx-to-geojson.TSTool) converts the dataset into GeoJSON format.  This step is optional and applicable for datasets in which a map will be created or if further processing will occur in GIS application such as QGIS.


## Data Issues ##
To advance the utility of this dataset, the following data would be helpful:
* Beer Production, in gallons or barrels, annual totals
* Water Deliveries - amount of water delivered by the municipal water provider (water utility), annual totals
* Wastewater - amount of water returned to the stream, annual totals

From this data, consumptive use and water efficiency (number of gallons of water used per gallon of beer produced) could be calculated.  However, after discussing this dataset with a member of the brewing industry, the following points were brought up for consideration:
* With the possible exceptions of the larger breweries (New Belgium, Odell and Anheuser-Busch), it is unlikely that smaller breweries have the time or ability to collect this data.
* The less than 4:1 ratio of water consumption to beer production, an industry goal for sustainable water use, is very difficult for small breweries to achieve.  Many of the conservation and efficiency strategies available to larger breweries aren't options for smaller breweries and, even with diligent efforts, small breweries may only obtain a ratio of 7:1.
* The general public does not understand that a 4:1 ratio of water consumption to beer production is a very low ratio, even for other types of manufacturing.  There is a concern that the general public would think the smaller breweries are more wasteful and this public scrutiny is not desirable.
* Among Fort Collins breweries, the majority don't measure how much water enters or leaves their facility.  Most are on shared water supplies or shared meters in leased spaces and don't have a single meter coming into their facility.  Furthermore, many breweries would not wish to know how much water they use from a shared supply because water bills are currently evenly divided and not based on how much water is used.
* Of those Fort Collins breweries that do have the methods to measure the water coming into their facilities, only the larger breweries have multiple submeters to analyze water use in each process of beer production.

At this time, OWF is uncertain as to the likelihood of obtaining additional data related to water use. 


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
