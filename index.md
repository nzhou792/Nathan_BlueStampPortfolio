# Wrist Rehabilitation Device

This device aims to detect speed and bend angle of the wrist using an accelerometer and flex sensor attached to a wrist sleeve, and determines whether the form of the wrist is good or bad. In addition to this, the device also consists of two LEDs that flash red or green depending on form, and a Piezo buzzer that emits noise when the wrist bends too far. An Arduino WiFi server has been set up so that the acceleration, bend angle, form, and adjustment based on form can be monitored live on a website.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Nathan Z | Leland | Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)

# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/x5zgZh8wqlc?si=WhV2SBc7aaDNutqB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- Since the previous milestone, I have attached the flex sensor and accelerometer to the wrist sleeve using neoprene fabric and lengthened the wires so I can move the wrist sleeve around. On the website, I have added a display for good/bad form and what adjustment should be made if the wrist is in bad form (turn wrist up/down).
- My biggest challenges here at BlueStamp were working on the starter project (because I had little experience with engineering), learning how to wire components to a microcontroller, and figuring out how to get components to function and create websites using code in the Arduino IDE.
- Some topics I learned about include physical engineering skills like soldering components together, various circuit components like microcontrollers, sensors, and resistors, and approaching a big project in smaller steps (thinking more like an engineer).
- In the future, I hope to work with bigger projects that involve more components, as well as possibly learning CAD and how to 3D-print custom parts. 



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CR1Y5pQMNKk?si=fOGP0NJ93SD7WFA_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- I have written code that allows the x-axis acceleration detected by the accelerometer to be actively displayed on the serial monitor. I also set up a Wi-Fi server that allows me to monitor the acceleration and flex sensor bend angle in real time on a website.
- So far, the project seems like it focuses much more on specific small components and the code that gets those components to work. This has been surprising because I initially envisioned a project much more focused on physical construction.
- Some challenges I have faced so far are successfully wiring the flex sensor to the breadboard and making its values more accurate, as well as figuring out how to use HTML code to set up the website.
- Before my last milestone, I must get the components wired and attached to a wrist sleeve in order to create the final functioning device. 

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**


<iframe width="560" height="315" src="https://www.youtube.com/embed/HHPdgFPQ0NM?si=8KZ95WOFw8eMHYcd" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


- So far, I have successfuly wired various physical components to the breadboard, such as an Arduino Nano, flex sensor, Piezo buzzer, IMU board (accelerometer), and Bluetooth module. I have successfully gotten the flex sensor to actively display its flex value and activate the Piezo buzzer when it passes a certain threshold.
- I am currently struggling to get the Bluetooth module to successfully connect to the computer, and the flex sensor's values could be more accurate.
- Next, I will focus on writing code for the accelerometer to obtain its values, and hopefully get the Arduino Nano to wirelessly connect to my computer.

# Starter Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/NxggbA9NjnA?si=uwGbsBWsHdI1Mzg9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- The components of this starter project (Jitterbug) include a battery holder to hold a 3V coin cell battery that powers the bug, two LED lights that light up upon powering on, a vibration motor to allow the bug to jitter, and legs made out of wire that allow it to stand.
- I have successfully attached all of the components to the PCB and soldered them in place, along with making all of the legs the same length.
- A challenge I'm facing is that my on/off switch is broken and is unable to turn on without falling apart. I hope to avoid a mistake like this in the future by making sure my individual components are functioning properly before putting them together.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
#include <Adafruit_LSM6DS.h>
#include <Adafruit_LIS3MDL.h>
#include <WiFi.h>
#include <ESPAsyncWebServer.h> 
#include <Arduino.h>
#include <Wire.h>

Adafruit_LSM6DS lsm6ds;
Adafruit_LIS3MDL lis3mdl;
AsyncWebServer server(80); 

const char* ssid = "bluestamp_j10";
const char* password = "blueblue123";

const int FLEX_PIN = A0; // Pin connected to voltage divider output
const int buzzerPin = D8; // buzzer to arduino pin D8
const int ledPinRed = A2;
const int ledPinGreen = A1;
const float VCC = 3.3; // Measured voltage of ESP32 (usually 3.3V)
const float R_DIV = 10000.0; // Measured resistance of resistor

const float STRAIGHT_RESISTANCE = 10000.0; // resistance when straight
const float BEND_RESISTANCE = 20000.0; // resistance at 90 deg

volatile float ax = 0;
volatile float bend_angle = 0; // Global variable to store the flex bend value
volatile bool good = true;
char feedback_status[32] = "Good form"; // Global variable to store human-readable feedback

// HTML page stored in flash memory using Raw String Literal
const char index_html[] PROGMEM = R"rawliteral(
<!DOCTYPE html>
<html>
<head>
    <title>ESP32 Dashboard</title>
