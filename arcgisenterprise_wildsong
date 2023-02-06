-- Copied from https://wiki.wildsong.biz/index.php/ArcGIS_Enterprise

2021-12-20 Testing installation of 10.9.1 on Windows.

2019-Oct-25 Have to use ArcGIS Enterprise at work. Have to learn to have fun with it. Discovered command line scripts exist even in Windows version!

2019-Jan-09 (If you have ESRI licenses to run in the cloud) I found this (slightly outdated) set of class notes on running AGE on Amazon AWS: https://www.e-education.psu.edu/geog865 I say "outdated" because they've changed how you deploy to use this [http://enterprise.arcgis.com/en/server/latest/cloud/amazon/arcgis-enterprise-cloud-builder-cli-for-aws.htm CLI utility.]

2018-May-05 I am tired of jumping through hoops and my license runs out in a month anyway, so skip it. Won't renew. Using [[PostGIS]] and its friends from now on. See also [[Boundless stack]].

2018-Apr-29 Today I am installing the "ArcGIS Enterprise Builder for Linux" version 10.6 into a virtual machine running Ubuntu 16.04, on [[Bellman]].

== Currently using 10.9+ ==

=== How to restart ===

I am tired of rebooting the entire VM whenever AGE gets locked up.
With the Linux version there are scripts but in Windows world, remote into the server and

 Control Panel -> Administrative Tools -> Services

then pick your poison, right click, restart.

* ArcGIS Data Store
* ArcGIS Server
* Portal for ArcGIS

=== ArcGIS Portal ===

There is a PostgreSQL instance running on port 7654 and you can log into it using the site administrative account and password,
whatever you chose and installation time.

<pre>
c:\Program Files\ArcGIS\Portal\framework\runtime\pgsql\bin>psql -p 7654 -U CCGISadmin postgres
Password for user CCGISadmin:
psql (12.4)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# \l
                                                    List of databases
   Name    |   Owner    | Encoding |          Collate           |           Ctype            |     Access privileges
-----------+------------+----------+----------------------------+----------------------------+---------------------------
 gwdb      | CCGISadmin | UTF8     | English_United States.1252 | English_United States.1252 |
 postgres  | CCGISadmin | UTF8     | English_United States.1252 | English_United States.1252 |
 template0 | CCGISadmin | UTF8     | English_United States.1252 | English_United States.1252 | =c/CCGISadmin            +
           |            |          |                            |                            | CCGISadmin=CTc/CCGISadmin
 template1 | CCGISadmin | UTF8     | English_United States.1252 | English_United States.1252 | CCGISadmin=CTc/CCGISadmin+
           |            |          |                            |                            | =c/CCGISadmin
(4 rows)


postgres=#
</pre>

User accounts (and many other things) are stored in gwdb. I can connect to the account and list out the table for example.

<pre>
\c gwdb
SELECT username FROM gw_users WHERE role='account_admin';
\dt
\d gw_groups
SELECT title,owner FROM gw_groups WHERE owner NOT LIKE 'esri%';
</pre>


==== Where do files get stored?? ====

'''Image files'''

If you upload a file (say, an image) in Portal using "Add from computer", you can reference it using a URL for example to use it as a thumbnail.
It will be assigned a GUID and then stored in C:/arcgis/arcgisportal/content/items/495fe19ccfb847a286f8b4e98a400e16/download.jpg
When you use this method you can get the URL from Portal too, in this case it's
https://delta.co.clatsop.or.us/portal/sharing/rest/content/items/495fe19ccfb847a286f8b4e98a400e16/data
Curiously there is no indication in the URL that the item is an image. It's just "data".
The REST API exposes information about the image as https://delta.co.clatsop.or.us/portal/sharing/rest/content/items/495fe19ccfb847a286f8b4e98a400e16

Note if you change its name when you upload it, it will not rename the file. So if you tell Portal the name is "House" that's what you will see
in Portal but the actual file will still be house_over_water.png

If you upload a thumbnail directly, for example, for a map from its "details" page, the file gets uploaded to the folder that has the map in it,
for example, in C:/arcgis/arcgisportal/content/items/0b842b314c27452ca372561b3078f44d/esriinfo/thumbnail/house_over_water_orig.png
and a new, thumbnail sized version (200 x 133) will be saved as house_over_water.png

=== ArcGIS DataStore ===

FAIL: The WEB GUI for the DataStore says there is already a relational store but will not let me connect to it because it's already there. 

Relational data is stored in postgresql in c:\arcgis\arcgisdatastore\pgdata and commands are in c:\arcgis\arcgisdatastore\pgsql10.6\bin 
Note that the "10.6" here refers to the version of Postgres not the version of ArcGIS.

