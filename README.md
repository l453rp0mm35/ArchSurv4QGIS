ArchSurv4QGIS (AS4QGIS) is an open source solution for automated archaeological feature drawings from in-field GNSS / totalstation point measurements via QGIS.

It is a suite containing two algorithms: Synthesis and Psyche

They are designed as adjustable ".model3" algorithm pipelines.

------------------------------------------------------------------

What is ArchSurv4QGIS Synthesis?

AS4QGIS Synthesis works on the basis of point data exported as delimited text from a surveying device. 

ArchSurv4QGIS Synthesis processes 10-character pointID-strings: e. g. '0001A03001'
- feature '1'
- line container / point property 'A'
- shape type '03'
- sequence number '001'


Depending on the entered "shape type", AS4QGIS Synthesis generates four output datasets:
- polygons.shp
- polylines.shp
- pointdata.shp
- vertices.shp


shape type spectrum:
feature | '01' - heights, '02' - polyline, '03' - polygon, '33' - closed polyline
sample | '51' - sample point, '52' - sample polyline, '53' - sample polygon
posthole | '06' / '61' - buffered point measurement
finds | '71' - find point, '72' - find polyline, '73' - find polygon
3D markers | '81' - 3D marker point
trench | '91' - fixed point, '92' - trench polyline, '93' trench polygon
section nails | '00' - section nail point


What is ArchSurv4QGIS Psyche?
Psyche processes line and polygon features. It complements the AS4QGIS Synthesis algorithm by adding the same attribute structure to existing line or polygon measurements that Synthesis generates from point data. This enables seamless merging of survey datasets from different data sources to be combined and analyzed together.


AS4QGIS is free to use and fully customizable.

----------------------------------------------------------------------

AS4QGIS Synthesis Workflow

In-field

Survey Device Requirements:
Spatial data from any surveying device (e. g. a total station, a GNSS receiver, ...) can serve as a basis for further processing via AS4QGIS. The only requirement for the device is the ability to output the acquired point data as 'Delimited Text'.

ArchSurv-Code Guide:
AS4QGIS processes 10-digit pointID-strings according to the following scheme 'XXXXYZZ001', which must be entered into the point ID field of the surveying device.

XXXX | 4 digit long feature number.
It is possible to record up to 9999 features; e.g. '0001'.
Y | 1 letter long line container / point property 
Acts as a separator of two or more lines of the same feature / Acts as a property of a point measurement; e.g. 'A'.
ZZ | 2 digit long shape type
Defines the shape type of the current feature measurement; e.g. '03'.
001 | 3 digit long sequence number
The serial number of a line measurement should always start at '001'. The surveying device usually jumps one numerical value higher after each point measurement.


----------------------------------------------------------------------

Shape Type Spectrum

feature | '01' - heights, '02' - polyline, '03' - polygon
sample | '51' - sample point, '52' - sample polyline, '53' - sample polygon
posthole | '61' - buffered point measurement
finds | '71' - find point, '72' - find polyline, '73' - find polygon
3D markers | '81' - 3D marker point
trench | '91' - fixed point, '92' - trench polyline, '93' trench polygon
section nails | '00' - section nail point


----------------------------------------------------------------------

Point Properties:
While letters act as line containers for polyline and polygon measurements, sample, posthole, and finds point measurements can be assigned point properties using letters.

sample
If ‘A’ is entered as point property for a sample measurement the property is considered ‘not declared’.
'A' - undeclared-sample; 'B' - brick-sample; 'C' - c14-sample; 'D' - dendro-sample; 'E' - soil_bulk_sample; 'F' - soil_block_sample; 'G' - soil_core_sample; 'H' - soil_monolith_sample; 'I' - soil_kubiena_sample; 'J' - soil_waterlogged_sample; 'K' - excav.specif.meth.1; 'L' - excav.specif.meth.2; 'M' - excav.specif.meth.3; 'N' - excav.specif.meth.4; 'O' - excav.specif.meth.5; 'P' - excav.specif.meth.6; 'Q' - excav.specif.meth.7; 'R' - excav.specif.meth.8; 'S' - excav.specif.meth.9; 'T' - excav.specif.meth.10; 'U' - excav.specif.meth.11; 'V' - excav.specif.meth.12; 'W' - excav.specif.meth.13; 'X' - excav.specif.meth.14; 'Y' - excav.specif.meth.15; 'Z' - excav.specif.meth.16  

