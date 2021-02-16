# GPS/GNSS and Garmin IMG FAQ
There are various GPS formats supported by various Garmin and other GNSS devices. Here are some tips, tricks and frequently asked questions on how to work with files particularly creating and obtaining free IMG files. 

## GeoJSON to GPX
Handheld devices accept GPX files. GeoJSON is a common GIS format and can be created, tested and edited using https://geojson.io. 

A free tool to convert GeoJSON to GPX: http://aaronpdennis.github.io/geojson-to-gpx/ (source: https://github.com/aaronpdennis/geojson-to-gpx)

## Copy GPX to your device
Be sure your GPX file contains a single line representing a track or it will show up as many "tracks". 
1. Connect the GPS device through a USB cable to your computer.
1. The internal memory and/or the micro SD card will be detected as disk units.
1. Access internal memory 
1. Copy the trail file to D:\Garmin\GPX\ folder from your internal memory. 
1. Some GPS manufacturers hide this folder. Click on the "Show hidden files" on your computer settings to see them. 
1. On your GPS, go to your trails/tracks/trips section, and you are set to go!

## Create Garmin IMG

1. Install GPSMapEdit (https://www.geopainting.com/) and cGPSMapper (https://www.gpsfiledepot.com/tools/cgpsmapper.php). 
1. Open the GPX file in GPSMapEdit
1. With the GPX file open, go to File then Map Properties pull-down. 
1. On Header tab:
    1. Set the Type set to Garmin
    1. Set a unique 8-digit ID (numeric)
    1. Set a name (spaces ok)
1. On Levels tab:
    1. Insert Before 4 times to have 5 levels.
    1. Change each to have "bits" and "MapSource zoom" to levels that correspond. You must apply before the MapSource zoom range is editable (bug?)
    1. Set the Map is Transparent on  cGpsMapper tab. Apply and Close map properties
1. Select all TrackLogs on map (which GPX is imported as). Then right-click and convert to polyline. Select an appropriate type (walkway, road, etc)
1. File, Save As.. your "polish format" map. 
1. File, Export Garmin IMG then name your IMG file. Then locate your C:\Program Files (x86)\cGPSmapper\cgpsmapper.exe file and click Run. 

You now have an IMG file for your device! It will appear as a map on Garmin devices. 

## Free data sources for pre-created IMG files 

### OpenStreetMap

Generate an IMG file for anyplace on earth. The maps are meant to be generic and will probably provide best routing results for car-drivers, however other routing options should work reasonably well too.

http://garmin.openstreetmap.nl/

### OpenTopo Garmin IMG files

Routable and free, these almost rival the paid-Garmin maps using the OpenStreetMap and Shuttle Radar Topography Mission DEM data! File sizes are large but work very fast, and are routable (relatively, Garmin MapSource works better). 

https://garmin.opentopomap.org/#north_america

### Ibycus Canada Topgraphic IMG
Data sourced from Canada's Geogratis Website (The BNDT dataset from Department of Natural Resources Canada). This is essentially the data you get on the government issue 1:50,000 topo maps. The original source has been removed and you need to download it via torrent, but can easily find other sources online. 

http://www.ibycus.com/ibycustopo/ (download ISO from Google Drive: https://drive.google.com/file/d/0B_OuRuvqYnudZGRJZVFra3VsT0k/view)