Tile caches are stored in hashed files in c:\arcgis\arcgisdatastore somewhere... not sure if I care really. Caches are boring.

"Scenes" are stored in couchdb (nosql) on my server they are in c:\arcgis\arcgisdatastore\nosqldata. I have not worked with Scenes yet so no more info here from me.

See c:\Program Files\ArcGIS\DataStore\, for example this command will reveal the location of the data files on your server, I suppose it varies...

 '''cat "$AGSDATASTORE"/etc/arcgis-data-store-config.properties'''
 #Thu Oct 24 10:58:06 PDT 2019
 dir.data=C\:/arcgis/arcgisdatastore/

I can use psql! I can use pg_config, see? 

<pre>
cd /c/arcgis/arcgisdatastore/pgsql12.4/bin
./pg_config
BINDIR = C:/arcgis/ARCGIS~3/pgsql12.4/bin
DOCDIR = C:/arcgis/arcgisdatastore/pgsql12.4/doc
HTMLDIR = C:/arcgis/arcgisdatastore/pgsql12.4/doc
INCLUDEDIR = C:/arcgis/arcgisdatastore/pgsql12.4/include
PKGINCLUDEDIR = C:/arcgis/arcgisdatastore/pgsql12.4/include
INCLUDEDIR-SERVER = C:/arcgis/arcgisdatastore/pgsql12.4/include/server
LIBDIR = C:/arcgis/ARCGIS~3/pgsql12.4/lib
PKGLIBDIR = C:/arcgis/ARCGIS~3/pgsql12.4/lib
LOCALEDIR = C:/arcgis/ARCGIS~3/pgsql12.4/share/locale
MANDIR = C:/arcgis/arcgisdatastore/pgsql12.4/man
SHAREDIR = C:/arcgis/ARCGIS~3/pgsql12.4/share
SYSCONFDIR = C:/arcgis/arcgisdatastore/pgsql12.4/etc
PGXS = C:/arcgis/arcgisdatastore/pgsql12.4/lib/pgxs/src/makefiles/pgxs.mk
CONFIGURE = --enable-thread-safety --enable-nls --with-ldap --with-openssl --with-ossp-uuid --with-libxml --with-libxslt
 --with-icu --with-tcl --with-perl --with-python
CC = not recorded
CPPFLAGS = not recorded
CFLAGS = not recorded
CFLAGS_SL = not recorded
LDFLAGS = not recorded
LDFLAGS_EX = not recorded
LDFLAGS_SL = not recorded
LIBS = not recorded
VERSION = PostgreSQL 12.4
</pre>

