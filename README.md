
## Repository Structure

firmware/
    Arduino source code (.ino)

documentation/
    Project report, diagrams, and technical documentation

images/
    Prototype photographs

media/
    Demonstration videos



# Smart Plant Watering System

An Arduino-based automated irrigation prototype that monitors soil moisture conditions and activates a water pump when the soil becomes dry. The system also displays real time operating information on an LCD screen.

![Smart Plant Watering System Prototype](images/completed_prototype.jpg)

## Project Overview

The purpose of this project was to design and build a low cost automated plant watering system that reduces the need for manual irrigation.

A soil moisture sensor continuously measures the condition of the soil. When the measured value crosses the defined dry soil threshold, the Arduino activates a water pump. Once sufficient moisture is detected, the pump is switched off.

The LCD provides the user with real time information about the moisture level and system operating status.

## Key Features

* Real time soil moisture monitoring
* Automatic water pump activation
* Adjustable moisture threshold
* LCD display of moisture and system status
* Low cost modular hardware
* Automatic control without continuous user input
* Tested working prototype

## System Operation

1. The soil moisture sensor measures the current soil condition.
2. The Arduino reads and processes the sensor value.
3. The measured value is compared with the programmed moisture threshold.
4. If the soil is dry, the water pump is activated.
5. If the soil has sufficient moisture, the pump remains off.
6. The LCD displays the moisture reading and watering status.

## System Architecture

```text
Soil Moisture Sensor
          │
          ▼
      Arduino UNO
       │       │
       ▼       ▼
   LCD Display   Pump Driver/Relay
                        │
                        ▼
                    Water Pump
```

## Hardware Components

* Arduino UNO
* Soil moisture sensor
* LCD display
* Mini water pump
* Pump driver or relay module
* Tubing
* Breadboard
* Jumper wires
* External power supply
* Water container

## Software and Tools

* Arduino IDE
* Arduino C/C++
* Sensor-based control logic
* Serial monitoring for testing and calibration

## Control Logic

The system uses threshold-based control:

```text
IF soil moisture indicates dry soil:
    Turn pump ON
ELSE:
    Turn pump OFF
```

The moisture threshold was adjusted through testing to distinguish between dry and adequately watered soil conditions.

## Testing

The prototype was tested under different soil moisture conditions to verify:

* Sensor response to dry and wet soil
* Correct pump activation and shutdown
* LCD status updates
* Repeatability of the watering logic
* Reliable interaction between the sensor, controller, display, and pump

## Engineering Skills Demonstrated

* Embedded system prototyping
* Arduino programming
* Sensor integration
* Control logic development
* Electrical wiring and hardware assembly
* Testing and troubleshooting
* System integration
* Technical documentation
* Iterative design improvement

## Author

**Emeka Chijioke**
Aerospace Engineering PhD Researcher
Interested in aerospace systems, automation, simulation, embedded systems, and engineering prototyping.

[LinkedIn](https://www.linkedin.com/in/emeka-chijioke) | [GitHub](https://github.com/NextGen-Engineers)

    
