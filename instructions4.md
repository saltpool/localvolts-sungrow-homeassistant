# Instructions continued...
> This is PART FOUR of the instructions

## Step 8: Grafana Dashboard
Grafana is an open platform for creating really visually stunning analytics and monitoring. We will create a dashboard in Grafana so that you can see how your energy management is going with one quick glance. I have this dashboard running in my kitchen so that we can quickly glance up and see what the solar and batteries are doing, what the forecast is, etc, to help us decide when to put on more power-intensive workloads.

### Install Grafana
1. Go into Settings -> Add-ons -> Add-on Store
2. Search for "grafana"
<img src="https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/7e3d85dcd74652e9e84e57b5da7e03520b79d87b/images/grafana-1.png" />

3. Select it and then select Install
4. Enable both "Watchdog" and "Show in sidebar"
5. Select Start
6. Click on Grafana on the side bar
7. You should be shown a screen similar to the following:
<img src="https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/7e3d85dcd74652e9e84e57b5da7e03520b79d87b/images/grafana-2.png" />

### Create a datasource (HASS)
1. From within HASS, click on your user name (bottom left) and then click on the "Security" tab
2. Scroll down to the "Long-lived access tokens" section
3. Click on "Create Token"
4. Name it "Grafana" and press Ok
5. Copy the access token that is displayed. You won't see this again, so either keep it on your clipboard or paste it in notepad (or similar) so you can access it in the next steps.
6. Click on "Grafana" from the side bar
7. From the Grafana side menu, click on "Connections" and then "Add new connection"
    1. Search for "infinity"
    <img src="https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/022a6c60b95f0143554b0a0bd0684110ebdd0114/images/grafana-3.png" />
    
    2. Select "infinity" and then click on "Install"
    3. Refresh the page and then select "Add new data source"
    4. From the settings page that is displayed, click on the "Bearer Token" auth type, and then paste the token created previously into the "bearer token" box
    5. Enter the name or IP address of your HASS server in the "Allowed hosts" box, and click "Add".  This should be the same as how you are going to connect to HASS to pull the sensor data through the HASS API. By default, the graphs/charts in the dashboard that will shortly be imported are configured to connect to http://homeassistant.local:8123 (note, to use homeassistant.local, you will need this set up in your internal DNS. If you don't have an internal DNS, change it to the IP address of your HASS instance, e.g., http://192.168.4.15:8123 (you will need to find out what your HASS IP address is yourself).
<img src="https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/19c1ed47d856a9970126d778ddbea64cb23fa68e/images/grafana-4.png" />
    6. Click on "Health check" on the left and paste the following in the "Health check URL":

```
http://homeassistant.local:8123/api/states/sensor.daily_pv_generation
```

   Note: Change the name to the IP of your HASS server, if the name is not appropriate for you.
   
   7. Click "Save and test". Make sure that it tells you that your connection was successful before you move on the the next step.

### Create the Dashboard
1. Click on the "Dashboards" menu item within the Grafana menu
2. Cick on the "New" dropdown box and select Import
3. Copy the raw content of the [grafana.yaml](https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/19c1ed47d856a9970126d778ddbea64cb23fa68e/dashboards/grafana.yaml) file to your clipboard.
4. Return to your "Import dashboard" page and paste the contents into the lower box "Import via dashboard JSON model" and press "Load"
<img src="https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/e5bfdc53068e8c6d31ba32ad64b4647fa15ec4a3/images/grafana-5.png" />
5. Either keep the Name "EnergyMonitor" or change it to whatever you want, select your datasource (that you just made) from the lower dropdown box, and then press "Import"
<img src="https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/eb110ce10f6f9fa129e83d6f9923fcc29b435d7b/images/grafana-6.png" />
6. Once imported, you should be shown a dashboard similar to the following:
<img src="https://github.com/saltpool/localvolts-sungrow-homeassistant/blob/eb110ce10f6f9fa129e83d6f9923fcc29b435d7b/images/grafana-7.png" />

>[!TIP]
>If your HASS instance is not access as http://homeassistant.local:8123, you will need to update each and every API URL in each of the charts manually. Hint - do this BEFORE you import. Take the source YAML content and do a simple search and replace, then paste into the import text box as above.

>[!NOTE]
>If your dashboard does not show the sensors correctly, you may have to check the API URL that is being queried. This will happen if you have your HASS server known as anything but http://homeassistant.local:8123.
