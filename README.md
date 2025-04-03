# WiFiJsonDisplay Library

A simple Arduino library for fetching JSON data over WiFi and displaying it on SSD1306 OLED displays.

## Features

- Easy connection to WiFi networks
- Fetches JSON data from web APIs
- Displays parsed JSON data on SSD1306 OLED displays
- Supports Arduino Nano (with WiFi), ESP8266, and ESP32 boards
- Customizable display functions

## Installation

1. Create a folder named `WiFiJsonDisplay` in your Arduino libraries directory
   - Windows: `Documents\Arduino\libraries\`
   - Mac/Linux: `~/Arduino/libraries/`
2. Copy `WiFiJsonDisplay.h` and `WiFiJsonDisplay.cpp` into this folder
3. Restart the Arduino IDE

## Dependencies

- Adafruit_SSD1306
- Adafruit_GFX
- ArduinoJson (v6+)
- WiFi library for your board (WiFiNINA, ESP8266WiFi, etc.)

## Quick Start

```cpp
#include <WiFiJsonDisplay.h>

WiFiJsonDisplay display;

void setup() {
  Serial.begin(9600);
  
  display.begin();
  display.setWiFiCredentials("YOUR_SSID", "YOUR_PASSWORD");
  display.setAPIEndpoint("api.example.com", "/data.json");
  
  display.showText("Ready!", 0, 0, 2);
}

void loop() {
  display.fetchAndDisplayJSON();
  delay(30000); // Update every 30 seconds
}
```

## Custom Display Function

```cpp
void weatherDisplay(JsonDocument& doc, Adafruit_SSD1306* display) {
  display->setCursor(0, 0);
  display->print("Temp: ");
  display->print(doc["main"]["temp"].as<float>());
  display->println("C");
  display->display();
}

void loop() {
  display.fetchAndDisplayJSON(weatherDisplay);
  delay(30000);
}
```

## License

MIT
