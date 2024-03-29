# Geoserver Install Basics (Servlet on Windows)

Summary from https://www.youtube.com/watch?v=7bbq3gWEXI8

## Getting Tomcat 9 running

Install JRE: https://jdk.java.net/java-se-ri/11 (JRE version)
Install Tomcat: https://tomcat.apache.org/download-90.cgi (Windows 64bit version 9.0.73) - DO NOT USE v10

Install with the management interface which can be accessed using u/p during setup
U/P can be modified in text file here:
$CATALINA_BASE/conf/tomcat-users.xml

URL is http://localhost:8080/manager/html

## Install Geoserver WAR file

Download Geoserver: https://geoserver.org/release/stable/ (WAR version 2.22.2)

Extract ZIP and copy WAR file to `$CATALINA_BASE/webapps` and it will automatically deploy

Check that it is running in tomcat manager (after a few minutes)

Open Geoserver http://localhost:8080/geoserver (default u/p:admin/geoserver)

Perform hardening as is: https://docs.geoserver.org/latest/en/user/installation/war.html
(hides version info, security through obscurity)

Change Geoserver admin password using web interface (security/users/admin change)

Now Geoserver is running locally (8080) as http. 

Turn off autodeploy, edit `C:\Geoserver\tomcat9\conf\server.xml` and modify `autoDeploy="false"`

## Configure redirect on IIS

Assumes IIS is already running with valid cert. 

Install https://www.iis.net/downloads/microsoft/application-request-routing
Install https://www.iis.net/downloads/microsoft/url-rewrite

Restart IIS

1. Open IIS Manager from Start menu
2. On server name Open Application Request Routing Enable proxy
3. Back to server name in IIS, Open URL Rewrite
4. Add new inbound rule with match pattern `(geoserver/.*)`
5. Rewrite URL: `http://localhost:8080/{R:0}`

### Tell Geoserver about the domain to be used. 

Add proxy base using web admin interface under global settings. 

Geoserver CSRF Whitelist edit to avoid security 403 errors using IIS passthru
Edit `\webapps\geoserver\WEB-INF\web.xml`

In section with   

`<context-param>`

add
```
<context-param>
	<param-name>GEOSERVER_CSRF_WHITELIST</param-name>
	<param-value>DOMAINNAME.COM</param-value>
</context-param>
```
### Enable CORS for Tomcat

Uncomment two other sections within web.xml to enable CORS wildcard.
