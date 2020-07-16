# Hardware-reference-design-for-telematics-devices
Reference circuit design for telematics devices. The repository contains schematic and white notes. Main modules and controller as MC60(GSM+GPS) and stm32f103 with important points to consider. The purpose of this repository is to share my learning under non-commercial and no derivative purpose to help build strong open source community and giving back to society. The below information is for reference purpose only. I am not liable for the authenticity and accuracy of the details provided here within. Please refer to the datasheets of individual modules/libraries. Below information is important points to consider while designing any schematics and board files.

# Library Descriptions 
Below library files can be easly found via key search.
MPU-9250. 
STM32F103C8 
EEPROM W25Q16BVSS 
MC60E 
BQ24195LRGER
LM2596S

# Antenna Suggestions for MC60 Module
Antenna Suggestions:-
(For GSM) 
-a π type matching circuit is suggested to be used to adjust the RF performance
-characteristic impedance should be close to 50Ω. input power 50W. Gain (dBi) 1. 

(Optional For GSM)  
SMA Connector space.
Onboard Antenna with dimension 25x6mm.

(For GPS)
-The impedance of RF trace should be controlled as 50Ω, and the trace length 
should be kept as short as possible.
-Passive antenna gain: >0dBi, Active antenna noise <1.5dB
(For Active mode in GPS)
-Antenna powered by GNSS_VCC with voltage (2.8-4.3v). If voltage does not meet
requirements then external ldo be used.
-Inductor L1=47nH is used to prevent the RF signal from leaking into GNSS_VCC 
 and amplyfication.

-The effective bandwidth of a GPS antenna is usually measured by the
frequency band, below -10dB return loss. The bandwidth of a GPS ceramic
patch narrows with size of the patch. 

Trace Suggestions:-
The VBAT trace should be wide enough to ensure that there is not too much voltage 
drop during burst transmission. The width of trace should be no less than 2mm; 
and in principle, the longer the VBAT trace, the wider it will be.

# Battery IC BQ24195 IC 
Power consumption
-I/P voltage 3.9-17V. (VBUS pin)
-I/P current 3A.
-O/P Current 4.5A.    (SYS pin)
-Battery Voltage 4.4V. 

PIN DESCRIPTION:
Input source VBUS, battery(BAT), or both.
FOR detection of input source.
D+/D- input source detection to program the input current limit
TWO TS pins to monitor the thermistor (NTC) in each cell independently.
HIZ- high impedance state
STAT- charging status. 
ILIM- To limit maximum input current on ILIM pin (protection)
OTG- 
CE- Active low Charge Enable pin.
TS- Temperature qualification voltage input. Connect NTC
BTST- PWM high side driver positive supply.
SW- Switching node connecting to output inductor.

blink rate -charging (LOW), charging complete/charge disable(HIGH), charging fault(blinking).

status register REG08[5:4]-> 00 charging disable, 01-precharge, 10-fast charge(const I nd V)
			     11 charging done.

TS fault register REG09[2:0]


Current in boost mode
During boost mode, the status register REG08[7:6] is set to 11, the VBUS output is 5 V and the output current
can reach up to 500 mA or 1.3 A, selected via I2C (REG01[0]).

Autonomous charging cycle (i.e without host involvement)

bq24190,bq24192
charging voltage 4.208V ,current 2.048A.

# Power Consumption of each modules used
Power Requirements:-

MC60.
-GNSS_VCC supply (2.8 - 3.3 - 4.3v).
-VRTC power supply (1.5 - 2.8 - 3.3v) backup domain.
-VBAT(GSM) Supply Voltage (3.3 - 4.0 - 4.6v). Voltage drop during transmitting burst (400mV).
 Peak supply current (during transmission slot) 1.6-2A. 577us radio burst in GSM part every 4.615ms.
 voltage at digital and analog pins (0-3.08v).

STM32F103C8 power 
(2-to-3.6V).

Relay driver circuit 
(TQ2SL-L2-5V smd) -> 
(SC5-S-DC12V through hole) -> latch with 5vdc.  


IMU
-In MPU6050 for module with ldo(3-5v).
-VDD for mpu6050 chip is (2.375-3.46v). 


-Buzzer circuit -> .
-10-20mA.

-Indicator LED's 
-Vdd Gsm led 4V 10-20mA.
-Vdd Gps led 4V 10-20mA.
-Vdd suppply led 1.7V 10-20mA.


Power Regulators:-
LM2596 
(I/p range is 12-13.6v, o/p is 12v 3amp(max),  )

LM1117 (3.3V )
MIC5219 (3.25V 500mA peak o/p ldo)
MIC29302 (4.01v 1.6Amps )