But what port is it running on? This doc says what 
[https://enterprise.arcgis.com/en/portal/latest/administer/windows/ports-used-by-arcgis-data-store.htm ports are in use]

Lots of juicy information in /c/arcgis/arcgisdatastore/etc/arcgis-data-store-config.json, to wit:
<pre>
cat arcgis-data-store-config.json
{
  "datastore.release": "10.9.0.26417",
  "datastore.release.configstore": "1.4",
  "dir.data": "C:\\arcgis\\arcgisdatastore\\",
  "dir.staging": "C:\\arcgis\\arcgisdatastore\\staging",
  "dir.temp": "C:\\arcgis\\arcgisdatastore\\temp",
  "dir.logs": "C:\\arcgis\\arcgisdatastore\\logs",
  "port.http": 9080,
  "port.https": 2443,
  "port.jmx": 9099,
  "machine.name": "CC-GIS.CLATSOP.CO.CLATSOP.OR.US",
  "webserver.maxheapsize": 512,
  "diskThreshold.warning": 10240,
  "diskThreshold.readonly": 1024,
  "features": {
    "feature.egdb": true,
    "feature.nosqldb": true,
    "feature.bigdata": false
  },
  "log.activeManager": "relational",
  "machine.initstarttime": 1622419481163,
  "serverRole": "Hosted"
}
</pre>

At 10.7 it had more, like this.

 {
  "datastore.release": "10.7.1.11595",
  "datastore.release.configstore": "1.4",
  "dir.data": "C:\\arcgis\\arcgisdatastore\\",
  "dir.staging": "C:\\arcgis\\arcgisdatastore\\staging",
  "dir.temp": "C:\\arcgis\\arcgisdatastore\\temp",
  "dir.logs": "C:\\arcgis\\arcgisdatastore\\logs",
  "port.http": 9080,
  "port.https": 2443,
  "port.jmx": 9099,
  "machine.name": "CC-GIS.CLATSOP.CO.CLATSOP.OR.US",
  "webserver.maxheapsize": 512,
  "diskThreshold.warning": 10240,
  "diskThreshold.readonly": 1024,
  "store.relational": {
    "datastore.release": "10.7.1.11595",
    "datastore.release.configstore": "1.4",
    "datastore.name": "ds_atjwr8b3",
    "dir.dbdata": "C:\\arcgis\\arcgisdatastore\\pgdata",
    "datastore.release.pg": "10.6",
    "datastore.release.sde": "10.7.1",
    "datastore.release.geometry": "1.25.1.4",
    "datastore.release.geometrylib": "1.25.1.4",
    "replication.role": "PRIMARY",
    "replication.method": "ASYNC",
    "dir.backup": "C:\\arcgis\\arcgisdatastore\\backup\\relational",
    "dir.backup.isshared": "false",
    "db.host": "CC-GIS.CLATSOP.CO.CLATSOP.OR.US",
    "db.port": 9876,
    "datastore.admindb": "dsadmindb",
    "datastore.lastknownstatus": "Started",
    "localstore.lastknownstatus": "Started",
    "datastore.initstarttime": 1519164852935,
    "datastore.manageddb": "db_0eoas",
    "datastore.registered": true,
    "lastLogScan": 1574755237952
  },
  "healthcheck.enable": true,
  "features": {
    "feature.egdb": true,
    "feature.nosqldb": true,
    "feature.bigdata": false
  },
  "store.tilecache": {
    "datastore.release": "10.7.1",
    "datastore.release.configstore": "1.4",
    "datastore.release.couchdb": "2.1.1",
    "datastore.name": "tcs_7vqbch1l",
    "dir.dbdata": "C:\\arcgis\\arcgisdatastore\\nosqldata",
    "db.http": 29080,
    "db.https": 29081,
    "db.host": "CC-GIS.CLATSOP.CO.CLATSOP.OR.US",
    "datastore.admindb": "dsconfig$",
    "dir.backup": "C:\\arcgis\\arcgisdatastore\\backup\\tilecache",
    "dir.backup.isshared": "false",
    "replication.role": "PRIMARY",
    "datastore.lastknownstatus": "Started",
    "localstore.lastknownstatus": "Started",
    "owningsys.type": "GISSERVER",
    "datastore.initstarttime": 1571939913377,
    "datastore.registered": true,
    "datastore.tilecache.enabled": true,
    "iniLocation": "C:\\arcgis\\arcgisdatastore\\nosqldata\\etc"
  },
  "log.activeManager": "relational",
  "machine.initstarttime": 1571939780518
 }


Looks like psql won't run in a bash shell, but works in powershell. Get passwords using the listadminusers.bat script. Try username 'sde'.

 ./psql -p 9876 -U sde -c "\l" postgres
 Password for user sde:
                                                    List of databases
     Name     |   Owner   | Encoding |          Collate           |           Ctype            |    Access privileges
 --------------+-----------+----------+----------------------------+----------------------------+-------------------------
 db_0eoas     | adm_o77v5 | UTF8     | English_United States.1252 | English_United States.1252 |
 dsadmindb    | adm_o77v5 | UTF8     | English_United States.1252 | English_United States.1252 |
 postgres     | adm_o77v5 | UTF8     | English_United States.1252 | English_United States.1252 |
 template0    | adm_o77v5 | UTF8     | English_United States.1252 | English_United States.1252 | =c/adm_o77v5           +
              |           |          |                            |                            | adm_o77v5=CTc/adm_o77v5
 template1    | adm_o77v5 | UTF8     | English_United States.1252 | English_United States.1252 | adm_o77v5=CTc/adm_o77v5+
              |           |          |                            |                            | =c/adm_o77v5
 template_gdb | sde       | UTF8     | English_United States.1252 | English_United States.1252 |
 (6 rows)

I am guessing my datastore relational database is db_0eoas

'''But there are scripts''' even on Windows! They are described in this [https://delta.co.clatsop.or.us/portal/portalhelp/en/data-store/latest/install/windows/data-store-utility-reference.htm reference]. The scripts live here: '''PS C:\Program Files\ArcGIS\DataStore\tools''' such as this one

 .\describedatastore.bat
 
 General information of ArcGIS data stores on CC-GIS.CLATSOP.CO.CLATSOP.OR.US
 ==================================================
 Data store release..................10.7.1.11595
 Staging location....................C:\arcgis\arcgisdatastore\staging
 Log location........................C:\arcgis\arcgisdatastore\logs
 Free disk space.....................313.00GB
 Threshold for READONLY mode.........1024MB
 
 Information for relational data store ds_atjwr8b3
 ==================================================
 Backup location.....................C:\arcgis\arcgisdatastore\backup\relational
 Is backup folder shared.............false
 Backup schedule.....................{"schedule-starttime":"00:00:00","schedule-frequency":"Every 4 DAYS"}
 Days backup retained................7
 Data store status...................Started
 member machines.....................CC-GIS.CLATSOP.CO.CLATSOP.OR.US
 Maximum connections.................150
 Owning system URL...................https://delta.co.clatsop.or.us/server
 Portal for ArcGIS URL...............https://delta.co.clatsop.or.us/portal
 Number of connections...............0 connection(s) to managed database
 Data Store mode.....................READWRITE
 Is Point-in-time recovery enabled...No
 Query optimizer enabled.............Yes
 
 Information for tile cache data store tcs_7vqbch1l
 ==================================================
 Data location.......................C:\arcgis\arcgisdatastore\nosqldata
 Data store status...................Started
 Backup location.....................C:\arcgis\arcgisdatastore\backup\tilecache
 Is backup folder shared.............false
 member machines.....................CC-GIS.CLATSOP.CO.CLATSOP.OR.US
 Owning system URL...................https://delta.co.clatsop.or.us:6443/arcgis/admin
 Portal for ArcGIS URL...............https://delta.co.clatsop.or.us/portal
 
 
 Operation completed successfully.

From the '''describedatastore''' command I learned there really is still a relational data store in there, it's just not connected up.
I think it got disconnected a few months ago. I need a place to stash hosted data so after 10.6 -> 10.7.1 I resurrected it.
I probably only need to use the registerdatastore command.

=== Tile cache ===

The DataStore also includes a "Tile Cache" that's not really a tile cache. It's actually '''CouchDB''' running on port 29080.
I can see the Fauxton interface, http://cc-gis:29080/_utils but I have to know what my credentials are. 
Turns out it's easy to find out! Do this as powershell admin user

'''c:\Program Files\ArcGIS\DataStore\tools\listadminusers.bat''' and lookie, it exposes all admin and password entries for PostgreSQL and CouchDB DataStore!

==== It's not a tile cache ====

Curiously there do not appear to be any documents stored here.  Just a configuration.
Yet my server does indeed have tiles... I asked about it in the ESRI forum and was told that the
Tile Cache is actually used for storing Scenes. I have not tried creating any 
scenes yet so it's empty.

== Older stuff ==

=== SSL and HTTPS ===

Today I noticed error messages about a "weak certificate" in my debug log for OpenLayers.
I had to navigate to the server to refresh the certificate (to tell it that a self signed cert was okay in other words.)
Once I did that pages loaded again in OpenLayers.

I needed to get "Let's Encrypt" set up on my (Linux based) ArcGIS Server. I did this later on. 
Note Let's Encrypt only wants to install onto public facing web servers so you will have problems
if you have a server that's locked up behind a firewall.

== Installing into an Ubuntu VirtualBox VM on Bellman ==

After installing Ubuntu,

 apt update
 apt upgrade
 apt install emacs-nox build-essential tomcat8 tomcat8-admin

I had to issue the mount command myself to get the VirtualBox additions cdrom to play.

 mount /dev/cdrom /media/cdrom
 cd /media/cdrom
 ./VBoxLinuxAdditions.run

Now I take a snapshot once the machine is configured and before installing ArcGIS... '''vboxmanage snapshot server take before_arcgis'''

I set the vm to share ~bwilson/Downloads and /green/GIS/Data_Repository

==== Set up tomcat ====

Edit /etc/tomcat8/tomcat-users.xml and add a user with the role manager-gui.
For example, 

 <role rolename="manager-gui"/>
 <user username="tomcat" password="s3cret" roles="manager-gui"/>

=== Running the Enterprise Builder ===

''Current advice: never use the Builder. Advice direct from ESRI help desk.''

The tarball is already unpacked in Downloads, so I ssh into bellman and

 sudo -s
 cd /media/sf_Downloads
 cd EnterpriseBuilder

The instructions are in HTML format, so I NFS mounted the folder on my Mac and opened the toplevel html file in Firefox.

* Gather prvc (provisioning files) good luck navigating the ESRI web site!
* Run ./Setup
* Get this message
 WARNINGS:
 ------------------------------------------------------------------------
 *** DIAG002: Unsupported Linux distribution.  Check the ArcGIS Data
 Store System Requirements for supported Linux distributions.

This is like being slapped in the face with a wet Mackerel, since I chose the distribution from ESRI's website.
Yep, here it is in the HTML docs too:
  Ubuntu Server LTS 16.04.3

I have this: PRETTY_NAME="Ubuntu 16.04.4 LTS"
Hmmm... that looks okay and in fact their

 ./Setup -s `pwd`/'''server.prvc''' -p '`pwd`/''portal.prvc -v
 Deploying ArcGIS 10.6 Enterprise Builder requires a minimum of 7.5 GB of RAM. Please contact your system administrator.

Ah.. fixing... bumped it to 10GB. Bellman has 32GB so that should be fine. Now it's giving me more instructions.
However clumsy these changes might seem to an experienced Linux user, make them to keep ESRI happy:

 adduser arcgis
 cat >> /etc/security/limits.conf <<EOF
 arcgis soft nofile 65536
 arcgis hard nofile 65536
 arcgis soft nproc 25059
 arcgis hard nproc 25059
 EOF
 
 /sbin/sysctl -w vm.max_map_count=262144
 /sbin/sysctl -w vm.swappiness=1

I edited /etc/hosts to put this line in
 192.168.123.72 duster.wildsong.biz duster
and I coerced the 127.1.0.1 line to have the domain in it, too.

Log out, log back in as arcgis and check
 ulimit -Sn -Hn

Run setup again.

All is in readiness.

<pre>
arcgis@duster:/media/sf_Downloads/EnterpriseBuilder$ ./Setup -p `pwd`/PortalforArcGIS_594279.prvc -s `pwd`/_ArcGISServer_594278.prvc -v
========================================================================
                  ArcGIS Server 10.6.0 Diagnostic Tool
                                    
                            Hostname: duster
========================================================================

 DIAG000: Check for installation as root                       [PASSED]
 DIAG001: Check for 64-bit architecture                        [PASSED]
 DIAG002: Check OS version                                     [PASSED]
 DIAG003: Check hostname for invalid characters                [PASSED]
 DIAG024: Check /etc/hosts for hostname entry                  [PASSED]
 DIAG004: Check installed packages                             [PASSED]
 DIAG005: Check system limits                                  [PASSED]
 DIAG008: Check HTTP port                                      [PASSED]
 DIAG009: Check HTTPS port                                     [PASSED]
 DIAG010: Check Xvfb ports                                     [PASSED]

------------------------------------------------------------------------
There were 0 failure(s) and 1 warning(s) found:


WARNINGS:
------------------------------------------------------------------------
*** DIAG024: The hostname entry in the /etc/hosts file must be in the
following format:

	<IP> <FQDN> <Machine_name>

For example:

	111.222.333.444 hostname.esri.com hostname

Federating an ArcGIS Server site with Portal for ArcGIS will fail if
this entry is formatted differently.  Update the hostname entry before
creating your ArcGIS Server site.


========================================================================
                Portal for ArcGIS 10.6.0 Diagnostic Tool
                                    
                            Hostname: duster
========================================================================

 DIAG000: Check for installation as root                       [PASSED]
 DIAG001: Check for 64-bit architecture                        [PASSED]
 DIAG002: Check OS version                                     [PASSED]
 DIAG003: Check hostname for invalid characters                [PASSED]
 DIAG005: Check system limits                                  [PASSED]
 DIAG004: Check installed packages                             [PASSED]
 DIAG016: Check Portal for ArcGIS ports                        [PASSED]
 DIAG024: Check localhost resolution                           [PASSED]
 DIAG029: Check file system type                               [PASSED]

------------------------------------------------------------------------
There were 0 failure(s) and 0 warning(s) found:



========================================================================
                ArcGIS Data Store 10.6.0 Diagnostic Tool
                                    
                            Hostname: duster
========================================================================

 DIAG000: Check for installation as root                          [PASSED]
 DIAG001: Check for 64-bit architecture                           [PASSED]
 DIAG002: Check OS version                                        [PASSED]
 DIAG003: Check hostname for invalid characters                   [PASSED]
 DIAG004: Check installed packages                                [PASSED]
 DIAG005: Check relational and tile cache data store requirements [PASSED]
 DIAG016: Check ArcGIS Data Store ports                           [PASSED]
 DIAG020: Check hostname IP address mismatches                    [PASSED]
 DIAG029: Check spatiotemporal big data store requirements        [PASSED]

------------------------------------------------------------------------
There were 0 failure(s) and 0 warning(s) found:



Enter 'q' to quit or press enter to continue: 
</pre>

Oh BITE me!

 Starting installation of ArcGIS 10.6 Enterprise Builder...
 [ArcGIS 10.6 Enterprise Builder Setup Warning]
 This setup has detected that the DISPLAY variable has not been set, but the silent UI mode was not selected.
 Note: For information on the silent setup UI mode, please run this script with the --help option.

Run setup again!

 ./Setup -p `pwd`/PortalforArcGIS_594279.prvc -s `pwd`/_ArcGISServer_594278.prvc -v -l yes -m silent

Eventually, after a subtantial wait,

<pre>
[ArcGIS 10.6 Enterprise Builder Installation Details]
UI Mode......................silent
Agreed to Esri License.......yes
Server Authorization File..../media/sf_Downloads/EnterpriseBuilder/_ArcGISServer_594278.prvc
Portal Authorization File..../media/sf_Downloads/EnterpriseBuilder/PortalforArcGIS_594279.prvc
Installation Directory......./home/arcgis
Install Set..................Typical

Starting installation of ArcGIS 10.6 Enterprise Builder...
...ArcGIS 10.6 Enterprise Builder installation is complete.

Before using ArcGIS 10.6 Enterprise Builder, please navigate to http://duster:6080/arcgis/enterprise to complete the configuration.
</pre>

=== Curiously painful step 7 ===

 7. In the Web Adaptor URLs panel, enter the URLs for the Web Adaptors (https://webadaptorhost.domain.com/webadaptorname) 
 that will be configured with the portal and server components of your deployment.
 '''These Web Adaptors must already be installed and located on the same machine where you ran the ArcGIS Enterprise Builder.'''

Okay fine. You told me I don't need Web Adaptor in the deployment but now you block configuration.
Over and over I read docs that say I don't need it but every time I try to install, I am blocked when I don't have it. 

There is a configuration SCRIPT tucked away though, trying that... it requires -ws and -wp options, so, oh well.

tools/configurebasedeployment/configurebasedeployment.sh -e brian@wildsong.biz -fn Brian -ln Wilson -qi 10 -qa ''''secret'''' -u bwilson -p ''''secret''''

Hence... installing Web Adaptor

== Running the Web Adaptor installer ==

Download and unpack tarball, then ignore the statement that you should be root. Log in as 'arcgis'

 cd WebAdaptor
 ./Setup -v -m silent -l yes -d ~

<pre>
[ArcGIS Web Adaptor (Java Platform) 10.6 Installation Details]
UI Mode..................silent
Agreed to Esri License...yes
Installation Directory.../home/arcgis/webadaptor10.6

Starting installation of ArcGIS Web Adaptor (Java Platform) 10.6...
Checking for POSIX df.
Found POSIX df.
Checking tail options...
Using tail -n 1.
True location of the self extractor: /media/sf_Downloads/WebAdaptor/WebAdaptor/Linux/Disk1/InstData/VM/install.bin
Creating installer data directory: /tmp/install.dir.32735
Creating installer data directory: /tmp/install.dir.32735/InstallerData
Gathering free-space information...
Space needed to complete the self-extraction: 451436 blocks
Available space: 43131176 blocks
Available blocks: 43131176    Needed blocks: 451436 (block = 512 bytes)
Computed number of blocks to extract: 2192
Extracting JRE from /media/sf_Downloads/WebAdaptor/WebAdaptor/Linux/Disk1/InstData/VM/install.bin to /tmp/install.dir.32735/Linux/resource/jre_padded ...
Extracting done, exit code = 0
Extracting JRE from /tmp/install.dir.32735/Linux/resource/jre_padded to /tmp/install.dir.32735/Linux/resource/vm.tar.Z ...
 Extracting done, exit code = 0
Unpacking the JRE...
gzip is /bin/gzip
 GZIP done.
 TAR done.
Extracting install.zip from /media/sf_Downloads/WebAdaptor/WebAdaptor/Linux/Disk1/InstData/VM/install.bin to /tmp/install.dir.32735/InstallerData/installer.padded ...
Extracting to padded done, exit code = 0
Extracting from padded to zip done, exit code = 0

========= Analyzing UNIX Environment =================================
Setting UNIX (linux) flavor specifics.
Importing UNIX environment into LAX properties.
Checking for POSIX awk.

========= Analyzing LAX ==============================================
LAX found............................ OK.
LAX properties read.................. OK.

========= Finding VM =================================================
Valid VM types.......................... 1.6+
Absolute LAX_VM path.................... /tmp/install.dir.32735/Linux/resource/jre/bin/java
Expanded Valid VM types.................  1.6+ 
Unzipping of installer.zip failed.
Using the Default JVM Search
Searching without JVM specs
* Using VM.....(lax.nl.current.vm)...... /tmp/install.dir.32735/Linux/resource/jre/bin/java

========= Virtual Machine Options ====================================
LAX properties incorporated............. OK.
classpath............................... "/tmp/install.dir.32735/InstallerData:/tmp/install.dir.32735/InstallerData/installer.zip"
main class.............................. "com.zerog.ia.installer.Main"
.lax file path.......................... "/tmp/install.dir.32735/temp.lax"
user directory.......................... "/tmp/install.dir.32735"
stdout to............................... "console"
sterr to................................ "console"
install directory....................... ""
JIT..................................... none
option (verify)......................... off
option (verbosity)...................... none
option (garbage collection extent)...... none
option (garbage collection thread)...... none
option (native stack max size).......... none
option (java stack max size)............ none
option (java heap max size)............. 201326592
option (java heap initial size)......... 16777216
option (lax.nl.java.option.additional).. none

========= Display settings ===========================================
X display............................... local
UI mode................................. silent
========= VM Command Line ============================================
options:   -Xmx201326592 -Xms16777216 
CLASSPATH:/tmp/install.dir.32735/InstallerData:/tmp/install.dir.32735/InstallerData/installer.zip:

========= Forking JAVA =============================================
LAX Version = 16.5
locale being set to: en

[AnalyzeSystemRequirements][install] Start
[AnalyzeSystemRequirements][install] Product=WebAdaptor
[AnalyzeSystemRequirements][checkUserHome] Start
[AnalyzeSystemRequirements][checkUserHome] /home/arcgis exists and is writable!
[AnalyzeSystemRequirements][checkUserHome] Finish
[AnalyzeSystemRequirements][install] Finish
[MiscUtils][getReleaseVersion] Simple version reported by setup: 10.6
[MiscUtils][runCommand][Threaded=false] About to execute: uname -n
[MiscUtils][runCommand][Threaded=false] StdOut Output: duster
[MiscUtils][runCommand][Threaded=false] StdErr Output: Ignored in non-threaded runCommand().
[MiscUtils][runCommand][Threaded=false] Exit Code    : 0
[MiscUtils][getESRIPropFilePath] ESRI.properties file path: /home/arcgis/.ESRI.properties.duster.10.6
[ReadESRIPropFile][install] ESRI prop file found at /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper] Open existing prop file: /home/arcgis/.ESRI.properties.duster.10.6
[ReadESRIPropFile] Z_DEVKIT_HOME=
[ReadESRIPropFile] Z_ArcGISServer_INSTALL_DIR=/home/arcgis/server
[ReadESRIPropFile] Z_ENGINE_HOME=
[ReadESRIPropFile] Z_ArcGISDataStore_INSTALL_DIR=/home/arcgis/datastore
[ReadESRIPropFile] ARCLICENSEHOME=/home/arcgis/server/framework/runtime/.wine/drive_c/Program Files/ESRI/License10.6/sysgen
[ReadESRIPropFile] Z_WebGIS_INSTALL_DIR=/home/arcgis
[ReadESRIPropFile] ESRI_PROGRAM_FILES=
[ReadESRIPropFile] Z_ArcGISPortal_INSTALL_DIR=/home/arcgis/portal
[ReadESRIPropFile] Z_REAL_VERSION=10.6
[DetermineInstallDirWebAdaptor][install] InstallDir from IA: /home/arcgis/webadaptor10.6
[DetermineInstallDirWebAdaptor][install] Set USER_INSTALL_DIR to: /home/arcgis/webadaptor10.6/java
installUnixJRE:  the source VM tar: /tmp/install.dir.32735/Linux/resource/vm.tar
    exists = true
installUnixJRE:  the source VMRoot: /tmp/install.dir.32735/Linux/resource/jre
    exists = true
installUnixJRE:  the dest VMRoot: /home/arcgis/webadaptor10.6/java/.Setup/jre
    exists = true
#
# INSTALLING VM: /home/arcgis/webadaptor10.6/java/.Setup/jre
#

installUnixJRE: Using new TAR technique...
Destination path for tar extraction (sans 'jre') =
    /home/arcgis/webadaptor10.6/java/.Setup

installUnixJRE: install shell script:
#!/bin/sh
echo "InstallUnixJRE Script begun..."
cd '/home/arcgis/webadaptor10.6/java/.Setup/jre'
rm -rf  *''
cd '/home/arcgis/webadaptor10.6/java/.Setup'
tar xf '/tmp/install.dir.32735/Linux/resource/vm.tar'
chmod -R '755' '/home/arcgis/webadaptor10.6/java/.Setup/jre'
echo "...InstallUnixJRE Script complete."
##### SCRIPT END ############

XMLScriptWriter: No Installation Objects were skipped
[MiscUtils][getReleaseVersion] Simple version reported by setup: 10.6
[MiscUtils][runCommand][Threaded=false] About to execute: uname -n
[MiscUtils][runCommand][Threaded=false] StdOut Output: duster
[MiscUtils][runCommand][Threaded=false] StdErr Output: Ignored in non-threaded runCommand().
[MiscUtils][runCommand][Threaded=false] Exit Code    : 0
[MiscUtils][getESRIPropFilePath] ESRI.properties file path: /home/arcgis/.ESRI.properties.duster.10.6
[getCurrentESRIPropFilePath][install] Set ESRI_PROP_FILE_PATH to: /home/arcgis/.ESRI.properties.duster.10.6
[ReadESRIPropFile][install] ESRI prop file found at /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper] Open existing prop file: /home/arcgis/.ESRI.properties.duster.10.6
[ReadESRIPropFile] Z_DEVKIT_HOME=
[ReadESRIPropFile] Z_ArcGISServer_INSTALL_DIR=/home/arcgis/server
[ReadESRIPropFile] Z_ENGINE_HOME=
[ReadESRIPropFile] Z_ArcGISDataStore_INSTALL_DIR=/home/arcgis/datastore
[ReadESRIPropFile] ARCLICENSEHOME=/home/arcgis/server/framework/runtime/.wine/drive_c/Program Files/ESRI/License10.6/sysgen
[ReadESRIPropFile] Z_WebGIS_INSTALL_DIR=/home/arcgis
[ReadESRIPropFile] ESRI_PROGRAM_FILES=
[ReadESRIPropFile] Z_ArcGISPortal_INSTALL_DIR=/home/arcgis/portal
[ReadESRIPropFile] Z_REAL_VERSION=10.6
[PropertiesFileWrapper] Open existing prop file: /home/arcgis/.ESRI.properties.duster.10.6
[PropFileUtils][setProperty] Set Z_WebAdaptor_INSTALL_DIR to /home/arcgis/webadaptor10.6/java in file /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper][save] Saving /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper] Open existing prop file: /home/arcgis/.ESRI.properties.duster.10.6
[PropFileUtils][setProperty] Set Z_REAL_VERSION to 10.6 in file /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper][save] Saving /home/arcgis/.ESRI.properties.duster.10.6
[WriteESRIPropFile][install] PRODUCT_NAME: WebAdaptor
[PropertiesFileWrapper] Open existing prop file: /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper][save] Saving /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper][save] Saving /home/arcgis/.ESRI.properties.duster.10.6
[PropertiesFileWrapper][save] Saving /home/arcgis/.ESRI.properties.duster.10.6
Retrying Installables deferred in pass 0
Deferral retries done because: 
There were no deferrals in the last pass.
...ArcGIS Web Adaptor (Java Platform) 10.6 installation is complete.
</pre>

