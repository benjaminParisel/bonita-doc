# Licenses

::: info
**Note:** For Performance, Efficiency, and Teamwork editions only.
:::

Bonita 7.1 introduces a case-counter mechanism to align with the Bonita Subscription edition licensing model. This page explains how to manage the license for your Bonita Platform. 

The **_License_** menu in Bonita Portal displays information about the current license. This information is available to the platform administrator only.

The [license for Bonita Studio](bonita-bpm-studio-installation.md) is managed through a wizard when you start the studio for the first time after installation (or after the previous license expires).

## Case-counter licensing

A case-counter license defines the maximum number of cases (process instances) that the platform is permitted to start in the counter period.  
The counter period is typically one year and starts when your Subscription starts or on the anniversary.  
Each time a case starts, the case counter is increased by one.  
Case-counter licenses are available for development and for production. A development license must not be used for production, and typically has a lower case limit than a production license.  
The maximum number of cases is defined in your commercial contract, in discussion with your sales person.

You can monitor the case counter using Bonita Portal *License* page in the Administrator profile, or using the [REST API](platform-api.md#license) to create a custom monitoring / alerting tool.  
Those two means also allow you to check the expiration date of the license.

When the case counter reaches the limit set in the license, no more cases can be started. Active cases continue to completion.  
If a user tries to submit an instantiation form after the case counter maximum limit is reached, the form is not submitted and an error message is displayed.  
**Note:** If the process still uses legacy, 6.x, forms, there is no error message.

## Get a new license

Your contract with Bonitasoft specifies the details of the subscription you have purchased, including the edition, and case limit for case-counter licensing. A license matching the subscription details is generated on request.

If this is a license renewal, you can find your request key in the Bonita Portal *License* menu of the Administrator profile or using the [platform REST API](platform-api.md#license).  
A request key looks like this: `(CIVpYDRB8bhouXdWadLY1M9TVctwYUYuv7ou7sqeIrSUSuCqUIkjQAs0ZGgzbtqv3gguFOHlyMZkyvwdr4HLgg==)`.

If this is the first time you generate a license, you need to generate a request key.

### Generate the request key

On the server where you installed Bonita Platform:  
1. Go to the `request_key_utils` folder
2. Run the `generateRequestKey.bat` script (for Windows) or the `generateRequestKey.sh` script (for other operating systems)

### Generate the new license

Copy your request key and go to the [Customer Portal license request](https://customer.bonitasoft.com/license/request) page.  
Then fill in the details in the form, copy the request key in the *Request Key* field, and submit.  
Note: keep the brackets () in the key; if the key is separated by a line break, remove it and put the key on a single line.  

The license file will be sent to you by email.

## Install the license

When you receive the license file (`.lic` file extension):
- If this is the first time you start the bundle, copy the file to the`<TOMCAT_HOME>/setup/platform_conf/licenses` folder or `<WILDFLY_HOME>/setup/platform_conf/licenses/` folder before starting the bundle.
- If the bundle has already been started, [you need to use the Platform setup tool](BonitaBPM_platform_setup.md#update_platform_conf) to push your license file to database.
Don't forget to restart your application server after pushing the license to the database.

## License renewal scheduling

If you are still within the Subscription period when you approach the license expiration date, request a new license that starts on the last day of your current license.  
[Use the Platform setup tool](BonitaBPM_platform_setup.md#update_platform_conf) to pull the existing configuration from the database.
Put the license you receive in the license folder alongside the existing license. 
[Use the Platform setup tool](BonitaBPM_platform_setup.md#update_platform_conf) to push your license file to database.
Don't forget to restart your application server after pushing the license to the database.

When you reach the "changeover" date for the licenses, Bonita Engine switches automatically from the expired license to the valid one.
**Note:** We recommend to regularly remove license files of expired licenses from the server.

If you approach both the license expiration date and the end of the Subscription period, contact your sales person.

The case counter is reset at the end of the counter period.  
If your license expiration date comes before the end of the counter period, get and install a new license as usual. The case counter will continue from its current value under the new license.  
If you approach or reach the case counter limit before the end of the license period, contact your sales person to get a new license with additional cases.
