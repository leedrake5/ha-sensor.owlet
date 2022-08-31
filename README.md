# ha-sensor.owlet
Owlet Smart Sock v2/v3 Sensor Integration for HomeAssistant using the modern Owlet API.

Credit for getting the new API to work goes to @mbevand for their work in https://github.com/mbevand/owlet_monitor/blob/master/owlet_monitor, which I borrowed from heavily while writing this.

# Installation:
### Manual Install:
Clone this repository, and move the `ha-sensor.owlet/custom_components/owlet` directory into your "custom_components" directory on homeassistant.

 and add the sensor configuration into your configuration.yml.

### HACS Install:

Add this repository as a custom repository in HACS under the type "integration."

### Both:

After installing the integration, you need to enable it by adding the sensor configuration into your configuration.yml - example:
```yaml
sensor:
  - platform: owlet
    username: your_owlet_email
    password: your_owlet_password
    region: "world"
```
Note that this formatting assumes you are using the secrets file. And if you want to have individual sensor values for the attributes, e.g. for outputting to a csv, you can use value_templates:
```yaml
- platform: template
  sensors:
    owlet_heart_rate:
      value_template: "{{states.sensor.owlet_smart_sock_[YOUR_SMART_SOCK_SERIAL_NUMBER].attributes.heart_rate}}"
      unit_of_measurement: BPM
    owlet_spo2:
      value_template: "{{states.sensor.owlet_smart_sock_[YOUR_SMART_SOCK_SERIAL_NUMBER].attributes.oxygen_saturation}}"
      unit_of_measurement: SPO2
    owlet_movement:
      value_template: "{{states.sensor.owlet_smart_sock_[YOUR_SMART_SOCK_SERIAL_NUMBER].attributes.movement}}"
      unit_of_measurement: '%'
    owlet_battery:
      value_template: "{{states.sensor.owlet_smart_sock_[YOUR_SMART_SOCK_SERIAL_NUMBER].attributes.battery}}"
      unit_of_measurement: '%'
    owlet_rssi:
      value_template: "{{states.sensor.owlet_smart_sock_[YOUR_SMART_SOCK_SERIAL_NUMBER].attributes.ble_rssi}}"
      unit_of_measurement: dBm
    owlet_monitoring_status:
      value_template: "{{states.sensor.owlet_smart_sock_[YOUR_SMART_SOCK_SERIAL_NUMBER].attributes.ble_rssi}}"
      unit_of_measurement: dBm
```

In the ha folder, you can find example configuration and automation yaml files that you can use with a docker installation to output data to a single csv file.
