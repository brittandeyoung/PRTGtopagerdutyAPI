# PRTGtopagerdutyAPI
This is a Powershell script that will allow PRTG notifications to be sent to pagerduty via the events V2 API and auto resolve incidents that resolve within PRTG. I created this script because there is no native integration between PRTG and pagerduty except email.

## Setup Instructions
### Powershell
Make sure you have the latest version of powershell installed on the PRTG monitoring server.
### In pagerduty
Follow the pagerduty documentation to "Create a Generic Events API Integration" for the Events API V2.
(https://support.pagerduty.com/docs/services-and-integrations)
This will give you a routing Key/ integration key for use later (this authenticates PRTG to the API).
### In PRTG Network Monitor
1. On your server, navigate to C:\Program Files (x86)\PRTG Network Monitor\Notifications\EXE and place the file named “prtgtopagerduty.ps1” in this directory. 
2. Log into your PRTG web interface.
3. Navigate to "Setup" > "Account Settings" > "Notification Templates".
4. Click "Add Notification Template" from the blue "+" symbol.
5. Give the Template a name and update the following fields:
* **Method** Always notify ASAP, never summarize
* Toggle "Execute Program"
* **Program File**: Select the Prtgtopagerduty.ps1 from the drop down.
* **Parameters**: -API_URL 'https://events.pagerduty.com/v2/enqueue' -ROUTING_KEY 'Put your pagerduty routing key here' -Sensor %sensorid% -SiteName '%sitename' -Device '%device - %name' -DeviceId '%deviceid' -Name '%name' -Status '%status' -Down '%down' -DateTime '%datetime' -LinkDevice '%linkdevice' -Message '%message'
6. click save.
7. Test the notification.
8. Use the Notification Template for the items you want to send to Pagerduty =). You can also test the notificaitons after they have been assigned to a sensor by using the "Simulate Error Status" on the sesonr.
