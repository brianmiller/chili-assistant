# chili-assistant

Simple execution examples:
<br>
<br>
./ooler_service 5C:02:72:AA:BB:CC 37648-mqtt1.phospher.com > /tmp/ooler_brianooler.log 2>&1 &<br>
./ooler_service 5C:02:72:XX:YY:ZZ 37648-mqtt1.phospher.com > /tmp/ooler_wifeooler.log 2>&1 &<br>
<br>
### Example Home Assistant 'climate' card
![image](https://user-images.githubusercontent.com/342276/181801482-17fd28cc-f7e9-4a2b-a3f9-21700de43d00.png)
<details>
 <summary>Click to see Home Assistant 'climate' card yaml exmaple</summary>
 
```
- platform: mqtt
  name: "Brian's Bed"
  modes:
    - 'auto'
    - 'off'
  fan_modes:
    - "low"
    - "medium"
    - "high"
  mode_command_topic: "oolers/5C:02:72:AA:BB:CC/command/power"
  mode_command_template: '{% if value == "off" %}00{% else %}01{% endif %}'
  mode_state_topic: "oolers/5C:02:72:AA:BB:CC/state/power"
  mode_state_template: '{% if value == "01" %}auto{% else %}off{% endif %}'

  temperature_command_topic: "oolers/5C:02:72:AA:BB:CC/command/thermostat"
  temperature_state_topic: "oolers/5C:02:72:AA:BB:CC/state/thermostat"
  temperature_unit: F

  current_temperature_topic: "oolers/5C:02:72:AA:BB:CC/state/temp"

  fan_mode_command_topic: "oolers/5C:02:72:AA:BB:CC/command/fan"
  fan_mode_command_template: '{% if value == "high" %}02{% elif value == "medium" %}01{% else %}00{% endif %}'
  fan_mode_state_topic: "oolers/5C:02:72:AA:BB:CC/state/fan"
  fan_mode_state_template: '{% if value == "02" %}high{% elif value == "01" %}medium{% else %}low{% endif %}'

  max_temp: 115
  min_temp: 55

  precision: 1.0
  unique_id: "ooler_brian"
```
  </details>

<br>
<strong>Whenever time allows:</strong>
<br>
<li>Add regular polling for status updates sent to message bus, currently status updates are realized after a command is sent to the bus
<li>Containerize ooler_service and include a direct and mobile friendly UI, removing the need for Home Assistant
<li>Author and publish the message bus queues, commands, inputs and outputs
 