</head>
<body>
    <h1>ESP32 Dashboard</h1>
    <p> X-Axis Acceleration: <span id="ax">0.00</span> m/s&sup2;</p>
    <p> Flex Sensor Bend: <span id="bend">0.00</span>&deg;</p>
    <p> Form: <span id="good">Good</span></p>
    <p> Adjustment: <span id="feedback">Good form</span></p>
    <script> 
    setInterval(() => {
        fetch('/data')
            .then(r => r.json())
            .then(d => {
                document.getElementById('ax').textContent = d.x.toFixed(2);
                document.getElementById('bend').textContent = d.bend.toFixed(2);
                // Displays "Good" if d.good is 1 (true), otherwise "Bad"
                document.getElementById('good').textContent = d.good === 1 ? "Good" : "Bad";
                // Displays wrist correction or good form message
                document.getElementById('feedback').textContent = d.feedback;
            })
            .catch(err => console.error("Error fetching data:", err));
    }, 100);
    </script>
</body>
</html>
)rawliteral";

void setup() {
  Serial.begin(9600);
  delay(1000);

  // Set ESP32 to Station mode
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  
  Serial.println("Connecting to Wi-Fi...");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("\nConnected to the Wi-Fi network!");
  Serial.print("Local IP Address: ");
  Serial.println(WiFi.localIP());

  // Route to serve the HTML page
  server.on("/", HTTP_GET, [](AsyncWebServerRequest* request) {
    request->send(200, "text/html", index_html);
  });

  // Route to serve JSON data
  server.on("/data", HTTP_GET, [](AsyncWebServerRequest* request) {
    char buf[160];
    // Formats JSON string to include acceleration, bend angle, form boolean, and text feedback
    snprintf(buf, sizeof(buf), "{\"x\":%.3f,\"bend\":%.3f,\"good\":%d,\"feedback\":\"%s\"}", ax, bend_angle, good ? 1 : 0, feedback_status);
    request->send(200, "application/json", buf);
  });

  bool lsm6ds_success, lis3mdl_success;

  delay(5000);
  lsm6ds_success = lsm6ds.begin_I2C();
  lis3mdl_success = lis3mdl.begin_I2C();
  
  Serial.print("Accelerometer range set to: ");
  switch (lsm6ds.getAccelRange()) {
    case LSM6DS_ACCEL_RANGE_2_G: Serial.println("+-2G"); break;
    case LSM6DS_ACCEL_RANGE_4_G: Serial.println("+-4G"); break;
    case LSM6DS_ACCEL_RANGE_8_G: Serial.println("+-8G"); break;
    case LSM6DS_ACCEL_RANGE_16_G: Serial.println("+-16G"); break;
  }

  Serial.print("Accelerometer data rate set to: ");
  switch (lsm6ds.getAccelDataRate()) {
    case LSM6DS_RATE_SHUTDOWN: Serial.println("0 Hz"); break;
    case LSM6DS_RATE_12_5_HZ: Serial.println("12.5 Hz"); break;
    case LSM6DS_RATE_26_HZ: Serial.println("26 Hz"); break;
    case LSM6DS_RATE_52_HZ: Serial.println("52 Hz"); break;
    case LSM6DS_RATE_104_HZ: Serial.println("104 Hz"); break;
    case LSM6DS_RATE_208_HZ: Serial.println("208 Hz"); break;
    case LSM6DS_RATE_416_HZ: Serial.println("416 Hz"); break;
    case LSM6DS_RATE_833_HZ: Serial.println("833 Hz"); break;
    case LSM6DS_RATE_1_66K_HZ: Serial.println("1.66 KHz"); break;
    case LSM6DS_RATE_3_33K_HZ: Serial.println("3.33 KHz"); break;
    case LSM6DS_RATE_6_66K_HZ: Serial.println("6.66 KHz"); break;
  }
  
  pinMode(FLEX_PIN, INPUT);
  pinMode(buzzerPin, OUTPUT);
  pinMode(ledPinRed, OUTPUT);
  pinMode(ledPinGreen, OUTPUT);

  server.begin();
}

