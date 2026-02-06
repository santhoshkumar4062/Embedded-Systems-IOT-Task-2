
# ENVIRONMENT MONITORING - TEMPERATURE & HUMIDITY SENSOR DHT22 WITH OLED DISPLAY MODULE:

----
## INTRODUCTION:


----
### CIRCUIT DIAGRAM:
<img width="791" height="551" alt="Screenshot 2026-02-06 085644" src="https://github.com/user-attachments/assets/d92cd5b9-f615-4fd5-ba76-d9cd0a016cde" />

----
#### PIN CONNECTIONS:
The Diagram

*DHT22 Sensor*
 - VCC - ESP32 (3.3V)
 - GND - ESP32 (GND)
 - DATA - ESP32 (GPIO4) Or Similar Digital Pin, Floating Label Suggests GPIO4

*OLED Display Module*
 - VCC → ESP32 3.3V
 - GND → ESP32 GND
 - SCK → ESP32 GPIO18 (SPI CLK, labeled as such)
 - MOSI → ESP32 GPIO23 (SPI data out)
 - RES → ESP32 GPIO16 (reset)
 - DC → ESP32 GPIO17 (data/command)
 - CS → ESP32 GPIO5 (chip select)
 - Pull-up resistor (4.7k-10kΩ) on DHT22 DATA line to VCC ensures stable single-wire Communication

----
#### WORKING PRINCIPAL:
The ESP32


----
#### ESP32 CODE:
Install Libraries:



----
#### CODE EXPLANATION:

- Libraries:
- Setup:
- Loop:

---- 
#### REAL-WORLD APPLICATONS:
- 