== Post-install work ==

Take another snapshot once it's running.

Set up the services to start automatically at boot. Or do it by hand...

 ssh arcgis@duster
 datastore/startdatastore.sh
 server/startserver.sh
 portal/startportal.sh

== Enterprise Geodatabase ==

On Windows this often can mean Microsoft SQL Server

=== SQL Server ===

==== User auth ====

==== SQL Server backup ====

# Check for connections in ArcGIS Pro, and kick people out if need be.
# Launch SQL Server Management Studio ("SSMS") anywhere (does not have to be on the SQL Server) 
# Right click the database, select Properties->Options->State and set Read-Only to True (this will dump all connections. See step 1)
# Connect to database using '''your own credentials''' (or some user that can READ the data and WRITE to the target on the network share.)
# Right click the database eg "Clatsop" and use Tasks->Backup.
# Select Recover mode = FULL
# Set Backup component to Database
# Set Destination to Disk
# Delete whatever comes up in like "Nul"
# So far, I have been unable to write output to a fileserver so I send it to "C:\Temp\sqlserver.backup" '''THIS IS STUPID''' but it works.
# Ignore the warning that it can't find the file because it does not exist
# Click on "Media options"
# Set "Verify backup when finished"
# Click OK
# Mark the database as Read-Write (See step 3)

