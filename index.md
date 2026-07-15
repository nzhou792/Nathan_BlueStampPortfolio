# Wrist Rehabilitation Device
<!---
---Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!---

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```
-->

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Nathan Z | Leland | Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)

# Starter Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/NxggbA9NjnA?si=uwGbsBWsHdI1Mzg9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- The components of this starter project (Jitterbug) include a battery holder to hold a 3V coin cell battery that powers the bug, two LED lights that light up upon powering on, a vibration motor to allow the bug to jitter, and legs made out of wire that allow it to stand.
- I have successfully attached all of the components to the PCB and soldered them in place, along with making all of the legs the same length.
- A challenge I'm facing is that my on/off switch is broken and is unable to turn on without falling apart. I hope to avoid a mistake like this in the future by making sure my individual components are functioning properly before putting them together.

```
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 
```
# First Milestone
```
**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/HHPdgFPQ0NM?si=8KZ95WOFw8eMHYcd" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


- So far, I have successfuly wired various physical components to the breadboard, such as an Arduino Nano, flex sensor, Piezo buzzer, IMU board (accelerometer), and Bluetooth module. I have successfully gotten the flex sensor to actively display its flex value and activate the Piezo buzzer when it passes a certain threshold.
- I am currently struggling to 

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
| Arduino Nano ESP32 | Microcontroller, contains code | $19.30 | <a href="https://www.amazon.com/Arduino-ABX00083-Bluetooth-MicroPython-Compatible/dp/B0C947BHK5?th=1"> Link </a> |
| Flex Sensor (4.5”) | Used to detect bend angle of the wrist | $17.95 | <a href="https://www.sparkfun.com/flex-sensor-4-5.html"> Link </a> |
| Piezo Buzzer | Emits a sound when wrist bends a certain amount| $6.99 | <a href="https://www.amazon.com/mxuteuk-Electronic-Computers-Printers-Components/dp/B07VK1GJ9X/ref=sr_1_6?dib=eyJ2IjoiMSJ9.wAyBeRS6gVe44PjVRBtGDNKks-EH_IddvvbrS5lP7ws8lbLh8RNqBaH9kb5xhXhl7MI8WQtio_tKkeH1YD6_yiGX7h2PwsC4Xm4emaporthsw8TqLLYHf3gw3xr_dTGaPUfmfdeCkpORNEhcAxsMfZYgGrRB0yphDoV5bsa_IT1CHUCMRTKJWfTyijyewlOycoYia-zs1sdJNdwYkWur90jqeI909HZS__vONk1Wv9DgVwvs1mk42ujIPDjLdWqpExujHId0l_C_ESKqP2n46A47I6sWRHoHtI9DI8k_ecA.kZsqmeDgDZNGjmc9dBGyjua1olRzvS49-2NieqlP5hI&dib_tag=se&keywords=piezo+buzzer&qid=1719416785&sr=8-6"> Link </a> |
| Accelerometer/Gyroscope | Detects speed/angle of wrist | $19.95 | <a href="https://www.adafruit.com/product/5543?gad_source=1&gclid=Cj0KCQjw4MSzBhC8ARIsAPFOuyW3bKrwhMSo2VoSfvSt319uDnnbDld4MoYm0IzXAV2mbivYMjEGez4aApeGEALw_wcB"> Link </a> |
| Jumper Wires | Used to wire components to the microcontroller | $6.98 | <a href="https://www.amazon.com/Elegoo-EL-CP-004-Multicolored-Breadboard-arduino/dp/B01EV70C78/ref=sr_1_3?crid=1GJIWX8C47LE6&keywords=jumper%2Bwires&qid=1689572180&sprefix=jumper%2Bwire%2Caps%2C200&sr=8-3&th=1"> Link </a> |
| Wrist Brace | Sleeve on wrist that the components are attached to | $15.97 ]<a href="https://www.amazon.com/Sparthos-Wrist-Support-Sleeves-Pair/dp/B074CXL9RM/ref=sxin_16_pa_sp_search_thematic-asin_sspa?content-id=amzn1.sym.f5052e1c-21bb-4068-ada8-6befb6325d04%3Aamzn1.sym.f5052e1c-21bb-4068-ada8-6befb6325d04&crid=BSDK6TEHKM0P&cv_ct_cx=wrist%2Bcompression%2Bsleeve&dib=eyJ2IjoiMSJ9.a0DsiZrtl24MGErE3gc3hs-1seJpCWa444LFuc4uL7pQ2OfUK_CsEha6Uf9uNkDHGCFhBOGcesu0YlU33vWUZg.4T09Mf5m41lcN3unhAgnkf-BS-7wLZL42PAvfgzOW1I&dib_tag=se&keywords=wrist%2Bcompression%2Bsleeve&pd_rd_i=B07G4JCSJ7&pd_rd_r=5b8b03e2-eea7-49ee-9e5f-8cbb186e681e&pd_rd_w=S03mj&pd_rd_wg=NPat3&pf_rd_p=f5052e1c-21bb-4068-ada8-6befb6325d04&pf_rd_r=0BBVYDM9P8428SY3RMC3&qid=1719355435&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sprefix=wrist%2Bcompress%2Caps%2C446&sr=1-2-baa1f287-65d3-41a3-a655-8bbba0531537-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9zZWFyY2hfdGhlbWF0aWM&th=1&psc=1"> Link </a> |
<!---
# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
-->
