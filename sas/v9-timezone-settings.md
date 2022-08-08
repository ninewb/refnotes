# Time Zone Settings

For various SAS processes you may need to add a parameter so that certain content are not written with the default timezone.  This could be because data is stored with a specific timezone, and as the data gets processed, the system time zone could inadvertantly change it undesirably.

Tomcat defaults to the GMT timezone. If you want to change it you need to add the following code to `$TOMCAT_HOME/bin/setenv.sh` (or `$TOMCAT_HOME/bin/setenv.bat` if you're on Windows) using your time zone:

| Location                                   | Setting                      |
|--------------------------------------------|------------------------------|
| !SASHOME/SASFoundation/9.4/sasv9_local.cfg | -timezone "America/Menominee |
| !SASHOME/bin/sasenv_local                  | export TZ=American/Menominee |

- The [following documentation](https://go.documentation.sas.com/?docsetId=nlsref&docsetTarget=n0px72paaaqx06n1ozps024j78cl.htm&docsetVersion=9.4&locale=en) outlines time zone settings within SAS.
- [Here](http://tutorials.jenkov.com/java-date-time/java-util-timezone.html) you will see a list of timezones.
