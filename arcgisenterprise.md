# ArcGIS Enterprise administration ticks and tricks

## Logging into the Postgres database powering the backend ArcGIS DataStore

https://enterprise.arcgis.com/en/portal/latest/administer/windows/data-store-utility-reference.htm

1. Find the tools in C:\AGE\ArcGIS\DataStore\tools
2. Take the username
3. run command `listmanageduser.bat` and take the credentials and database name
4. run `allowconnection.bat <host name> <username> [<database>]` using the name discovered credentials from previous step. Example `allowconnection.bat localhost username`
5. Use PGAdmin or ArcGIS pro to connect and see inside the underlying postgres datastore on TCP 9876. You can open and view spatial tables this way too. 
6. The PostgreSQL Client Authentication Configuration File can be modified directly for remote access \arcgisdatastore\pgdata\pg_hba.conf

