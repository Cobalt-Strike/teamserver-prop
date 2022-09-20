# README

The Cobalt Strike 4.4 release introduced an optional file, **TeamServer.prop**, that contains a number of  parameters that can be used to customize the settings used to validate screenshot and keylog callback data. 

The Cobalt Strike 4.7.1 release introduced new settings for the maximum number of beacons, thresholds for new beacons and beacon XSS validation. 

The file is not included by default and a warning appears if it cannot be found when the teamserver starts up, but the absence of the file does not break the teamserver. 

This repository contains an example TeamServer.prop. We don't recommend that the defaults values are changed but if this is something that you want to do, simply copy the file into your Cobalt Strike directory and (re)start the teamserver.

- Lines starting with "#" are comments.

- **limits.\*_data_maxlen** is the maximum size of screenshot/keylog data that will be processed. Callbacks exceeding this limit will be rejected.
- **limits.\*_validated=false** means that the three following "**..._maxlen**" settings are ignored
- Setting any of the "**..._maxlen**" settings to zero will disable that particular setting
- **limits.\*_diskused_percent** sets the threshold for callback processing. Callbacks are rejected when disk usage exceeds the specified percentage
    - **limits.\*_diskused_percent=0** (zero) disables this setting
    - Valid values are 0-99


Add a limit to the number of beacons allowed (spam protection).
- **limits.beacons_max** is the maximum number of beacon allowed (default is *500*)
    - **limits.beacons_max=0** (zero) disables this setting

Threshold rate for adding new beacons (spam protection).
Add a limit to the number of new beacons added within a specified time period.
When the limit is exceeded, disable accepting new beacons for the disable duration.
- **limits.beacon_rate_period** milliseconds of the time period (default is *30000*)
    - **limits.beacon_rate_period=0** (zero) disables this setting
- **limits.beacon_rate_maxperperiod** new beacons allowed during time period (default is *50*)
    - **limits.beacon_rate_maxperperiod=0** (zero) disables this setting
- **limits.beacon_rate_disableduration** milliseconds to disable when threshold is exceeded (default is *600000*)
    - **limits.beacon_rate_disableduration=0** (zero) disables this setting

Perform XSS Validation on select new beacon metadata (spam protection).
- **limits.beacons_xssvalidated** (default is *true*)
    - **limits.beacons_xssvalidated=false** disables this setting