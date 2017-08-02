# *Water Level Sensor*
## Part I. General Overview
### What is the sensor and what does it do?

~~The Water Level Sensor from RobotDyn measures water level in [units of height].~~ The Water Level Sensor detects the presence of water (i.e. when water touches the metal plates on the sensor), and is therefore used as a proxy.
This will be finalized once the test results are in

### Datasheet
~~[PMS 3003 Datasheet](https://github.com/JordanFleming/sensor_documentation/blob/master/datasheets/PMS3003_Datasheet.pdf)~~
No data sheet currently exists for the water 
### Connection Images
<img src="https://github.com/JordanFleming/sensor_documentation/blob/master/pms3003/images/PMS3003_pin_out.jpg?raw=true" width="650" height="400">

The following image describes how to connect PMS3003 to a Particle **Photon** board.

<img src="https://github.com/JordanFleming/sensor_documentation/blob/master/pms3003/images/connection_diagram_pms30003.png?raw=true" width="700" height="500">

### Working Logic / Functionality
#### Output
* Type: UART
* Default baud rate: 9600 bps
  * Parity: None
  * Stop bit: 1 bit
* Length: 24 bytes
  <img src="https://github.com/JordanFleming/sensor_documentation/blob/master/pms3003/images/bit_parsing.jpg?raw=true">
