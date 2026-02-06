
# ENVIRONMENT MONITORING - TEMPERATURE & HUMIDITY SENSOR DHT22 WITH OLED DISPLAY MODULE:

----
## INTRODUCTION:
This Mini Project Features an ESP32 Micro-Controller Interfaced with a DHT22 Temperature and Humidity Sensor and an SSD1306 OLED Display Module via SPI. ItMonitors Environmental Conditions and Displays Real-Time Temperature and Humidity Reading on the OLED Sceen, Ideal for IOT Prototypes.

----
### CIRCUIT DIAGRAM:
<img width="791" height="551" alt="Screenshot 2026-02-06 085644" src="https://github.com/user-attachments/assets/d92cd5b9-f615-4fd5-ba76-d9cd0a016cde" />

----
#### PIN CONNECTIONS:
The Diagram shows Labeled Connections from DHT22, ESP32, and OLED. Key Mapping Based on Standard ESP32 WROOM-32 Pins and SPI Setup.

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
The ESP32 Reads Digital Temperature (–40°C to 80°C ±0.5°C) and Humidity (0-100% ±2%) Data From DHT22 Every 2 Seconds via its Proprietary one-wire protocol. Data is processed and sent to the OLED over SPI (High-Speed Serial Interface), where the SSD1306 Controller Renders Pixel Graphics to show values like "24.6°C 44%". The Loop Repeats for Continous Monitoring.

----
#### ESP32 CODE:
Install Libraries: DHT Sensor Library by AdaFruit, AdaFruit SSD1306, AdaFruit GFX, Use ESP32 Board in Arduino IDE.

- #include <DHT.h>
- #include <SPI.h>
- #include <Adafruit_GFX.h>
- #include <Adafruit_SSD1306.h>
  
- #define DHTPIN 4         // DHT22 data pin
- #define DHTTYPE DHT22   // Sensor type
- DHT dht(DHTPIN, DHTTYPE);
  
- #define SCREEN_WIDTH 128
- #define SCREEN_HEIGHT 64
- #define OLED_RESET -1
- #define SCREEN_ADDRESS 0x3C     // SPI mode uses CS pin, but init like I2C for simplicity
  
- Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &SPI, 5, 17, 16);  // CS=5, DC=17,
  
- void setup() {
  - Serial.begin(115200);
  - dht.begin();
  - if(!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
    - Serial.println(F("SSD1306 allocation failed"));
    - for(;;);
 - }
  - display.clearDisplay();
  - display.setTextSize(1);
  - display.setTextColor(SSD1306_WHITE);
 - }

- void loop() {
  - delay(2000);
  - float h = dht.readHumidity();
  - float t = dht.readTemperature();

  - display.clearDisplay();
  - display.setCursor(0,0);
  - display.print("Temp: ");
  - display.print(t);
  - display.println(" C");
  - display.print("Hum: ");
  - display.print(h);
  - display.println(" %");
  - display.display();
  - Serial.print("Humidity: "); Serial.print(h); Serial.print(" %\tTemperature: "); Serial.
  - }


*Note:* 
- For Pur SPI, Adjust Display. Begin(SSD1306_SPI) And Specify SCK/MOSI Pins via SPI.begin (SCK, MISO, MOSI, CS). This Hybrid init works for many Modules. Tests Pins Match Diagram.
  
----
#### CODE EXPLANATION:

*Libraries:*
 - DHT For Sensor Protocol: GFX/SSD1306 FOR OLED Graphics and SPI Control.
*Setup:*
 - Initializes Serial for Debug, DHT Sensor, And OLED (Checks Allocation). Clears and Configures Display Font/Colour.
*Loop:*
 - Reads H/T Every 2S (DHT22 Min Interval), clears OLED, Prints values at Cursor Positior Updates Displays. Serial Mirrors for Monitoring. Errors Handling via NaN Checks in Full Code.

---- 
#### REAL-WORLD APPLICATONS:

*Home Automation:*
 - HVAC Control Based on Room Climate.
*Green House:*
 - Crop Monitoring for Optional Growth.
*Wearable/IoT:*
 - Portable Weather Stations Or Fridge Monitors.
*Industrial*
 - WareHouse Humidity Alerts to Prevent Damage. Scalable to WIFI For Cloud Logging.