posthole
It is only mandatory to specify the point property in the case of plug hole measurements (shape type ‘61’). Based on a central measurement, the model generates a buffer with the diameter specified by the point property. 
'A' - 1 cm; 'B' - 2 cm; 'C' - 3 cm; 'D' - 4 cm; 'E' - 5 cm; 'F' - 6 cm; 'G' - 7 cm; 'H' - 8 cm; 'I' - 9 cm; 'J' - 10 cm; 'K' - 11 cm; 'L' - 12 cm; 'M' - 13 cm; 'N' - 14 cm; 'O' - 15 cm; 'P' - 16 cm; 'Q' - 17 cm; 'R' - 18 cm; 'S' - 19 cm; 'T' - 20 cm; 'U' - 21 cm; 'V' - 22 cm; 'W' - 23 cm; 'X' - 24 cm; 'Y' - 25 cm; 'Z' - 26 cm   

finds
If ‘A’ is entered as point property for a finds measurement the property is considered ‘not declared’.
'A' - undeclared; 'B' - metal; 'C' - coin; 'D' - stone_object; 'E' - silex; 'F' - iron; 'G' - glass; 'H' - homo; 'I' - animal_bones; 'J' - architectural_ceramics; 'K' - ceramics; 'L' - burnt_daub; 'M' - mortar; 'N' - slag; 'O' - organic; 'P' - excav.specif.cat.1; 'Q' - excav.specif.cat.2; 'R' - excav.specif.cat.3; 'S' - excav.specif.cat.4; 'T' - excav.specif.cat.5; 'U' - excav.specif.cat.6; 'V' - excav.specif.cat.7; 'W' - excav.specif.cat.8; 'X' - excav.specif.cat.9; 'Y' - excav.specif.cat.10; 'Z' - misc

----------------------------------------------------------------------

Example Codes
'0037A03005' | The 5th point measurement of a polygon around feature 37.
'0037A02027' | The 27th point measurement of a polyline within feature 37.
'0037B02003' | The 3rd point of a second polyline within feature 37.
'0037B01006' | The 6th height point of feature 37.
'0123C51056' | The 56th sample of the excavation. This is a C14 sample from feature 123.
'0090A53004' | The 20th point measurement of a sample-polygon.
'0061D61003' | The 3rd peg hole measurement of feature 61. This peg hole has a diameter of 4 cm.
'0467E71537' | The 537th finds point measurement of the excavation. The find comes from feature 467 and is a flint stone.
'1729A72013' | The 13th point measurement of a finds-polyline. The documented find is located within feature 1729.
'0404A81008' | The 8th 3D marker for the documentation of feature 404.
'0000A91027' | Fixed point number 27. It is advised to record fixed points, other trench related measurements, and finds from unknown contexts within 'pseudo'-feature '0000' or '9999'.
'0000A92045' | The 45th point measurement of a polyline of the excavation boundary.
'0738A33002' | The second point of a closed polyline, which will be displayed in QGIS as a polyline rather than a polygon.

----------------------------------------------------------------------

How to Correctly Collect Spatial Data:

The application of diverse measurement strategies during fieldwork leads to ideal mapping results in subsequent ArchSurv4QGIS post-processing. These are considered "best practices."

- Different lines cannot be measured using the same ArchSurv string. (!!!)
- Closed lines '03', i.e. polygons, should indicate the largest dimensions of the feature. This means that for a wall that spreads downwards, the lower edges of the wall should ideally be measured as closed polygons '03', while the upper edges should be measured as open polylines '02'.
- Line measurements for finds '72', '73' and samples '52', '53' should also be supplemented with a point measurement '71' or '51' within the polyline or polygon measurement.
- Find point measurements '71' and sample measurements '51' can be assigned additional properties on-site using the 5th character [0000'X'71037] of the 10-character ArchSurv-string. If you do not want to specify any additional properties, use the letter 'A'. This corresponds to the value 'undeclared'.
- Plughole measurements '61' are performed using a centrally placed point. The diameter of the plughole is given by the 5th character [e.g., 0007'C'51001] of the ArchSurv character string. For surveying efficiency, it is recommended to group the plughole measurements according to their different diameters.
- Excavation boundaries '92' and '93' are ideally measured under the layer ID '0000' or '9999' [e.g., 0000'C'51001]. 0000A93001]. The label field should contain the trench name.
- Closed lines that should not be in the polygon.shp layer but in the polyline.shp layer can be measured under the "shape type" code '33'.

In-office

Type of Input Data

