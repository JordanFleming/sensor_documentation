# *Water Level Sensor*
## Part I. General Overview
### What is the sensor and what does it do?

~~The Water Level Sensor from RobotDyn measures water level in [units of height].~~ The Water Level Sensor from RobotDyn detects the presence of water (i.e. when water touches the metal plates on the sensor), and is therefore used as a proxy.
This will be finalized once the test results are in

### Datasheet
~~[Water Level Senor Datasheet](https://github.com/JordanFleming/sensor_documentation/blob/master/datasheets/PMS3003_Datasheet.pdf)~~
No data sheet currently exists for the water level sensor
### Connection Images
The following image describes how to connect PMS3003 to a Particle **Photon** board. Both sensors share the same connection diagram.


<img src="https://github.com/JordanFleming/sensor_documentation/blob/master/Water_Level_Sensor/images/WaterLevelSensor_B_Connection%20Diagram.png?raw=true" width="650" height="400">

<img src="https://github.com/JordanFleming/sensor_documentation/blob/master/Water_Level_Sensor/images/WaterLevelSensor_R_ConnectionDiagram.png?raw=true" width="650" height="400">

### Working Logic / Functionality
#### Output
* Type: Analog
* Default baud rate: 9600 bps
  [Insert data output diagram once the output is characterized.]

## Part II. Waggle Specific
### Application
#### How does the sensor work with Photon and Particle I/O Cloud?
The Water Level Sensor transmits a resistance through the analog pin on the Particle Photon.. The [source code posted below](#particle) publishes the data as a live stream of events to the Particle cloud (click [here to visit the Particle cloud event console](https://console.particle.io/events)). 

The data is not stored on the Particle cloud, you must purchase storage space through Particle or save the data to a text file -- or something similar -- in order to retain information. The Particle Photon communicates with the Particle cloud via WiFi. The data can be pushed from the Particle cloud and into Beehive dev ([for more documentation on this process, click here](#beehive)). 

#### How do I setup a Particle Photon?
[Documentation detailing how to setup the Particle Photon can be found here.](https://github.com/charihara/Experimental_Sensors/blob/master/Photon_Instructions.md)

### Source Code from particle.io <a name="particle"></a>
```C   
float out = A0; //Sensor output
int ledpin = D7; //Built_in LED

void setup() {
pinMode(out, OUTPUT);
pinMode(ledpin, OUTPUT);
}

void loop() {
int output_volt=(analogRead(out));
Serial.println(output_volt);
analogWrite(ledpin, LOW);
if (output_volt > 600);
    //analogWrite(A2, 255);
    digitalWrite(D1, HIGH);
        //else analogWrite(A2, LOW);
delay(1000);

}
```    
    
### Particle Data Interface with Beehive dev <a name="beehive"></a>

[Particle to Beehive dev source code](https://github.com/JordanFleming/sensor_documentation/blob/master/Particle_to_Beehive_plugin)
### Waggle-space ID
### Data Structure
