# IoT Plant Monitor
This project is essentially a smart watering system that can detect the current temperature, humidity, intensity of light, and soil moisture of a plant of your choosing and displays them on Blynk. You are also able to pump water into the plants by turning on the Switch toggle in Blynk. 

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Alison L | Cupertino High School | Computer Science/Product Design | Incoming Sophomore

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Photo of myself](IMG_5211.jpg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My final milestone was finishing everything up and making a setup that can not only track the plant's information but also pump water into the plant. I had to order a tube that can connect to the water pump to be able to carry water from a bowl of water into the plant itself. My motor would not work for the longest time because I had been powering my board with 3.3 volts because that was the amount the ESP8266 required, except my motor need 5 volts. So, once I plugged the wire that was connecting the VCC in the motor driver board to 5 volts in the arduino, my motor worked and could pump water into my plant. A modification I did for this project was using a LED and a buzzer to notify me when the soil was too dry. After wiring the LED and the buzzer up, I edited my code that would get the LED to light up and the buzzer to sound whenever the soil moisture was too dry. Something I noticed was that the higher the number being displayed for soil moisture meant the drier the soil instead of the other way around. So, in the code I had to write that whenever the soil moisture is greater than a certain amount, the LED would flash and the buzzer would sound. 

# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My second milestone was mostly getting familiar with Blynk and using the Arduino IDE, as this is my first time using such programs. I started off by connecting my Arduino board to Blynk, then I started adding virtual pins into my Blynk dashboard. A big step I took for my project was actually trying it out. I inputted code into the Arduino IDE, then I put my soil moisture sensor in a plant and had the temperature, humidity, soil moisture etc. data to be displayed on Blynk. You are also able to turn on the water pump by pressing the on and off button on the Blynk dashboard. The main issue that I had to fix for this milestone was getting my Arduino Uno online in Blynk, which was mostly due to my ESP8266 wifi module.

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone was first building my circuit and making sure that all the necessary parts were wired correctly. Then, I made sure that my soil moisture sensor and my humidity and temperature sensor worked by plugging my board into my computer, then I imputted code into the Arduino IDE that would display the temperature, humidity, and soil moisture on the serial monitor. A problem I faced was that my ESP8266 chip could not be plugged directly into the breadboard, so I had to order an adapter for it. It was very frustrating and took a lot of time get the wifi module to work, but with help I managed to get it to work and then I could continue with my project.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Below is the main code used to send all the data collected from the sensors to Blynk:
```c++
#define BLYNK_TEMPLATE_ID ""
#define BLYNK_TEMPLATE_NAME ""
#define BLYNK_AUTH_TOKEN ""

#define BLYNK_PRINT Serial

#include <ESP8266_Lib.h>
#include <BlynkSimpleShieldEsp8266.h>

char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = "ssid";
char pass[] = "password";

#include <SoftwareSerial.h>
SoftwareSerial EspSerial(2, 3); // RX, TX

#define ESP8266_BAUD 9600
ESP8266 wifi(&EspSerial);

#include <DHT.h>
#define DHTPIN 4       // The pin connected to the DHT11 sensor
#define DHTTYPE DHT11  // DHT 11
DHT dht(DHTPIN, DHTTYPE);

#define lightPin A0
#define moisturePin A1
#define pumpA 8

double roomHumidity = 0;
double roomTemperature = 0;

BlynkTimer timer;

BLYNK_WRITE(V0)
{
  if (param.asInt() == 1) {
    digitalWrite(pumpA, HIGH);
  } else {
    digitalWrite(pumpA, LOW);
  }
}

int readMoisture() {
  return analogRead(moisturePin);
}

int readLight() {
  return analogRead(lightPin);
}

void readDHT() {
  roomHumidity = dht.readHumidity();
  roomTemperature = dht.readTemperature();
}

void myTimerEvent()
{
  readDHT();
  int light = readLight();
  int moisture = readMoisture();

  if (!isnan(roomHumidity) && !isnan(roomTemperature)) {
    Serial.print("Humidity: ");
    Serial.print(roomHumidity);
    Serial.print(" %\t");
    Serial.print("Temperature: ");
    Serial.print(roomTemperature);
    Serial.println(" *C");
    
    Blynk.virtualWrite(V4, roomHumidity);
    Blynk.virtualWrite(V5, roomTemperature);
  }
  Blynk.virtualWrite(V6, light);
  Blynk.virtualWrite(V7, moisture);
}

void alert(){
  const int buzzerPin = 10; // Change this to the desired digital pin
const int ledPin = 9;  // Change this to the desired digital pin for the LED

void setup() {
  pinMode(buzzerPin, OUTPUT);
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // Sound the buzzer with a frequency of 1000 Hz for 500 milliseconds (0.5 seconds)
  tone(buzzerPin, 1000);
  delay(500);
  
  // Silence the buzzer for 500 milliseconds
  noTone(buzzerPin);
  delay(500);
    for (int brightness = 0; brightness <= 255; brightness++) {
    analogWrite(ledPin, brightness);
    delay(10); // Adjust the delay time to control the speed of the glow
}
  for (int brightness = 255; brightness >= 0; brightness--) {
    analogWrite(ledPin, brightness);
    delay(10); // Adjust the delay time to control the speed of the glow
  }
}

void setup()
{
  // Debug console
  Serial.begin(115200);

  dht.begin(); // Initialize DHT sensor

  EspSerial.begin(ESP8266_BAUD);
  delay(10);

  Blynk.begin(auth, wifi, ssid, pass);

  timer.setInterval(1000L, myTimerEvent);

  pinMode(pumpA, OUTPUT);
}

void loop()
{
  Blynk.run();
  timer.run(); // Initiates BlynkTimer
}


```
Here is the code I used to test the DHT11 humidity and temperature sensor:
```c++
#include "DHT.h"

#define DHTPIN 4  // The pin connected to the DHT11 sensor

// Uncomment the type of sensor in use:
#define DHTTYPE DHT11   // DHT 11 

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600); 
  Serial.println("DHTxx test!");

  dht.begin();
}

void loop() {
  // Wait a few seconds between measurements
  delay(2000);

  // Reading temperature or humidity takes about 250 milliseconds!
  float h = dht.readHumidity();
  // Read temperature as Celsius (the default)
  float t = dht.readTemperature();

  // Check if any reads failed and exit early (to try again)
  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  Serial.print("Humidity: "); 
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature: "); 
  Serial.print(t);
  Serial.println(" *C");
}

```
Here is the code I used to test the soil moisture sensor and the photoresister:
```c++
const int soilMoisturePin = A1; // Connect the capacitive soil moisture sensor to analog pin A0
const int photoResistorPin = A0; // Connect the photoresistor to analog pin A1

void setup() {
  Serial.begin(9600);
}

void loop() {
  // Read soil moisture value
  int soilMoistureValue = analogRead(soilMoisturePin);
  int moisturePercentage = map(soilMoistureValue, 0, 1023, 0, 100);
  Serial.print("Soil Moisture Percentage: ");
  Serial.print(moisturePercentage);
  Serial.println("%");

  // Read illumination value
  int illuminationValue = analogRead(photoResistorPin);
  Serial.print("Illumination Value: ");
  Serial.println(illuminationValue);

  delay(1000); // Delay between readings, adjust as needed
}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Elegoo Uno R3 Board with USB Cable | Microcontroller | $15.99 | <a href="[https://www.amazon.com/ELEGOO-Board-ATmega328P-ATMEGA16U2-Compliant/dp/B01EWOE0UU/ref=sr_1_3?keywords=elegoo+uno+r3+board&qid=1690488175&sr=8-3](https://www.amazon.com/ELEGOO-Controller-ATmega328P-Compatible-Arduino/dp/B0B6VV7MS7/ref=sr_1_4?keywords=elegoo+uno+r3+board&qid=1690488247&sr=8-4)/"> Link </a> |
| Solderless Breadboards | Base for all the components | $9.99 for 4pc | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6](https://www.amazon.com/Breadboards-Solderless-Breadboard-Distribution-Connecting/dp/B07DL13RZH/ref=sr_1_3?crid=1KRC08FNZVCYJ&keywords=breadboard&qid=1690488491&sprefix=breadboar%2Caps%2C198&sr=8-3)/"> Link </a> |
| ESP8266 Module | Enables the microcontroller to connect to WiFi | $8.99 for 3 pc | <a href="https://www.amazon.com/Breadboards-Solderless-Breadboard-Distribution-Connecting/dp/B07DL13RZH/ref=sr_1_3?crid=1KRC08FNZVCYJ&keywords=breadboard&qid=1690488491&sprefix=breadboar%2Caps%2C198&sr=8-3/"> Link </a> |
| Soil Moisture Sensor | Sensor to track the plant's soil moisutre | $11.99 for 5 pc | <a href="https://www.amazon.com/Capacitive-Moisture-Corrosion-Resistant-Detection/dp/B07SYBSHGX/ref=sr_1_16?crid=1BVQIFJEXQ443&keywords=soil+moisture+sensor&qid=1691435304&sprefix=soil+moisutre+senso%2Caps%2C167&sr=8-16/"> Link </a> |
| DHT11 Humidity Sensor | Sensor to track the temperature and humidity of the room | $9.99 for 5 pc | <a href="https://www.amazon.com/HiLetgo-Temperature-Humidity-Digital-3-3V-5V/dp/B01DKC2GQ0/ref=sr_1_3?crid=1QIFNX5NG5UNO&keywords=dht11+temperature+and+humidity+sensor&qid=1691435425&sprefix=dht11%2Caps%2C214&sr=8-3/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