ArchSurv4QGIS Synthesis processes delimited Text imported into QGIS as point data with X, Y, and Z values ​​using the "Delimited Text" import function. The file format and the delimiter type of the exported file from the surveying device are insignificant. The exported file should simply be in a format generally readable by QGIS (e.g., .csv, .txt, .asc, etc.) and contain a "point_ID" attribute and a "code" attribute:

- "point_ID" contains the "ArchSurv-String"

- "code" contains additional feature-information

----------------------------------------------------------------------

Import Input Data

First, the desired text file should be imported into QGIS. Follow these steps:
1 | Click the "Open Data Source Manager" icon. Select the "Delimited Text" option. Use the "[...]" icon to the right of the "File name" field to locate the text file you want to import.

2 | Under File Format, select "Custom delimiters". Here you can set the "Delimiter" used in the text file. If the correct delimiter has been selected, the data should already be displayed as a table under "Sample Data."

3 | Under "Geometry Definition," select the "Point Coordinates" option. Here, select the x, y, and z coordinates from the table. The following applies:
X field: 'easting'
Y field: 'northing'
Z field: 'elevation'
Under "Geometry CRS", select the coordinate reference system used to record the point coordinates.

4 | Click "Add". Your text file should now be imported with point coordinates.

----------------------------------------------------------------------

Start AS4QGIS Synthesis

1 | Start AS4QGIS Synthesis by double-clicking.
2 | Select the text file you want to edit.
3 | Click "Run."
4 | AS4QGIS Synthesis will generate four virtual layers. Review your datasets and save them, or add them to your overall project using "copy and paste."

Note: All point measurements with IDs that do not begin with four digits, as specified by the ArchSurv code, will be filtered out by the algorithm and excluded from the output data.

----------------------------------------------------------------------


Output Shapefiles

Starting from the input file, AS4QGIS Synthesis generates four shapefiles based on the 'shape type' defined in-field on the surveying device. These include the following shape types:
vertices | All measurement points that do not serve any further function than being vertex points of polylines or polygons.
pointdata | '00', '01', '51', '71', '81', '91'
polylines | '00', '02', '33', '52', '72', '92'
polygons | '03', '53', '61', '73', '93'


----------------------------------------------------------------------


vertices

point-ID | the original ID of the point measurement as entered on the surveying device.
x | the x/easting value of the point measurement.
y | the y/northing value of the point measurement.
z | the z/elevation value of the point measurement.
code | the 'label/code' of the point measurement as entered on the surveying device.
ID | the identifier of the feature.
shptype | the shape type as an integer.
maxH | maximum elevation value of a feature.
minH | minimal elevation value of a feature.
maxHtemp | pseudo-date of the maximum elevation value of a feature.
minHtemp | pseudo-date of the minimal elevation value of a feature.
originfile | the file name of the processed 'delimited text'.
of_espg | the epsg of the input_layer.
IDstring | the identifier of the feature (string) as entered on the surveying device.
ID_code | A composite identifier consisting of the 'IDstring' and the 'code' attribute fields.
code_ID | A composite identifier consisting of the 'code' and the 'IDstring' attribute fields.


----------------------------------------------------------------------

pointdata

ID | the identifier of the feature.
code | the 'label/code' of the point measurement as entered on the surveying device.
shptype_n | the shape type as a string corresponding to the shape type integer.
shptype | the shape type as an integer.
point-prop | the property of a plug hole, sample, or find measurement.
find-nr. | the consecutive find number within an excavation.
sample-nr. | the consecutive sample number within an excavation.
f_ma/s_me | the finds material or sample method as text according to field "point-prop".
contin-nr. |  the consecutive measurement number as assigned by the surveying device..
point-ID | the original ID of the point measurement as entered on the surveying device.
x | the x/easting value of the point measurement.
y | the y/northing value of the point measurement.
z | the z/elevation value of the point measurement.
maxH | maximum elevation value of a feature.
minH | minimal elevation value of a feature.
maxHtemp | pseudo-date of the maximum elevation value of a feature.
minHtemp | pseudo-date of the maximum elevation value of a feature.
originfile | the file name of the processed 'delimited text'.
of_espg | the epsg of the input_layer.
IDstring | the identifier of the feature (string) as entered on the surveying device.
ID_code | A composite identifier consisting of the 'IDstring' and the 'code' attribute fields.
code_ID | A composite identifier consisting of the 'code' and the 'IDstring' attribute fields.

----------------------------------------------------------------------

polylines

