# metadata_utils_arcpro
To include tools for documenting data in arcgis data models - shapefiles, feature classes, etc.

## xml_module
metdata_arcpro/python_toolboxes/xml_module</br>
**CONTENTS of directory:**</br>
*Note that the only two required files are `xml_module.pyt` and `xml_module.pyt.xml`; the latter only being necessary as it includes metadata with information for running the tool, the input parameters, etc.**
- xml_module.py</br>
- xml_module.py**t**</br>
identical to xml_module.py but with different file type.  Just a text file saved as a `.pyt`.  
- xml_module.xml_element_template.pyt.xml</br>
created automatically once tool is `Added` in ArcGIS Pro Catalog</br>
Step 1 of the tool - described below
- xml_module.define_xml_elements.pyt.xml</br>
created automatically once tool is `Added` in ArcGIS Pro Catalog</br>
Step 2 of the tool - described below
- xml_module.pyt.xml

## INSTRUCTIONS `xml_module` Toolbox:</br>
![toolbox screenshot](https://user-images.githubusercontent.com/48263393/232112338-81a2b313-310c-4132-ac13-2c724ca30ea1.jpg)

### Access Tool the `xml_module.pyt` toolbox:**</br>
- *Add* as a Python Toolbox in your ArcGIS Pro Catalog Toolbox dropdown</br></br>
OR</br></br>
- *Connect* via Catalog [Connect to a toolbox](https://pro.arcgis.com/en/pro-app/latest/help/projects/connect-to-a-toolbox.htm) </br>
### Using the tool
- **GENERAL WORKFLOW**</br> 
There are currently two tools in this toolbox (2023 April), which are to be used sequentially. `step1_attr_level_metadata` and `step2_attr_level_metadata`.  The basic simplified workflow is 1) output a table (csv) in step 1.  This will export a csv with all fields in the target feature class. 2) Fill out values for `attrdef` and `attrdefs` to define the fields of the feature class directly in the metadata.  The elements are The Definition and The Definition Source respectively.  For instance, the theoretical field `lot_size` in a county parcel dataset would have values of *the size of the residential lot as measured by survey crew* and *Ada County Assessor's Department* for `attrdef` and `attrdefs` respecively. </br></br>
### STEP BY STEP
:+1: **TOOL1: step1_attr_level_metadata** </br>
INPUTS:</BR>
- `Input Feature`: Use drop down to select a feature from map Table of Contents (TOC) or browse for shapefile or feature class elsewhere.</br>
- `csv_directory`: This tool returns a csv itemizing the fields of fc_in. This parameter is the path/to/the/directory/to/house/csv.</br>
- `csv_filename`:The filename of csv to be output. Can be <name_of_csv> or <name_of_csv>.csv.</br></br>

![xml_module_step1](https://user-images.githubusercontent.com/48263393/232112333-a144e80b-bf8f-4987-b22a-00e614d8b0b8.jpg)

**RUN** --> Returns a csv (csv_directory/csv_filename) with the below structure.</br> 
*Note that `attralias` will have values only if they are defined in the shapefile/FC.*</br>

| attrlabl | attralias | attrdef | attrdefs |
| ---- | ----| ---- | ---- |
| FID | FID |
| Shape | Shape | 
| name | name | 
| site_id | site_id |
| location | location |
| date_obs | date_obs |
| symb | symb |
| user_fld1 | user_fld1 |
| user_fld2 | user_fld2 |

:+1:**TOOL2: step1_attr_level_metadata** </br>
INPUTS:</BR>
- `fc_in`: Feature Class of interest for adding metadata. Can be feature class, shapefile, etc. Same FC from step1</br>
- `processing_dir`: Output directory. Required argument, but only relevant for a feature class as this directory will house an intermediary xml file to be used in importing updated metadata to the feature class. </br>
- `xml_csv`:path/to/populated/csv from previous step (step_1).</br></br>

![xml_module_step2](https://user-images.githubusercontent.com/48263393/232112347-77e4a504-629f-4e24-b53c-63ae8121e0af.jpg)

Prior to running tool, populate the blank columns - these values will be stamped into the metadata of target feature class or shapefile:</br>

| attrlabl | attralias | attrdef | attrdefs |
| ---- | ----| ---- | ---- |
| FID | FID | | |
| Shape | Shape | | |
| name | name | feature name | Mcmillen Corp |
| site_id | site_id | USGS historical site name | US Geological Survey | 
| location | location | relative location in relation to closest recognizable geographical feature | McMillen Corp |
| date_obs | date_obs | Date of data observation (YYYYMMDD) | McMillen Corp |
| symb | symb | Code (integer value) used to symbolize layer | McMillen Corp |
| user_fld1 | user_fld1 | Blank field to be populated by data collector | McMillen Corp |
| user_fld2 | user_fld2 | Blank field to be populated by data collector | McMillen Corp |

### Resultant Metadata
- *Note this is the intermediary xml created in step1, however the displayed portion is identical to the metadata created for the actual target FC or shapefile*</br>
- This *attribute level* metatdata can now be viewed in the feature's `Item Desciption` in ArcGIS Pro, Dekstop, Catalog, etc.</br></br>
![xml_module_xml_populated](https://user-images.githubusercontent.com/48263393/232112343-0cbe2034-f577-4099-97b1-e863f47f7334.jpg)









