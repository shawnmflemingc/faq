# GPS/GNSS and Garmin Data FAQ
There are various GPS formats supported by various Garmin and other GNSS devices. Here are some tips, tricks and frequently asked questions on how to work with them. 
I work with:
* Bad Elf Surveyor and Pro (https://bad-elf.com/pages/compare)
* Trimble Nomad
* Garmin eTrex (yellow [original], blue [legend])
* Garmin GPSMAP 66s
* Garmin Dakota 20
* Garmin Fenix 3hr
* Garmin Nuvi, Drivesmart
* Garmin Striker 4 and 4cv+
* Internal GPS on various smartphones

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
  1. Change each to have "bits" and "MapSource zoom" to levels that correspond. 
1. Go to Levels tab