ID | the identifier of the feature.
code | the 'label/code' of the point measurement as entered on the surveying device.
shptype | the shape type as an integer.
maxH | maximum elevation value of a feature.
minH | minimal elevation value of a feature.
maxHtemp | pseudo-date of the maximum elevation value of a feature.
minHtemp | pseudo-date of the maximum elevation value of a feature.
originfile | the file name of the processed 'delimited text'.
of_espg | the epsg of the input_layer.
IDstring | the identifier of the feature (string) as entered on the surveying device.
ID_code | A composite identifier consisting of the 'IDstring' and the 'code' attribute fields.
code_ID | A composite identifier consisting of the 'code' and the 'IDstring' attribute fields.

----------------------------------------------------------------------

polygons

ID | the identifier of the feature.
code | the 'label/code' of the point measurement as entered on the surveying device.
shptype | the shape type as an integer.
maxH | maximum elevation value of a feature.
minH | minimal elevation value of a feature.
maxHtemp | pseudo-date of the maximum elevation value of a feature.
minHtemp | pseudo-date of the maximum elevation value of a feature.
originfile | the file name of the processed 'delimited text'.
of_espg | the epsg of the input_layer.
IDstring | the identifier of the feature (string) as entered on the surveying device.
ID_code | A composite identifier consisting of the 'IDstring' and the 'code' attribute fields.
code_ID | A composite identifier consisting of the 'code' and the 'IDstring' attribute fields.

----------------------------------------------------------------------

Temporal Controller

Synthesis and Psyche generate the pseudo-data fields “maxHtemp” and “minHtemp” based on the attribute fields “maxH” and “minH”. In other words, the minimum and maximum elevation values of a feature measurement are translated into a date.

The following rules apply to this pseudo-date conversion:

Year: The meter value of the elevation + 1000

Month: Determined by the centimeter value of the elevation, where:

<10 cm = January

<20 cm = February

<30 cm = March

<40 cm = April

<50 cm = May

<60 cm = June

<70 cm = July

<80 cm = August

<90 cm = September

>90 cm = October

Day: Always set to '1'

Because “maxHtemp” and “minHtemp” provide a pseudo time range, you can use the "Temporal Controller Panel" and its slider to filter and view features based on their elevation values.

To activate the time component, double-click on one of the datasets in the “Layers” panel. In the now-visible “Layer Properties” window, click on “Temporal” (clock icon) and enable the checkbox “Dynamic temporal control.”

If no default settings are visible, enter the following:

Configuration: Separate fields for start and end date/time

Extent: Include start, Include end

Start field: minHtemp

End field: maxHtemp

Click [Apply] and then [OK].

In the “Map Navigation Toolbar,” click on “Temporal Controller” (clock icon). In the “Temporal Controller Panel”, click on “Animated temporal navigation.” Now use the slider to set a time value “t.”
If no changes are visible, you may need to click the blue refresh icon “Set to Full Range.”


All features will be displayed that have a pseudo time range (i.e. an elevation range) which includes the selected time “t.”


----------------------------------------------------------------------

Qgis2threejs as a Useful Plugin

A visual confirmation that the algorithm-generated outputs are truly three-dimensional datasets can be obtained either through a .dxf export or by using the Qgis2threejs plugin.

The Qgis2threejs extension can be found and installed from the menu bar under "Plugins" > "Manage and Install Plugins...", then by searching "qgis2threejs" in the search field.

Once installed, click the Qgis2threejs icon and, in the opened viewer, select your polygon and polyline datasets by checking the corresponding checkboxes.

You will then see an interactive, rotatable 3D view of your measurements.


----------------------------------------------------------------------


CAD-Export

AS4QGIS output files can be converted to a CAD format using the QGIS internal function "Project" - "Import/Export" - "Export Project to DXF...".
First, select a save location. Under "Output Layer Attribute" (you must scroll to the right to see this), select the desired attribute according to which the layers should be created in the DXF. Depending on your requirements, it is recommended to use either "ID", "IDstring", or "CAD-ID" as the layer attribute for the shapefiles "polylines.shp" and "polygons.shp". To export the point measurements "pointdata.shp" grouped by their properties, it is recommended to export using the attribute "shptype_n".
The "Symbology mode" should be 'Symbol Layer Symbology'.
The "Encoding" should be 'ISO-8859-1' (or if you work in the .gpkg-format: 'Big5').
Check the "Export labels as MTEXT elements" checkbox.

Click "OK." Your DXF has been generated.

