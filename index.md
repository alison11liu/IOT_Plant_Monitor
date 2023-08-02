# IoT Plant Monitor
This project is essentially a smart watering system that can detect the current temperature, humidity, intensity of light, and soil moisture of a plant of your choosing and displays them on Blynk. You are also able to pump water into the plants by turning on the Switch toggle in Blynk. 

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Alison L | Cupertino High School | Software Engineering/Product Design | Incoming Sophomore

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Photo of myself](IMG_5211.jpg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My final milestone was finishing everything up and making a setup that can not only track the plant's information but also pump water into the plant. I had to order a tube that can connect to the water pump to be able to carry water from a bowl of water into the plant itself. For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My second milestone was mostly getting familiar with Blynk and using the Arduino IDE, as this is my first time using such programs. I started off by connecting my Arduino board to Blynk, then I started adding virtual pins into my Blynk dashboard. A big step I took for my project was actually trying it out. I inputted code into the Arduino IDE, then I put my soil moisture sensor in a plant and had the temperature, humidity, soil moisture etc. data to be displayed on Blynk. You are also able to turn on the water pump by pressing the on and off button on the Blynk dashboard. The main issue that I had to fix for this milestone was getting my Arduino Uno online in Blynk, which was mostly due to my ESP8266 wifi module.

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone was first building my circuit and making sure that all the necessary parts were wired correctly. Then, I made sure that my soil moisture sensor and my humidity and temperature sensor worked by plugging my board into my computer, then I imputted code into the Arduino IDE that would display the temperature, humidity, and soil moisture on the serial monitor. A problem I faced was that my ESP8266 chip could not be plugged directly into the breadboard, so I had to use male to female wires to manually wire the chip in. It was very frustrating and took a lot of time get the wifi module to work, but with help I managed to get it to work and then I could continue with my project.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

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

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
