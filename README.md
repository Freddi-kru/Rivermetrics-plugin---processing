# **RiverMetrics** - Qgis Processing

## Hydromorphological River Metrics Measurements 
![RM logo con ombra](other/icons&logos/RM2.png)

A set of tools for extracting river metrics. Useful for identifying the hydro-morphological characteristics and analysing the geomorphological evolution over time of a river.    
It is developed in [Python-3 environment](www.python.org) and is compatible with QGIS 3.22 and later.

The plugin is divided into two parts: the first part is an experimental plugin with a dock in the main QGIS interface, while the second part is a set of tools integrated into QGIS processing.

> [!Note]
> The [RiverMetrics plugin](https://github.com/pierluigiderosa/RiverMetrics.git) is in the official QGIS repository (experimental flag) and can be easily installed using the standard procedure. 

 The QGIS RiverMetrics processing tools can be found here.

---
## QGIS processing tools

The tools have been grouped into a set called **RM Hydromorphological Analysis**. The set consists of three tools, two of which are split into two parts. There are five QGIS models listed below:

* River axis extraction ;
* Braiding-width 1: measure;
* Braiding-width 2: reaches mean values;
* Valley confinement index 1: input data preparation
* Valley confinement index 2: calculation.
---
## How to install into the **QGIS processing panel**
Once you have downloaded and unzipped the **zip project file** (green code button at the top right of the page) there are two easy ways to import the models into QGIS.

### Copy the _.model3_ files in the Processing configuration folder 
The user profile configuration folders are directly accessible from the QGIS interface via the command bar: _Settings/User Profiles/Open Active Profile Folder_.

![aprire cartella del profilo](other/images/installazione.jpg)

The models are located in the **project's _"models"_ folder**. They have a _**.model3**_ extension. 
After copying the models files to the 
`.../user/processing/models` folder, you will need to restart the software and the tools will be listed in the Processing Toolbox.

### Adding using the Processing Toolbox button
Alternatively, the models can be added one by one to the Processing Toolbox using the button at the top left.

![processing toolbox button](other/images/pulsante_processing.jpg)

---
## River Axis Extraction
The riverbed axis is an input to both the RiverMetrics plugin and the Braid Width 1: Measure model.

### Concepts of river geomorphology
In geomorphology, the axis of the riverbed is defined as the median line formed by the points at the same distance from the banks. The axis is determined from the polygon of the bankfull riverbed.

The bankfull riverbed can be identified from remotely sensed imagery and includes the part of the riverbed comprising the channel(s) and the active (bare or sparsely vegetated) bars. The banks separate it from the floodplain and form its boundary. Also excluded are bars with tree vegetation, which are not considered active because they do not participate in sediment transport (bed load).

### Model operation

The first operation performed by the model is to eliminate from the polygon of the bankfull riverbed the holes caused by the presence of longitudinal tree bars, known as 'islands'. This requires a threshold (maximum area - SR units<sup>2</sup>), which is set to 5000 by default.

The axis is obtained by a process of "skeletonisation" of the polygon using the GRASS gis _**v.voronoi**_ tool present in the Processing Toolbox.

As the line obtained may be excessively fragmented, a simplification is carried out to remove nodes that are closer than a threshold (SR units) defined by the operator. The default value is 1.

As the resulting line may be split into several parts, the initial vertices of the lines are extracted to facilitate identification of the different parts. These must then be manually joined together by the operator (" editing" mode) to obtain a single line of a "single part" layer.