void loop() {
  sensors_event_t accel, gyro, mag, temp;
  lsm6ds.getEvent(&accel, &gyro, &temp);
  lis3mdl.getEvent(&mag);

  int flexADC = analogRead(FLEX_PIN);
  float flexV = flexADC * VCC / 4095.0;
  float flexR = R_DIV * (VCC / flexV - 1.0);
  float angle = map(flexR, STRAIGHT_RESISTANCE, BEND_RESISTANCE, 0, 90.0);
  angle += 10;

  bool goodForm = (accel.acceleration.x <= 0.7) && ((angle < 15 ) && (angle > -15));
  bool badFormUp = (accel.acceleration.x > 0.7) || (angle >= 15);
  bool badFormDown = (angle <= -15);

  Serial.print("Accelerometer X Value: ");
  Serial.println(accel.acceleration.x, 4);
  Serial.print("Bend: ");
  Serial.print(angle);
  Serial.println(" degrees");

  ax = accel.acceleration.x;
  bend_angle = angle; 
  good = goodForm;

  if (goodForm) {
    Serial.println("Good form");
    digitalWrite(buzzerPin, LOW);
    digitalWrite(ledPinGreen, HIGH);
    digitalWrite(ledPinRed, LOW);
    strcpy(feedback_status, "Good form");
  } else {
    Serial.println("Bad form");
    digitalWrite(buzzerPin, HIGH);
    digitalWrite(ledPinRed, HIGH);
    digitalWrite(ledPinGreen, LOW);
    delay(300);
    digitalWrite(buzzerPin, LOW);
    if (badFormUp) {
      Serial.println("Turn wrist up");
      strcpy(feedback_status, "Turn wrist up");
    } else {
      Serial.println("Turn wrist down");
      strcpy(feedback_status, "Turn wrist down");
    }
  }

  delay(1000);
}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Nano ESP32 | Microcontroller, contains code | $19.30 | <a href="https://www.amazon.com/Arduino-ABX00083-Bluetooth-MicroPython-Compatible/dp/B0C947BHK5?th=1"> Link </a> |
| Flex Sensor (4.5”) | Used to detect bend angle of the wrist | $17.95 | <a href="https://www.sparkfun.com/flex-sensor-4-5.html"> Link </a> |
| Piezo Buzzer | Emits a sound when wrist bends a certain amount| $6.99 | <a href="https://www.amazon.com/mxuteuk-Electronic-Computers-Printers-Components/dp/B07VK1GJ9X/ref=sr_1_6?dib=eyJ2IjoiMSJ9.wAyBeRS6gVe44PjVRBtGDNKks-EH_IddvvbrS5lP7ws8lbLh8RNqBaH9kb5xhXhl7MI8WQtio_tKkeH1YD6_yiGX7h2PwsC4Xm4emaporthsw8TqLLYHf3gw3xr_dTGaPUfmfdeCkpORNEhcAxsMfZYgGrRB0yphDoV5bsa_IT1CHUCMRTKJWfTyijyewlOycoYia-zs1sdJNdwYkWur90jqeI909HZS__vONk1Wv9DgVwvs1mk42ujIPDjLdWqpExujHId0l_C_ESKqP2n46A47I6sWRHoHtI9DI8k_ecA.kZsqmeDgDZNGjmc9dBGyjua1olRzvS49-2NieqlP5hI&dib_tag=se&keywords=piezo+buzzer&qid=1719416785&sr=8-6"> Link </a> |
| Accelerometer/Gyroscope | Detects speed/angle of wrist | $19.95 | <a href="https://www.adafruit.com/product/5543?gad_source=1&gclid=Cj0KCQjw4MSzBhC8ARIsAPFOuyW3bKrwhMSo2VoSfvSt319uDnnbDld4MoYm0IzXAV2mbivYMjEGez4aApeGEALw_wcB"> Link </a> |
| Jumper Wires | Used to wire components to the microcontroller | $6.98 | <a href="https://www.amazon.com/Elegoo-EL-CP-004-Multicolored-Breadboard-arduino/dp/B01EV70C78/ref=sr_1_3?crid=1GJIWX8C47LE6&keywords=jumper%2Bwires&qid=1689572180&sprefix=jumper%2Bwire%2Caps%2C200&sr=8-3&th=1"> Link </a> |
| Wrist Brace | Sleeve on wrist that the components are attached to | $15.97 | <a href="https://www.amazon.com/Sparthos-Wrist-Support-Sleeves-Pair/dp/B074CXL9RM/ref=sxin_16_pa_sp_search_thematic-asin_sspa?content-id=amzn1.sym.f5052e1c-21bb-4068-ada8-6befb6325d04%3Aamzn1.sym.f5052e1c-21bb-4068-ada8-6befb6325d04&crid=BSDK6TEHKM0P&cv_ct_cx=wrist%2Bcompression%2Bsleeve&dib=eyJ2IjoiMSJ9.a0DsiZrtl24MGErE3gc3hs-1seJpCWa444LFuc4uL7pQ2OfUK_CsEha6Uf9uNkDHGCFhBOGcesu0YlU33vWUZg.4T09Mf5m41lcN3unhAgnkf-BS-7wLZL42PAvfgzOW1I&dib_tag=se&keywords=wrist%2Bcompression%2Bsleeve&pd_rd_i=B07G4JCSJ7&pd_rd_r=5b8b03e2-eea7-49ee-9e5f-8cbb186e681e&pd_rd_w=S03mj&pd_rd_wg=NPat3&pf_rd_p=f5052e1c-21bb-4068-ada8-6befb6325d04&pf_rd_r=0BBVYDM9P8428SY3RMC3&qid=1719355435&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sprefix=wrist%2Bcompress%2Caps%2C446&sr=1-2-baa1f287-65d3-41a3-a655-8bbba0531537-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9zZWFyY2hfdGhlbWF0aWM&th=1&psc=1"> Link </a> |
<!---
# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
-->
