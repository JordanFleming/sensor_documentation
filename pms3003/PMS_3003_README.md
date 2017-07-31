# *PMS3003 Sensor*
## Part I. General Overview
### What is the sensor and what does it do?

The Plantower PMS3003 is a particle sensor that measures particulate matter in the air uisng laser scattering. The sensor is sensitive enough to detect 0.3 um particles.

### Datasheet
[PMS 3003 Datasheet](https://github.com/JordanFleming/sensor_documentation/blob/master/datasheets/PMS3003_Datasheet.pdf)
### Connection Images
<img src="https://github.com/JordanFleming/sensor_documentation/blob/master/pms3003/images/PMS3003_pin_out.jpg?raw=true" width="750" height="400">

<img src="https://github.com/JordanFleming/sensor_documentation/blob/master/pms3003/images/connection_diagram_pms30003.png?raw=true">

### Working Logic / Functionality
#### Output
* Type: UART
* Default baud rate: 9600 bps; Parity: None; Stop bit: 1 bit
* Length: 32 bytes
  <img src="https://github.com/JordanFleming/sensor_documentation/blob/master/pms3003/images/bit_parsing.jpg?raw=true" width="100" height="100">

## Part II. Waggle Specific
### Application
#### How does the sensor work with Photon and P I/O Cloud?
##### (link to event page on particle.io)
##### (explain how the data is displayed as a log -- link to log page on particle.io)
### Source Code from particle.io
    #include "Particle.h"

    #define PMS7003 0x01
    // #define PMS3003 0x02

    #ifdef PMS7003
    #define LENG 32
    #endif 

    #ifdef PMS3003
    #define LENG 24
    #endif 

    char buf[LENG + 2];
    int data_CRC = 0x00;




      void setup()
      {
       Serial1.begin(9600);   //use serial0
      }

      void loop()
      {
    
    if (Serial1.available() > 0)
    
    {
        
        //Particle.publish("RSG-1", String(Serial.read()), PRIVATE);
        
       if (Serial1.read() == 0x42)
            
        {
            
            Serial1.readBytes(buf,LENG-1);
            if(buf[0] == 0x4d)
            {
                data_CRC = 0x42;
                for ( int i = 0x00; i < LENG -3 ; i ++)
                {
                    data_CRC = data_CRC + buf[i] ; 
                }
                
                if ( data_CRC == (( buf[LENG - 3] << 8 ) + buf[LENG - 2]))
                {
                    String data_send;
                    for (unsigned char i = 0x00; i < LENG; i++)
                    {
                        if (buf[i] < 0x10)
                        {
                            data_send = data_send + '0';    
                        }
                        
                        data_send = data_send + String(buf[i],HEX);
                    }
                    
                    Particle.publish("PMS7003", data_send, PRIVATE);
                    
                }
            }
        }
        
        
    }
    
    delay(500);
    
    }
    
    
### Particle Data Interface with Beehive dev
### Waggle-space ID
### Data Structure
