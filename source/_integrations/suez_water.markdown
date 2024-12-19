---
title: Suez Water
description: Instructions on how to integrate Suez Water daily data within Home Assistant.
ha_release: 0.97
ha_category:
  - Sensor
ha_iot_class: Cloud Polling
ha_config_flow: true
ha_codeowners:
  - '@ooii'
  - '@jb101010-2'
ha_domain: suez_water
ha_platforms:
  - sensor
ha_integration_type: integration
---

The **Suez Water** {% term integration %} fetches your water consumption data from the French water provider [Tout Sur Mon Eau](https://www.toutsurmoneau.fr) website.

## Configuration

{% configuration_basic %}

Username:
  description: The username used to connect to [Tout Sur Mon Eau](https://www.toutsurmoneau.fr) website
Password:
  description: The password used for connecting the user define above
Counter ID:
  description: "The water meter ID. It should be found automatically during setup. If it was not found, the ID can be found on your _Tout Sur Mon Eau_ [user account](https://www.toutsurmoneau.fr/mon-compte-en-ligne/historique-de-consommation-tr). Look in the source code of the page for something similar to `url: '/mon-compte-en-ligne/statMData' + '/123456789'`. The `counter_id` in this case is `123456789`."

{% endconfiguration_basic %}


## Sensors

- The **Water usage yesterday** sensor shows yesterday's water consumption data if that data is available.
- The **Water price** sensor shows the current water price in euros per cubic meter (€/m3).

### Extra attributes

Extra attributes of `Water usage yesterday` sensor:

- Daily consumption for the current month
- Daily consumption for the previous month
- Monthly consumption for the last 26 months
- Highest monthly consumption
- Last year total consumption
- Current year total consumption
{% include integrations/config_flow.md %}

## Data updates

The integration collects data every 12 hours. To customize the refresh interval, refer to [defining a custom polling interval](/common-tasks/general/#defining-a-custom-polling-interval). Specify one single entity from the suez device as target of the action using the `+ choose entity` button. Updating one entity will update all entities of the Suez integration; there is no need to specify multiple or all entities.
When updating the refresh rate remember that Suez data are updated once a day, generally in the morning.

## Supported devices

For the integration to work you must have a connected weter and an account on [Tout Sur Mon Eau](https://www.toutsurmoneau.fr).
If monthly and daily consumption are available at [consumption history](https://www.toutsurmoneau.fr/mon-compte-en-ligne/historique-de-consommation-tr) then your meter is compatible.

## Remove integration

This integration can be removed by following these steps:

{% include integrations/remove_device_service.md %}

## Troubelshooting

### Debug log

When experiencing issues during the use of the integration, enable the debug log for the Suez integration. Then restart the integration. This will add details on the data collection to the Home Assistant log file. Leave the debug log enabled long enough to capture the occurrence of the issue. If the issue is intermittent, this may take a while and it may grow the log file quite a bit.

Once the issue occurred, stop the debug logging again. When reporting the issue, include the content of the debug logs, be careful to redact sensible information (username and meter id).

The debug log will show all communication with [Tout Sur Mon Eau](https://www.toutsurmoneau.fr). Lines starting with below examples are log entries for the integration:

```txt
2024-03-07 11:20:11.897 DEBUG (MainThread) [homeassistant.components.suez_water
2024-03-07 11:20:11.898 DEBUG (MainThread) [pysuez
```