Once the backup has completed I move it to a file share. 
Also note that C:\Temp\ refers to a folder '''on the SQL Server''' NOT on your desktop!!

Also note an ssh session does not allow me access to the file server either. What? Oy. I have to open a remote connection and do it there. Yup.

Example file in its final destination '''\\cc-files01\Applications\GIS\backups\cc-gis-2022-05-18_backup''' If I try to write ".backup" on our file server, it fails! I cannot! Humans!

You won't be able to delete the "C:\Temp\" copy until you exit SSMS! Ha! Fraught with many perils, this process is.

I have successfully "restored" from a full backup onto another SQL Server machine, it works. I have yet to restore onto the machine it came from.

== Versioning ==

When editing in ArcMap by default all edits are versioned.

https://desktop.arcgis.com/en/arcmap/latest/manage-data/geodatabases/changing-versions-in-arcmap.htm

=== "Change Version" is disabled (greyed out) ===

You can't change versions while an edit session is active.

=== "I can't edit a table because it's not versioned" ===

== Publishing a layer ==

Registration: I want the data to continue living in SQL Server so first I have to
tell the server about it. They call this process [http://enterprise.arcgis.com/en/server/latest/publish-services/windows/registering-your-data-with-arcgis-server-using-arcgis-for-desktop.htm registering].

More on publishing here: 
[[Publishing data in ArcGIS Enterprise]]



[[Category: GIS]]
