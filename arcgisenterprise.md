# ArcGIS Enterprise administration ticks and tricks

## Logging into the Postgres database powering the backend ArcGIS DataStore

https://enterprise.arcgis.com/en/portal/latest/administer/windows/data-store-utility-reference.htm

1. Find the tools in C:\AGE\ArcGIS\DataStore\tools
1. Take the username
1. run command `listmanageduser.bat` and take the credentials and database name
1. run `allowconnection.bat <host name> <username> [<database>]` using the name discovered credentials from previous step. Example `allowconnection.bat localhost username`
1. Use PGAdmin or other software to connect and see inside the underlying postgres datastore. 
