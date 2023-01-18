# ArcGIS Enterprise administration ticks and tricks

## Installation of Portal tricks to avoid DNS problems

From https://enterprise.arcgis.com/en/portal/latest/install/windows/installing-portal-for-arcgis.htm:
Create `C:\Dir\ArcGIS\Portal\framework\etc\hostname.properties` with entry `hostname=full.dns.name` to override it using the machine name
Modify `C:\Dir\ArcGIS\Portal\framework\runtime\ds\framework\etc\hostidentifier.properties` uncomment and set `hostidentifier=` to DNS name

Copy same hostname.properties file in both ArcGIS Server (C:\Dir\ArcGIS\framework\etc) and DataStore (C:\Dir\ArcGIS\DataStore\framework\etc)

From ArcGIS Server https://enterprise.arcgis.com/en/server/latest/deploy/windows/multiple-nic-cards-dns-entries.htm and Data Store https://enterprise.arcgis.com/en/portal/latest/administer/windows/create-data-store.htm#ESRI_SECTION2_0959726881944C3483C5DF63FBE1553A

These following items require local administrative access to the machine. 
None of the settings are sanctioned by Esri and most are unsupported -- DO SO AT YOUR OWN RISK. 

## Logging into the Postgres database powering Portal's item catalog and configuration

This is not supported by esri. 

1. The username and password will be the same user initially created to deploy the portal. Usually this is the administrator. 
2. The postgres is running on TCP 7654. 
3. Configuration for the postgres is located at `C:\AGE\arcgisportal\db`. The PostgreSQL Client Authentication Configuration File `C:\AGE\arcgisportal\db\pg_hba.conf`

## Logging into the Postgres database powering the backend ArcGIS DataStore

https://enterprise.arcgis.com/en/portal/latest/administer/windows/data-store-utility-reference.htm

1. Find the tools in C:\AGE\ArcGIS\DataStore\tools
2. Take the username
3. run command `listmanageduser.bat` and take the credentials and database name
4. run `allowconnection.bat <host name> <username> [<database>]` using the name discovered credentials from previous step. Example `allowconnection.bat localhost username`
5. Use PGAdmin or ArcGIS pro to connect and see inside the underlying postgres datastore on TCP 9876. You can open and view spatial tables this way too. 
6. The PostgreSQL Client Authentication Configuration File can be modified directly for remote access `\arcgisdatastore\pgdata\pg_hba.conf`

Using the connections in ArcGIS Pro: `agename,9876` for the DataStore
