# MendixSprintrAutomationLibrary

**** IMPORTANT NOTE: DOES NOT WORK (YET) FOR PRODUCTION ENVIRONMENTS (due to mostly 2fa issues) ****

SETUP REQUIRED

step 1:

Install Node on your computer: https://nodejs.org/en/download/

step 2:

Open CMD (windows) or Terminal (Mac) and go to the folder of the sprintrAutomation library.
example 'cd desktop/programming/MendixSprintrAutomationLibrary

step 3:

make the project ready for use with npm. Type: 'npm init'
hit enter about 10 times untill you see a dollar sign again $

step 4:

install dependancies:
- install puppeteer: type  'npm install puppeteer'  and hit Enter. this is a prebuilt module the script uses to navigate throug a webpage.
- install downloads-folder: type:  'npm install downloads-folder'  and hit Enter. This modul we need to get the local downloads folder on your computer 
(so it can locate the downloaded logfiles from sprintr).

step 5:

in the root folder, create a file called 'credentials.json' and paste the following json in there:

{
    "username": "username",
    "password": "yourSprintrPassword",
    "pgAdminUrl": "http://[IP-localhost]:[port]/?key=[key]",
    "pgAdminPass": "yourPgAdminPassword"
}

Where 
[IP-localhost]  = most of the time 127.0.0.1, but you can find this number by launching pgAdmin in the webbrowser and clicking on the url.
[port] = launch pgAdmin in the webbrowser and click on the url. Some numbers will appear in the url on the place where [port] stands in the example above. 
[key] = launch pgAdmin, enter password. Then go to cookies in your browser for this page. Copy the value for  PGADMIN_INT_KEY

Everytime you shutdown the pgAdmin server the key and port are deleted, so i just have it running all the time on my computer. Only after restarting my computer i have to refresh these attributes in the credentials file.


RUN THE PROGRAM

This library contains multiple scripts you can run:
- deployApp: deploys de latest version of the given appname and brancheline to an environment of choice (acceptance is default)
- downloadLogfile: downloads and displays the logfile for the appname and date.
- downloadDb: this downloads a backup from the sprintrEnvironment for the appname and date. 
- UploadBackupToPgAdmin: this downloads a backup from sprintr environment and restores it in pgAdmin

DeployApp:
You can run the deployboyApp.js from the commandline from the directory where the file is located.
The file uses two extra parameters [appname] and [branchename] so the command will look like this:

(..)/MendixSprintrAutomationLibrary$ node deployApp.js [appname] [branchename]

please note that the appname nor branchename can have spaces inbetween, because else those separate words of the branche or appname will be 
interpreted as separate parameters. So instead of a ' ' you have to type a '.' So 'my branche name' needs to be typed as 'my.branche.name'.

DownloadLogfile:
run the downloadLogfile.js from the commandline from the directory where the file is located.
The file uses two extra parameters [appname] and [date] (formatted 'yyyy-mm-dd', they are also formatted like this on the mendix sprintr),
so the command will look like this:

(..)/MendixSprintrAutomationLibrary$ node downloadLogfile.js [appname] [date]

DownloadDb:
run the downloadDb.js from the commandline from the directory where the file is located (root).
The file uses two extra parameters [appname] and [date] (formatted 'yyyy-mm-dd', they are also formatted like this on the mendix sprintr),
so the command will look like this:

(..)/MendixSprintrAutomationLibrary$ node downloadDb.js [appname] [date]

UploadBackupToPgAdmin:
This script uses the same parameters as DownloadDB.
so the command will look like this:

(..)/MendixSprintrAutomationLibrary$ node UploadBackupToPgAdmin.js [appname] [date]




PERSONAL SETTINGS (and in case of errors, read this)

1. In the root directory you can find a file called 'globalvariables.json'. In this file a couple of attributes are defined. A couple of variables
define the timeoutlength (wait untill a certain element appears on the page before trowing an error). If you experience any errors while running the script,
try making these numbers bigger. The sprinter environment sometimes loads slow so a timeout could happen.
2. by default it deploys to the acceptance environment. if you want to deploy to the 'test' or 'production' environment you can change the 'environment' attribute's value. 
3. by default the script opens a browser so you can see what happens exactly. If you don't want this to happen you can change the 'showProcesInBrowser' attribute to false.
4. if your appname by default uses the '.' character then you need to define another 'charToReplaceSpace'. You can do this overhere aswell.




LIMITATIONS & KNOWN BUGS

1. If the sprinter environment itself encountered an error (like: "there was an error restarting the app") This wil not be handled. Since this should not occur 99% of the time.
2. The pgAdmin part is created and tested on pgAdmin version 4.18

 
 
