---
layout: default
title: Akron "Unbuildable" Lots
permalink: /projects/akron_unbuildable
---
# Akron "Unbuildable" Lots
### [Repository for this project accessible here](https://github.com/gracejulien/unbuildable/tree/main){:target="_blank" rel="noopener noreferrer"}.

The City of Akron offers city-owned vacant residential lots [for sale to residents](https://www.akronohio.gov/cms/site/96eb9cb67e2b1ccd/index.html#Unbuildable%20Parcel){:target="_blank" rel="noopener noreferrer"}. The City offers two categories of vacant lots: “buildable,” and “unbuildable.”
[Buildable parcels](https://www.akronohio.gov/cms/site/96eb9cb67e2b1ccd/index.html#Unbuildable%20Parcel){:target="_blank" rel="noopener noreferrer"} are defined as lots “having a minimum of 50-foot frontage and a lot size of greater than 5,000 sq. ft.” The City sells these parcels at $0.50 per square foot.
[Unbuildable parcels](https://www.akronohio.gov/cms/site/96eb9cb67e2b1ccd/index.html#Unbuildable%20Parcel){:target="_blank" rel="noopener noreferrer"} are defined as lots “having less than a 50-foot frontage.” The City sells these parcels at $0.05 per square foot.

Buildable parcels are considered development-ready, and are priced higher. Unbuildable parcels are treated as surplus land, and thus without significant value.

This distinction clearly influences the shape and character of future redevelopment in the city.

Spending time in Akron’s older neighborhoods reveals a large number of houses on small lots. I was curious to see how many residential buildings are located on “unbuildable” lots.

The answer is quite a few.

To understand just how many, I began working in Python.

First, I downloaded parcel characteristics from the Summit County Fiscal Office's Data Downloads website. I used [PARDAT](https://fiscaloffice.summitoh.net/index.php/documents-a-forms/viewdownload/10-cama/236-sc705pardat){:target="_blank" rel="noopener noreferrer"} and [LAND](https://fiscaloffice.summitoh.net/index.php/documents-a-forms/viewdownload/10-cama/271-sc709land){:target="_blank" rel="noopener noreferrer"}. This data allowed me to access the Land Use Codes (LUCs), building values, frontages, square footage, and other useful information for parcels.

I combined the two datasets from the Summit County Fiscal Office to create a dataset with attributes from both for every residential parcel in the city, and used [tax parcel](https://data-summitgis.opendata.arcgis.com/datasets/summitgis::parcels-web-geodata-tax-parcels/explore){:target="_blank" rel="noopener noreferrer"} and [jurisdiction](https://data-summitgis.opendata.arcgis.com/datasets/summitgis::jurisdictions-2/explore){:target="_blank" rel="noopener noreferrer"} data from County of Summit GIS.

I then filtered this dataset down to only include F type parcels, which are parcels that the County provides a measure of the frontage for. They are typically residential. The County divides parcels into three groups: F type, for frontage, S type, for square footage, and A type for acreage. This left only parcels for which there was frontage information.

I then further filtered the dataset, removing all parcels that had frontage greater than 45 ft or less than 25 ft. I chose these bounds to exclude very small and irregular parcels and to provide a margin of error at the upper bound.

This produced a dataset of "unbuildable" residential parcels in the City of Akron.

I then used the building value to distinguish between parcels that are vacant and parcels that have a residential building by creating a new Boolean vacancy column. If a parcel has a building value of 0, I considered it vacant, and set the Vacancy value to True for that parcel. If the parcel has a building value greater than 0, it has a residential building, and I set the Vacancy value to False.

The code described above is located [here](https://github.com/gracejulien/unbuildable/blob/main/generate_data.ipynb){:target="_blank" rel="noopener noreferrer"}.

This dataset of “unbuildable” parcels was then used to produce the maps below.

The static maps were created using QGIS (file located [here](https://github.com/gracejulien/unbuildable/blob/main/map.qgz){:target="_blank" rel="noopener noreferrer"}). The dynamic map at the bottom of the page was created using GeoPandas and Folium in Python (code located [here](https://github.com/gracejulien/unbuildable/blob/main/generate_visuals.ipynb){:target="_blank" rel="noopener noreferrer"}), and the parcels highlighted in it can be clicked on for information on the parcel, including Land Use Code, building value, and frontage.

This dataset revealed that there are 21,606 “unbuildable” lots with residential buildings on them in the city.

There are an additional 6,285 vacant parcels that are considered “unbuildable.”

Six hundred of those vacant parcels have been assigned Land Use Code 640, which means that they are owned by the City.



![Akron](./unbuildable_images/Akron.png)

![HS](./unbuildable_images/Highland_Square.png)

![Ellet](./unbuildable_images/Ellet.png)

![NH](./unbuildable_images/North_Hill.png)

![LD](./unbuildable_images/Laird_Dudley.png)

![Kenmore](./unbuildable_images/Kenmore.png)

<iframe src="front_all.html" height="700" width="900"></iframe>
